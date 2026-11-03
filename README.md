# Gujarat Sales Dashboard — ZSM login update

This bundle targets Firebase project `gujarat-dashboard-cd680` and includes the updated dashboard as `index.html`.

## Included changes
- Added the 14 supplied work email addresses to the ZSM access mapping.
- Each mapped account is assigned a fixed ZSM scope and the ZSM selector is locked to that name.
- Hides the HO workbook upload and area-wide ZSM selection controls for ZSM users.
- The HTML does not store or validate passwords. Authentication still uses Firebase Email/Password.

## Important setup steps
1. In Firebase Console → Authentication → Sign-in method, enable **Email/Password**.
2. In Firebase Console → Authentication → Users, create each of the 14 accounts using the email in `ZSM-ACCOUNT-SETUP.csv` and the initial password you specified. Do not put the password in GitHub or in the HTML source.
3. Require every user to change the initial password after first sign-in; a shared default password is only for onboarding.
4. Deploy `index.html` to the existing GitHub repository's root and push to `main` to trigger the included Firebase Hosting workflow.

## Data availability limitation
The current HTML reads an Excel workbook locally in the browser and does not publish the HO-uploaded workbook to other users or persist it in Firebase. ZSM accounts therefore will not automatically receive the HO's workbook just because they can log in. To share current sales data across devices, add a secure shared data source (for example, Firestore/Cloud Storage with server-enforced access rules) or safely embed a published dataset before rollout.

## Security limitation
The ZSM email-to-scope mapping and browser filters improve the UI experience but are **not a server-side security boundary**. A user who receives the complete workbook or can inspect/modify the client code may access data outside the UI filter. Do not put confidential cross-ZSM data in the client unless access is enforced by Firestore Security Rules or a trusted backend. For production, create authoritative `users/{uid}` profiles and enforce access on the data source.

## GitHub deployment workflow
The included `.github/workflows/firebase-hosting.yml` expects the repository secret:
`FIREBASE_SERVICE_ACCOUNT_GUJARAT_DASHBOARD_CD680`

If that secret has not been configured, the GitHub workflow will fail until an administrator adds the Firebase service-account JSON as a GitHub Actions secret.
