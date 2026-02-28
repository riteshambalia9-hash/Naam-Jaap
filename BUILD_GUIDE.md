# 📱 नाम जाप — Android APK Build Guide

## Method 1: Android Studio (Easiest — Free)

### Step 1: Install Android Studio
Download from: https://developer.android.com/studio
Install with default settings (includes Android SDK automatically)

### Step 2: Open Project
1. Unzip `NaamJaap-AndroidProject.zip`
2. Open Android Studio
3. Click **"Open"** → select the `NaamJaap` folder
4. Wait for Gradle sync to complete (~2-3 minutes first time)

### Step 3: Build APK
- Menu → **Build → Build Bundle(s) / APK(s) → Build APK(s)**
- Wait ~1-2 minutes
- Click **"locate"** in the notification → APK is in:
  `app/build/outputs/apk/debug/app-debug.apk`

### Step 4: Install on Phone
- Connect phone via USB (enable USB debugging)
- Click ▶ **Run** button in Android Studio, OR
- Copy `app-debug.apk` to phone and install manually
  (Settings → Security → Unknown Sources → ON)

---

## Method 2: Online Builder (No PC needed)

### Using Appetize / Buildozer online:
1. Go to https://appetize.io or https://buildozer.io
2. Upload the `NaamJaap` project zip
3. Download the APK

### Using GitHub Actions (Free automated build):
1. Create a free GitHub account
2. Upload this project as a new repository
3. Add `.github/workflows/build.yml` (see below)
4. GitHub will automatically build the APK

```yaml
# .github/workflows/build.yml
name: Build APK
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with: { java-version: '17', distribution: 'temurin' }
      - run: chmod +x gradlew
      - run: ./gradlew assembleDebug
      - uses: actions/upload-artifact@v3
        with:
          name: NaamJaap-APK
          path: app/build/outputs/apk/debug/app-debug.apk
```

---

## App Features
✅ Fullscreen immersive (no status bar, no navigation bar)
✅ Screen stays ON during jaap (FLAG_KEEP_SCREEN_ON)
✅ Audio autoplay enabled
✅ localStorage works (drag positions saved)
✅ Portrait orientation locked
✅ Works offline (HTML bundled inside app)
✅ Min Android: 5.0 (API 21) — supports 98% of devices

## Package Info
- Package: com.naamjaap.app
- App Name: नाम जाप
- Min SDK: 21 (Android 5.0)
- Target SDK: 34 (Android 14)
