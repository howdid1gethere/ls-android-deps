# ls-android-deps — Android wrapper for LibreSprite (Samsung tablet fork)

This is the Android wrapper/build for the Samsung-tablet fork of **LibreSprite**. It is
cloned into `android/` inside the [LibreSprite editor fork](https://github.com/howdid1gethere/LibreSprite)
to build the APK.

➡️ **Pre-built APK and the full project README live in the editor fork:**
https://github.com/howdid1gethere/LibreSprite
(grab the APK from its [Releases](https://github.com/howdid1gethere/LibreSprite/releases) page).

Built and tested on a **Samsung Galaxy Tab S7 FE** (S Pen, Book Cover keyboard, DeX).

## What's different from upstream `ls-android-deps`

- **Samsung DeX:** removed the self-relaunch that crashed the app on maximize. It now
  opens as a large window and survives a manual maximize (manifest `<layout 100%>` +
  expanded `configChanges`).
- **S Pen palm rejection** in the touch handler — releases the synthesized touch-mouse
  button on `ACTION_CANCEL`, and requires deliberate movement before a two-finger
  gesture activates, so a resting palm no longer draws or pans/zooms.
- **Hardware-keyboard shortcuts** (Samsung Book Cover keyboard) routed to SDL via
  `MainActivity.dispatchKeyEvent`, with the on-screen keyboard suppressed when a
  hardware keyboard is connected.
- **Storage:** All-files-access prompt on launch; user files under
  `/storage/emulated/0/LibreSprite/`; "open containing folder" via Samsung My Files
  (`MainActivity.openFolder`).
- **Build:** `CMAKE_POLICY_VERSION_MINIMUM=3.5` for the bundled sub-projects, the
  swatch-file source wired into the native build, plus audio-permission and gradle-heap
  fixes.

These changes are also offered back upstream in
[ls-android-deps#2](https://github.com/LibreSprite/ls-android-deps/pull/2).

## Build

See the editor fork's [INSTALL](https://github.com/howdid1gethere/LibreSprite/blob/my-version/INSTALL.md).
In short: run the host codegen pass, then `cd android && ./gradlew assembleArm64Debug`.
The APK lands in `app/build/outputs/apk/arm64/debug/`.
