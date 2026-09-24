# Nova
Площадка музыки
name: Build NOVA APK
name: Build NOVA APK

on:
  push:
    branches:
      - main
      - master
  workflow_dispatch:

jobs:
  build:
    name: Build NOVA
    runs-on: ubuntu-latest

    steps:
      - name: Checkout NOVA
        uses: actions/checkout@v4

      - name: Set up Java
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Set up Android SDK
        uses: android-actions/setup-android@v3

      - name: Make Gradle executable
        run: chmod +x gradlew

      - name: Build NOVA APK
        run: ./gradlew assembleDebug --stacktrace

      - name: Upload NOVA APK
        uses: actions/upload-artifact@v4
        with:
          name: NOVA-APK
          path: app/build/outputs/apk/debug/app-debug.apk
          if-no-files-found: error
          NOVA/
├── gradlew
├── gradlew.bat
├── gradle/
│   └── wrapper/
├── settings.gradle
├── build.gradle
├── app/
│   └── build.gradle
└── .github/
    └── workflows/
        └── build-apk.yml
        app-debug.apk app-debug.apk
