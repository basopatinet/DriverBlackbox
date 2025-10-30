# Release Build Instructions (GitHub Actions)

This repository already contains an Android project and two GitHub Actions workflows:
- `.github/workflows/android.yml` — builds a **debug** APK and uploads it as an artifact.
- `.github/workflows/android-release.yml` — (new) builds a **release** APK. It can produce a **signed** release APK when you add signing secrets.

## How to produce a signed release APK automatically

1. Generate a keystore locally (or use your existing `.jks`):

```bash
keytool -genkeypair -v -keystore release.keystore -alias mykeyalias -keyalg RSA -keysize 2048 -validity 10000
```

When prompted, record the keystore password and key alias/password.

2. Encode the keystore to base64 and add it to GitHub Secrets:

```bash
base64 -w 0 release.keystore > release.keystore.base64
# copy the output file content and set it as the GitHub secret SIGNING_KEY
```

Set the following repository secrets (Settings -> Secrets -> Actions):
- `SIGNING_KEY` — base64 content of your `.jks` file
- `KEY_ALIAS` — the alias used when creating the key (e.g. `mykeyalias`)
- `KEY_PASSWORD` — password for the key
- `STORE_PASSWORD` — password for the keystore

3. Push this repository to GitHub (to `main` or `master`) and trigger the workflow:
- Go to Actions → select "Android CI - Build Signed Release APK" → Run workflow
- Or push a commit to `main`/`master` to trigger automatically.

4. After the workflow finishes, download the artifact `DriverBlackbox-release-apk` from the workflow run.

## If you prefer to build locally

1. Open the project folder in Android Studio.
2. Build → Generate Signed Bundle / APK → follow the dialog, provide your keystore and passwords.

## Notes
- For production release on Google Play, use proper versionCode/versionName and enable ProGuard/R8 if required.
- Keep your keystore and passwords secure. Do not commit the keystore or passwords to the repository.
