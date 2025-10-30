DriverBlackbox - Android project skeleton (Kotlin)

What this is:
- Minimal Android Studio project skeleton for a driver-side "blackbox" app.
- Includes a Foreground Service (BlackboxService) using CameraX, location updates, file encryption (Jetpack Security MasterKey), Room entities, and a WorkManager cleanup worker.
- NOT a finished product; finalization & testing required.

How to use:
1. Download / unzip the project.
2. Open in Android Studio (Electric Eel or later).
3. Let Gradle sync; update dependency versions if needed.
4. Test on a real device.
5. Build -> Generate Signed Bundle/APK.

Important:
- Respect privacy and local laws. Inform passengers if recording audio/video.
- Some devices restrict long-running background services; request user to whitelist app from battery optimization.
