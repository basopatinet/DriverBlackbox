# Permissions & Media Saving (Driver Blackbox)

Driver Blackbox v1.0.0 requires runtime permissions for:
- CAMERA (for video capture)
- RECORD_AUDIO (for voice recording)
- ACCESS_FINE_LOCATION / ACCESS_COARSE_LOCATION (for GPS)
- FOREGROUND_SERVICE (to run background recording)
- READ/WRITE_EXTERNAL_STORAGE (to save media to gallery on older Android versions)

Behavior:
- Recordings (video/audio) are saved to the device **Gallery** so they are easy to find.
- On Android 10+ the app uses MediaStore APIs to insert media into the gallery.
- The app must request runtime permissions at first-run. Please grant all requested permissions for full functionality.

CI / Signing:
- To produce a signed APK via GitHub Actions, set secrets:
  - SIGNING_KEY (base64 of release.keystore)
  - KEY_ALIAS
  - KEY_PASSWORD
  - STORE_PASSWORD
