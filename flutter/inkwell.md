# Explain Inkwell widget in Flutter

`InkWell` in Flutter is a widget that responds to touch gestures **with a ripple effect**, making it perfect for Material Design apps. It provides visual feedback (ink splash) when tapped, which `GestureDetector` doesn’t do by default.

---

### 🔹 Basic Usage
```dart
InkWell(
  onTap: () {
    print("Tapped InkWell");
  },
  child: Container(
    padding: EdgeInsets.all(16),
    child: Text("Tap Me"),
  ),
)
```

This will show a ripple splash effect when tapped — **but only if it's inside a Material widget**.

---

### 🔹 Must be Inside a Material
To show the ripple effect, `InkWell` needs a `Material` ancestor. If not present, you won’t see any effect.

```dart
Material(
  child: InkWell(
    onTap: () {},
    child: Padding(
      padding: EdgeInsets.all(16),
      child: Text("Tap with Ripple"),
    ),
  ),
)
```

---

### 🔹 Common Properties

| Property         | Description |
|------------------|-------------|
| `onTap`          | Called when tapped. |
| `onDoubleTap`    | Called on double tap. |
| `onLongPress`    | Called on long press. |
| `onHover`        | Called when mouse hovers (web/desktop). |
| `splashColor`    | Color of the ripple splash. |
| `highlightColor` | Color of the highlight during tap. |
| `radius`         | Radius of the splash circle. |
| `borderRadius`   | Rounds the edges of the ripple effect. |
| `customBorder`   | Custom shape for the ripple. |

---

### 🔹 Example with Rounded Splash
```dart
Material(
  color: Colors.grey[200],
  child: InkWell(
    onTap: () {},
    borderRadius: BorderRadius.circular(12),
    splashColor: Colors.blue.withOpacity(0.3),
    child: Container(
      padding: EdgeInsets.all(20),
      child: Text("Rounded Ripple"),
    ),
  ),
)
```

---

### 🔹 InkWell vs GestureDetector

| Feature             | `InkWell`        | `GestureDetector` |
|---------------------|------------------|--------------------|
| Ripple Effect        | ✅ Yes           | ❌ No               |
| Requires `Material` | ✅ Yes           | ❌ No               |
| Touch Feedback      | ✅ Yes           | ❌ No               |
| Custom Gestures     | ❌ Limited       | ✅ More Flexible    |

---

So if you're working on a Material-themed UI and want that native tap effect, go with `InkWell`. For more advanced gestures or custom effects, `GestureDetector` is your friend.
