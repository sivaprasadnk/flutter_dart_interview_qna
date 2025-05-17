# Explain Padding widget in Flutter

In Flutter, the `Padding` widget is used to insert space around a child widget. It helps in adjusting spacing inside layouts without modifying the child widget itself.

### Syntax:

```dart
Padding(
  padding: EdgeInsets.all(16.0), // or symmetric/only/fromLTRB
  child: YourWidget(),
)
```

### Common EdgeInsets options:

* `EdgeInsets.all(double value)`: Same padding on all sides.
* `EdgeInsets.symmetric({double vertical, double horizontal})`: Different vertical and horizontal padding.
* `EdgeInsets.only({left, top, right, bottom})`: Custom padding for specific sides.
* `EdgeInsets.fromLTRB(left, top, right, bottom)`: Like `.only` but positional.

### Example:

```dart
Padding(
  padding: EdgeInsets.symmetric(horizontal: 20.0, vertical: 10.0),
  child: Text('Hello Flutter!'),
)
```

This adds horizontal padding of 20 and vertical padding of 10 around the `Text` widget.
