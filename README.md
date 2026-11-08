# Adam's Armory – Android build

Offline ballistic calculator, ammo log and inventory. All data is encrypted on the device (AES-256-GCM, key from your password via PBKDF2-SHA256, 310,000 iterations). The app has **no internet permission**.

`www/index.html` is the whole app. Open it in any desktop browser (Chrome, Edge or Firefox) to test it.

## Option A – Cloud build, then download on your phone (recommended)
1. Sign in at github.com (free account) → **+ ▸ New repository** → name it `adams-armory`, set it to **Private** → Create.
2. On the new repo page, click **uploading an existing file**. Drag in **everything** from this folder (unzipped) except `node_modules`, then click **Commit changes**.
   - The hidden `.github` folder is sometimes skipped. If the **Actions** tab shows no workflow, choose **Actions ▸ set up a workflow yourself**, paste in the contents of `.github/workflows/build-apk.yml`, and commit.
3. Open the **Actions** tab and wait about 5–8 minutes for the green check.
4. **On your phone**, open `github.com/<you>/adams-armory/releases/latest` (you need to be signed in, because the repo is private) → tap **AdamsArmory.apk**.
5. Open the downloaded file. When Android asks, allow your browser to **Install unknown apps**, then tap **Install**.
   - Google Play Protect may warn about an "unrecognized app" because it is not from the Play Store. Tap **More details ▸ Install anyway**.

Every later upload or commit builds a new APK, which installs over the old one. Your data stays, because every build is signed with the same key (`android/debug.keystore`).

## Option B – Build locally with Android Studio
1. Install Node.js 22 and Android Studio.
2. In this folder, run `npm install`, then `npx cap sync android`.
3. Run `npx cap open android`, then in Android Studio choose **Build ▸ Build APK(s)**.

## Updating the app
Replace `www/index.html` with the new version, then rebuild. Your data stays on the phone as long as the app ID (`ca.adamhoward.armory`) stays the same and the new APK is signed with the same key. Debug builds from the same machine or workflow use the same debug key. **Export an encrypted backup from Settings before you update.**
