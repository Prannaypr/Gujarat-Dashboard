# Gujarat Sales Performance Dashboard — Firebase Hosting

This bundle preserves the uploaded dashboard HTML, including its existing Firebase Authentication configuration, and targets Firebase project `gujarat-dashboard-cd680`.

## Files
- `index.html` — dashboard
- `firebase.json` — Firebase Hosting configuration
- `.firebaserc` — default Firebase project
- `.github/workflows/firebase-hosting.yml` — deploys to the live Hosting channel when code is pushed to `main`

## Deploy through Firebase Console (recommended)
1. Open Firebase Console and select `gujarat-dashboard-cd680`.
2. Open **Hosting** and choose **Get started** / **Set up GitHub action**.
3. Connect the GitHub repository where these files are committed and select the `main` branch.
4. If Firebase generates its own workflow, review it before keeping both workflows; avoid duplicate deploy workflows.
5. Commit and push these files. Confirm the GitHub Actions run succeeds, then open the Hosting URL shown in Firebase Console.

## If using the included GitHub Actions workflow
1. Commit these files to the root of the repository on branch `main`.
2. In GitHub, open **Settings → Secrets and variables → Actions → New repository secret**.
3. Add secret named `FIREBASE_SERVICE_ACCOUNT_GUJARAT_DASHBOARD_CD680` containing a Firebase service-account JSON key with only the permissions needed to deploy Hosting.
4. Push to `main`, then check the **Actions** tab for deployment status.

Never put a service-account key in this repository or in `index.html`.

## Authentication and security notes
- The HTML keeps its existing Firebase Web App configuration and sign-in flow.
- Firebase Authentication must have **Email/Password** enabled, and authorized users must exist in Authentication.
- The app expects a Firestore document at `users/{uid}` with an active role profile (`role` must be `HO`, `ZSM`, `ASM`, or `CM`; `active` must be `true`).
- Client-side role filtering is not a security boundary. Before storing or serving confidential sales data from Firestore, enforce access using Firestore Security Rules. The current workbook processing happens in the user's browser.
- A successful Hosting deployment does not automatically configure Authentication providers, Firestore profiles, or security rules.

## Important
This package prepares deployment files; it does not itself publish to Firebase. Live deployment requires the repository to be connected/authorized and the GitHub Action to run successfully.
