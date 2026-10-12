# Port Terminal – Daily Shift Cargo Dashboard

Static website (GitHub Pages) + free Firebase Firestore database so every supervisor sees the same live data.

## 1. Create the database (5 minutes, free)
1. Go to https://console.firebase.google.com -> **Add project**.
2. **Build -> Firestore Database -> Create database** (production mode, pick a region near you, e.g. Frankfurt/Mumbai).
3. **Rules** tab -> paste the contents of `firestore.rules` -> **Publish**.
4. **Project settings (gear) -> Your apps -> Web (</>)** -> register an app -> copy the `firebaseConfig` values.
5. Open `index.html`, find `window.FIREBASE_CONFIG` near the top and paste the values.

## 2. Publish on GitHub Pages
1. Create a new GitHub repository (e.g. `cargo-dashboard`).
2. Upload `index.html` (and this README) to the repository root.
3. **Settings -> Pages -> Build and deployment -> Deploy from a branch -> main / (root) -> Save**.
4. After ~1 minute your site is live at `https://<your-username>.github.io/cargo-dashboard/`.

## 3. Use it
- Supervisors open the link on phone/tablet/PC and use **Shift Entry**.
- Press **T** (or the TV Mode button) on the Dashboard for the TV screen.
- Edit and Generate-report password: `GC123` (change it: see below).

## Security notes
- The Firestore rules above let anyone with the link read/write the three collections (simple, matches a shared-link workflow). For stricter control, enable Firebase Authentication and change the rules to `if request.auth != null`.
- The edit password is checked in the browser, so it is a light safeguard only. To change it, compute the SHA-256 of your new password (e.g. `printf 'NEWPASS' | sha256sum`) and replace the value of `PWH` in `index.html`.
