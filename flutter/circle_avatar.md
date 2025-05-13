# Explain CircleAvatar in Flutter

`CircleAvatar` is a widget in Flutter used to display a **circular image or icon**, commonly for **user profile pictures**.

---

### 📌 Syntax

```dart
CircleAvatar({
  Key? key,
  Widget? child,
  Color? backgroundColor,
  Color? foregroundColor,
  double? radius,
  double? minRadius,
  double? maxRadius,
  ImageProvider? backgroundImage,
  Color? backgroundImageError,
})
```

---

### ✅ Common Use Cases

* Profile pictures
* User initials in a circle
* Rounded icons

---

### 📘 Example 1: Simple CircleAvatar with initials

```dart
CircleAvatar(
  child: Text('SP'),
)
```

> Displays a circle with the text "SP" centered.

---

### 📘 Example 2: CircleAvatar with an image

```dart
CircleAvatar(
  backgroundImage: NetworkImage('https://example.com/user.jpg'),
  radius: 30,
)
```

> Displays a 60x60 circular image fetched from the internet.

---

### 📘 Example 3: CircleAvatar with background color and icon

```dart
CircleAvatar(
  backgroundColor: Colors.blue,
  child: Icon(Icons.person, color: Colors.white),
)
```

> Circle with a white person icon on a blue background.

---

### 🎯 Tips

* Use `radius` to control the size.
* Use `backgroundImage` for images from `AssetImage`, `NetworkImage`, or `FileImage`.
* You can also place a widget (like an icon or text) inside using the `child`.

---
