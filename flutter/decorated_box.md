# Explain DecoratedBox widget in Flutter

In Flutter, a `DecoratedBox` is a widget that paints a decoration (like background color, border, gradient, etc.) **behind** its child.

### Basic Usage:

```dart
DecoratedBox(
  decoration: BoxDecoration(
    color: Colors.blue, // Background color
    border: Border.all(color: Colors.black, width: 2), // Border
    borderRadius: BorderRadius.circular(12), // Rounded corners
    boxShadow: [
      BoxShadow(
        color: Colors.black26,
        offset: Offset(2, 2),
        blurRadius: 5,
      ),
    ],
  ),
  child: Padding(
    padding: EdgeInsets.all(16.0),
    child: Text(
      'Hello, Flutter!',
      style: TextStyle(color: Colors.white),
    ),
  ),
)
```

### Notes:
- `DecoratedBox` does **not** provide padding/margin itself—you have to use `Padding` or `Container` for that.
- If you want a simpler alternative, you can use `Container` which combines `DecoratedBox` and other features like padding, margin, alignment.
