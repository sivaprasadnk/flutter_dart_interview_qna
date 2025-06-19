# Explain ImageWidget in Flutter

The `Image` widget in Flutter is used to display images in your app. It’s one of the most commonly used widgets and supports loading images from various sources like assets, network, file system, or memory.

---

### 🔹 Basic Syntax

```dart
Image.asset('assets/images/logo.png')
Image.network('https://example.com/image.png')
Image.file(File('path/to/image.png'))
Image.memory(bytes)
```

---

### 🔹 Common Constructors

| Constructor     | Description                              |
| --------------- | ---------------------------------------- |
| `Image.asset`   | Loads image from your app’s local assets |
| `Image.network` | Loads image from a URL                   |
| `Image.file`    | Loads image from a file on the device    |
| `Image.memory`  | Loads image from raw bytes               |

---

### 🔹 Important Properties

| Property                   | Description                                                                                          |
| -------------------------- | ---------------------------------------------------------------------------------------------------- |
| `width` / `height`         | Set image dimensions                                                                                 |
| `fit`                      | Controls how the image should be resized to fit its box. E.g. `BoxFit.cover`, `BoxFit.contain`, etc. |
| `alignment`                | Aligns the image within its container                                                                |
| `repeat`                   | Repeats the image (if needed)                                                                        |
| `color` / `colorBlendMode` | Applies color overlay with blend mode                                                                |
| `loadingBuilder`           | Customize loading UI for `Image.network`                                                             |
| `errorBuilder`             | Handle and show widget if image fails to load                                                        |

---

### 🔹 Example Usage

```dart
Image.asset(
  'assets/images/logo.png',
  width: 100,
  height: 100,
  fit: BoxFit.cover,
)
```

```dart
Image.network(
  'https://example.com/image.png',
  loadingBuilder: (context, child, loadingProgress) {
    if (loadingProgress == null) return child;
    return CircularProgressIndicator();
  },
  errorBuilder: (context, error, stackTrace) {
    return Icon(Icons.error);
  },
)
```

---

### 🔹 Asset Image Setup

To use `Image.asset`, make sure you declare your image in `pubspec.yaml`:

```yaml
flutter:
  assets:
    - assets/images/logo.png
```

Or for a folder:

```yaml
flutter:
  assets:
    - assets/images/
```
