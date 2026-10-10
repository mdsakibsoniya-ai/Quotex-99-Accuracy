# BUILD_INSTRUCTIONS

## Prerequisites
- Android Studio
- JDK 11+
- Android SDK 34
- Kotlin
- Gradle 8+

## Local Build
```bash
./gradlew assembleRelease
```

## APK Output
```bash
app/build/outputs/apk/release/app-release.apk
```

## CodeMagic Build
Use this command in CodeMagic:
```bash
./gradlew assembleRelease
```

## Install APK on Device
```bash
adb install app/build/outputs/apk/release/app-release.apk
```

## Important
- The project should be ready for Android app build without extra setup
- Must be built as release APK
- Accessibility Service must be enabled manually on device
- User must grant SYSTEM_ALERT_WINDOW permission

## Notes
- This repository only contains the specification set and instructions
- The 96 pattern screenshots will be provided separately as a ZIP file
- The implementation must use the exact rules described in the specification
