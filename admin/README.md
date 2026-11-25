# Xaven Property Discovery Admin — setup notes

The first admin UI shell is deployed at /admin/. It intentionally does not permit sign-in until Firebase is configured.

## Required Firebase setup
1. Create/select a Firebase project.
2. Register a Web App and copy its web configuration.
3. Enable Authentication > Sign-in method > Email/Password.
4. Create the administrator account in Authentication > Users.
5. Set Authentication > Settings > Authorized domains to include xav enting.github.io (without the space; exact domain: xaventing.github.io).
6. Replace the REPLACE_* values in admin/index.html with the Firebase Web App config.
7. Configure Firestore/Storage security rules so only the designated admin UID can write. Never rely on hiding the /admin URL as security.

## Google Sheets integration
Do not publish a spreadsheet edit link or put a service-account private key in browser code. Use a protected server-side endpoint (e.g. Cloud Functions or a carefully authenticated Apps Script web app) to read/write Sheets. The endpoint must verify the Firebase ID token and authorize the admin UID before any write.

## Firebase Storage
Create a bucket and restrictive rules allowing writes only for the admin UID. Store image URLs and metadata in the project records.

## Current status
- Admin UI shell: deployed
- Firebase login: awaiting project config and admin account
- Google Sheets API: not connected
- Firebase Storage uploads: not connected
- Live project CRUD: not enabled
