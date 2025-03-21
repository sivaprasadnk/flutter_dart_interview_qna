# 🚀 **CI/CD in Flutter**  

**CI/CD** stands for **Continuous Integration** and **Continuous Deployment/Delivery**. It automates the process of building, testing, and deploying Flutter apps, ensuring a faster and more reliable development cycle.

---

## 🏆 **Why CI/CD for Flutter?**  
✅ Automates building and testing  
✅ Ensures code quality and consistency  
✅ Reduces deployment errors  
✅ Provides fast feedback  
✅ Speeds up delivery to the app stores  

---

## 🎯 **Key Components of CI/CD**  
1. **Continuous Integration (CI):**  
   - Automatically builds and tests the app whenever new code is pushed to the repository.  
   - Ensures that changes do not break existing functionality.  

2. **Continuous Delivery (CD):**  
   - Deploys the app to staging or production environments automatically after successful testing.  

3. **Continuous Deployment:**  
   - Automates the deployment to production without manual intervention.  

---

## 🏗️ **CI/CD Flow for Flutter**  
### ✅ 1. **Code Commit:**  
Developer pushes code changes to a version control system like **GitHub**, **GitLab**, or **Bitbucket**.

### ✅ 2. **CI Process:**  
- Linting  
- Build creation  
- Unit testing  
- Integration testing  

### ✅ 3. **CD Process:**  
- Create signed builds (Android: `.apk` / `.aab`, iOS: `.ipa`)  
- Deploy to TestFlight (iOS) or Firebase App Distribution (Android)  
- Upload to Play Store / App Store  

---

## 🌟 **Popular CI/CD Tools for Flutter**
| Tool | Platform | Free Tier | Notes |
|------|----------|-----------|-------|
| **GitHub Actions** | Cross-platform | ✅ Free for public repos | Native integration with GitHub |
| **Bitrise** | Cross-platform | ✅ Free for small teams | Special Flutter support |
| **Codemagic** | Cross-platform | ✅ Free for open-source | Flutter-focused |
| **CircleCI** | Cross-platform | ✅ Free tier available | Flexible setup |
| **GitLab CI/CD** | Cross-platform | ✅ Free for small teams | Self-hosted option available |
| **Jenkins** | Cross-platform | ✅ Open-source | Highly configurable |

---

## 🛠️ **1. GitHub Actions for Flutter**
### ✅ **Setup GitHub Actions for Flutter:**
1. Create `.github/workflows/flutter.yml` in the project root.

2. Add the following YAML configuration:
```yaml
name: Flutter CI/CD

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Flutter
        uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.x.x'

      - name: Install dependencies
        run: flutter pub get

      - name: Analyze code
        run: flutter analyze

      - name: Run tests
        run: flutter test

      - name: Build APK
        run: flutter build apk --release
```

### ✅ **Explanation:**
- `on` – Triggers the workflow on a push or pull request to the `main` branch.  
- `checkout` – Clones the repository.  
- `flutter-action` – Sets up Flutter environment.  
- `flutter pub get` – Installs dependencies.  
- `flutter analyze` – Runs static analysis for linting.  
- `flutter test` – Runs unit tests.  
- `flutter build apk` – Builds the release APK.  

---

## 🛠️ **2. Bitrise for Flutter**
### ✅ **Setup Bitrise:**
1. Sign up at [https://www.bitrise.io](https://www.bitrise.io).  
2. Connect your GitHub repository.  
3. Select **Flutter** as the project type.  
4. Add build steps:  
   - **Flutter Analyze**  
   - **Flutter Test**  
   - **Flutter Build**  

### ✅ **Example Bitrise Configuration:**
- Build `.apk`:
```yaml
workflows:
  primary:
    steps:
      - flutter-analyze
      - flutter-test
      - flutter-build@0:
          inputs:
            - platform: "android"
            - build_type: "apk"
```

---

## 🛠️ **3. Codemagic for Flutter**
### ✅ **Setup Codemagic:**
1. Sign up at [https://codemagic.io](https://codemagic.io).  
2. Connect your GitHub repository.  
3. Create a `codemagic.yaml` file:  

### ✅ **Example `codemagic.yaml` Configuration:**
```yaml
workflows:
  flutter-app:
    name: Flutter App Build
    instance_type: mac_mini_m1
    triggering:
      events:
        - push
        - tag
    environment:
      flutter: stable
    scripts:
      - name: Get dependencies
        script: |
          flutter pub get
      - name: Analyze project
        script: |
          flutter analyze
      - name: Run tests
        script: |
          flutter test
      - name: Build APK
        script: |
          flutter build apk --release
    artifacts:
      - build/**/outputs/**/*.apk
```

---

## 🛠️ **4. GitLab CI/CD for Flutter**
### ✅ **Example `.gitlab-ci.yml` Configuration:**
```yaml
stages:
  - build
  - test

flutter_setup:
  stage: build
  script:
    - git clone https://github.com/flutter/flutter.git -b stable --depth 1
    - export PATH="$PATH:`pwd`/flutter/bin"
    - flutter pub get
    - flutter build apk --release

flutter_test:
  stage: test
  script:
    - flutter test
```

---

## 🚀 **Code Signing in CI/CD**  
### ✅ **Android:**
1. Create a `key.properties` file:
```properties
storePassword=<password>
keyPassword=<password>
keyAlias=<alias>
storeFile=<path-to-keystore>
```

2. Add to `build.gradle`:
```gradle
signingConfigs {
    release {
        storeFile file("key.jks")
        storePassword System.getenv("STORE_PASSWORD")
        keyAlias System.getenv("KEY_ALIAS")
        keyPassword System.getenv("KEY_PASSWORD")
    }
}

buildTypes {
    release {
        signingConfig signingConfigs.release
    }
}
```

3. Add to CI/CD Secrets:
- `STORE_PASSWORD`  
- `KEY_ALIAS`  
- `KEY_PASSWORD`  

---

### ✅ **iOS:**
1. Generate a `.p12` file using Xcode.  
2. Add the `.p12` file and the provisioning profile to the CI/CD environment.  
3. Add keychain setup in the CI/CD config:
```bash
security create-keychain -p "" build.keychain
security import Certificate.p12 -k build.keychain -P "$CERT_PASSWORD" -T /usr/bin/codesign
security list-keychains -s build.keychain
security default-keychain -s build.keychain
```

---

## 🎯 **Release to Play Store and App Store**
### ✅ **Firebase App Distribution:**
```bash
firebase appdistribution:distribute build/app/outputs/flutter-apk/app-release.apk --app <app-id>
```

### ✅ **Google Play:**
Use `fastlane`:
```bash
fastlane supply --track production --json_key_path "key.json"
```

### ✅ **Apple Store:**
Use `fastlane`:
```bash
fastlane deliver
```

---

## 🌟 **Best Practices for CI/CD**
✅ Always automate testing and linting  
✅ Secure your signing keys and secrets  
✅ Use environment variables for sensitive data  
✅ Monitor builds for failures and fix promptly  
✅ Keep build times short by using caching  

---

## 🏆 **Summary**  
✔️ **CI/CD** automates building, testing, and deploying Flutter apps.  
✔️ Use **GitHub Actions**, **Bitrise**, or **Codemagic** for easy setup.  
✔️ Secure signing keys and environment variables.  
✔️ Monitor and improve pipeline performance over time. 😎