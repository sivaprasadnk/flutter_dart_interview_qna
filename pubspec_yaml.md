# What is pubspec.yaml file ?

In Flutter, **pubspec.yaml** is the configuration file where you define **project metadata** and **dependencies**. It's located at the **root** of your Flutter project and tells Flutter how to build your project and what packages to include.

---

## 🏷️ **Structure of `pubspec.yaml`**  
A typical `pubspec.yaml` file looks like this:

```yaml
name: my_app
description: A new Flutter project.
version: 1.0.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true
  assets:
    - assets/images/
  fonts:
    - family: Roboto
      fonts:
        - asset: assets/fonts/Roboto-Regular.ttf
```

---

## 🏷️ **Explanation of Sections**  

### ✅ **1. `name`**  
Defines the name of the project.  
- Should be **lowercase** and use **underscores** instead of spaces.  
- This is used when publishing the app to **pub.dev** or running commands.  

```yaml
name: my_app
```

---

### ✅ **2. `description`**  
Provides a short description of the app.  
- Maximum length: **180 characters**.  
- Helps others understand the purpose of the app/package.  

```yaml
description: A new Flutter project.
```

---

### ✅ **3. `version`**  
Specifies the app version.  
- Format: `major.minor.patch+buildNumber`  
- Example: `1.0.0+1`  
   - `1.0.0` → Version number  
   - `+1` → Build number  

```yaml
version: 1.0.0+1
```

> ✅ The `buildNumber` is used for app updates and store releases.  

---

### ✅ **4. `environment`**  
Defines the supported Dart SDK version.  
- This ensures compatibility with specific Dart versions.  
- Example:  
   - `>=3.0.0 <4.0.0` → Compatible with Dart 3.x, not 4.x  

```yaml
environment:
  sdk: '>=3.0.0 <4.0.0'
```

---

### ✅ **5. `dependencies`**  
Lists the packages required for the app to work.  

```yaml
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
```

- `flutter` → Core Flutter SDK  
- `cupertino_icons` → A package for Cupertino-style icons  
- `^1.0.2` → Version constraint (**caret operator**)  
   - `^1.0.2` → Use version `1.0.2` or higher, but **less than 2.0.0**  

---

### ✅ **6. `dev_dependencies`**  
Lists the packages used for **development and testing**.  
- They are not included in the final production build.  

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
```

- `flutter_test` → Used for unit testing  

---

### ✅ **7. `flutter`**  
Flutter-specific settings.  

**➔ Material Design**  
- Enables the use of Material components.  

```yaml
flutter:
  uses-material-design: true
```

---

**➔ Assets**  
Defines assets (like images, JSON files, etc.).  
- Use a trailing `/` to include all files in the folder.  
- Example:  

```yaml
flutter:
  assets:
    - assets/images/  # Loads all images from this folder
    - assets/config/config.json
```

**Accessing in code:**  
```dart
Image.asset('assets/images/logo.png');
```

---

**➔ Fonts**  
Defines custom fonts.  

```yaml
flutter:
  fonts:
    - family: Roboto
      fonts:
        - asset: assets/fonts/Roboto-Regular.ttf
        - asset: assets/fonts/Roboto-Bold.ttf
          weight: 700
```

**Accessing in code:**  
```dart
Text(
  'Hello, World!',
  style: TextStyle(fontFamily: 'Roboto', fontWeight: FontWeight.bold),
);
```

---

### ✅ **8. `platforms`**  
Defines the platforms supported by the project.  
- Default platforms: `android`, `ios`, `web`, `macos`, `windows`, `linux`  
- You can remove a platform if not needed.  

```yaml
platforms:
  android:
  ios:
  web:
```

---

## 🏷️ **Adding Dependencies**  
### 🔹 Add Dependency Using `pubspec.yaml`  
1. Open `pubspec.yaml`  
2. Add dependency under `dependencies`  
```yaml
dependencies:
  http: ^1.2.0
```

3. Run:  
```bash
flutter pub get
```

---

### 🔹 Add Dependency Using Terminal  
You can add dependencies directly using the terminal:  
```bash
flutter pub add http
```

---

### 🔹 Example (Dependency with Git)  
You can add a dependency from a Git repository:  
```yaml
dependencies:
  my_package:
    git:
      url: https://github.com/user/my_package.git
      ref: main
```

---

### 🔹 Example (Dependency from Local File)  
You can add a dependency from a local folder:  
```yaml
dependencies:
  my_package:
    path: ../my_package
```

---

## 🏷️ **Version Constraints**  
| Symbol | Meaning | Example |
|--------|---------|---------|
| `^`     | Allows minor updates but not major updates | `^1.0.0` → `1.0.1` or `1.1.0` ✅, but not `2.0.0` ❌ |
| `~`     | Allows patch updates but not minor or major updates | `~1.0.0` → `1.0.1` ✅, but not `1.1.0` ❌ |
| `>=`    | Minimum version allowed | `>=1.0.0` |
| `<=`    | Maximum version allowed | `<=2.0.0` |
| `*`     | Any version allowed | `*` |
| `-`     | Range of versions allowed | `>=1.0.0 <2.0.0` |

---

## 🏷️ **Locking Dependencies**  
When you run `flutter pub get`, it generates a `pubspec.lock` file, which:  
- Locks the dependency versions.  
- Ensures that builds are reproducible.  

> ✅ Delete `pubspec.lock` if you want to update all dependencies.  

---

## 🏷️ **Running Commands**  

| Command | Description |
|---------|-------------|
| `flutter pub get` | Fetches dependencies |
| `flutter pub upgrade` | Upgrades all dependencies to the latest versions |
| `flutter pub outdated` | Shows outdated dependencies |
| `flutter clean` | Cleans the build folder and cache |
| `flutter pub add` | Adds a new dependency |

---

## 🎯 **Best Practices**  
✔️ Always run `flutter pub get` after modifying `pubspec.yaml`.  
✔️ Use `^` for most dependencies to allow minor updates.  
✔️ Lock dependencies in `pubspec.lock` for consistent builds.  
✔️ Remove unused dependencies to reduce build size.  
✔️ Keep dependencies up to date using `flutter pub upgrade`.  

---

## 🚀 **Example (Complete `pubspec.yaml`)**  
```yaml
name: my_app
description: A Flutter project.
version: 1.0.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  http: ^1.2.0
  cupertino_icons: ^1.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true
  assets:
    - assets/images/
  fonts:
    - family: Roboto
      fonts:
        - asset: assets/fonts/Roboto-Regular.ttf
```

---

🔥 **`pubspec.yaml`** is essential for defining your app’s configuration — mastering it gives you control over your project's structure! 😎