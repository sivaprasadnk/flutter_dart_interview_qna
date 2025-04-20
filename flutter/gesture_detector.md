# Explain Gesture Detector in Flutter

In Flutter, the `GestureDetector` widget is used to detect gestures made by the user on the screen — like taps, swipes, long presses, double taps, and more. It's a non-visual widget, meaning it doesn’t render anything on its own, but you can wrap it around any widget to make that widget respond to gestures.

---

### 🔹 Basic Structure:
```dart
GestureDetector(
  onTap: () {
    print("Tapped!");
  },
  child: Container(
    color: Colors.blue,
    padding: EdgeInsets.all(16),
    child: Text("Tap me"),
  ),
)
```

---

### 🔹 Common Gesture Callbacks:

| Callback             | Triggered When…                             |
|----------------------|---------------------------------------------|
| `onTap`              | The user taps the widget.                   |
| `onDoubleTap`        | The user double-taps the widget.            |
| `onLongPress`        | The user long-presses the widget.           |
| `onTapDown`          | A pointer that might cause a tap has touched down. |
| `onTapUp`            | A pointer that will trigger a tap has stopped contacting the screen. |
| `onTapCancel`        | The pointer that previously triggered `onTapDown` will not end up causing a tap. |
| `onHorizontalDragStart` / `Update` / `End` | For horizontal dragging gestures. |
| `onVerticalDragStart` / `Update` / `End`   | For vertical dragging gestures. |

---

### 🔹 Example with Multiple Gestures:
```dart
GestureDetector(
  onTap: () => print("Single tap"),
  onDoubleTap: () => print("Double tap"),
  onLongPress: () => print("Long press"),
  onHorizontalDragUpdate: (details) {
    print("Dragging horizontally: ${details.delta.dx}");
  },
  child: Container(
    height: 100,
    width: 100,
    color: Colors.orange,
    child: Center(child: Text("Try gestures")),
  ),
)
```

---

### 🔹 Important Notes:
- `GestureDetector` only detects gestures on non-transparent areas (unless the `behavior` property is set to `HitTestBehavior.translucent`).
- You can wrap anything with `GestureDetector` — even a `Text`, `Image`, or a custom widget.

---

### 🔹 Alternatives:
- **`InkWell`** / **`InkResponse`**: If you want gesture detection with a material ripple effect (commonly used inside Material apps).
- `RawGestureDetector`: More advanced, allows custom gesture recognizers.

---
