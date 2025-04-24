# Explain Snackbar in Flutter

A **Snackbar** is a lightweight message displayed at the bottom of the screen to briefly inform users of an event or action. It’s commonly used to give feedback like:

- "Message sent"
- "Item deleted"
- "No Internet Connection"

It can also have an optional **action**, like “UNDO.”

---

## 🧱 Basic Syntax

```dart
ScaffoldMessenger.of(context).showSnackBar(
  SnackBar(
    content: Text('Hello, Snackbar!'),
  ),
);
```

### ✅ Explanation:

- `ScaffoldMessenger.of(context)`: Shows the snackbar using the current scaffold context.
- `SnackBar()`: The widget that defines the content and behavior of the snackbar.
- `content`: The main message, typically a `Text`.

---

## ✨ Full Example

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: SnackbarDemo(),
    );
  }
}

class SnackbarDemo extends StatelessWidget {
  void _showSnackbar(BuildContext context) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(
        content: Text('This is a Snackbar'),
        duration: Duration(seconds: 3),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Snackbar Demo')),
      body: Center(
        child: ElevatedButton(
          onPressed: () => _showSnackbar(context),
          child: Text('Show Snackbar'),
        ),
      ),
    );
  }
}
```

---

## 🧩 Snackbar with Action

```dart
ScaffoldMessenger.of(context).showSnackBar(
  SnackBar(
    content: Text('Item deleted'),
    action: SnackBarAction(
      label: 'UNDO',
      onPressed: () {
        // Undo logic here
      },
    ),
  ),
);
```

- `SnackBarAction`: A built-in widget to add a button inside the snackbar.

---

## 🎨 Customizing Snackbar

You can customize the snackbar’s appearance:

```dart
SnackBar(
  content: Text('Custom Snackbar'),
  backgroundColor: Colors.green,
  behavior: SnackBarBehavior.floating,
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(10),
  ),
  margin: EdgeInsets.all(16),
  duration: Duration(seconds: 2),
);
```

### 🛠 Properties Explained:

| Property                | Description |
|------------------------|-------------|
| `backgroundColor`      | Changes the snackbar’s color. |
| `behavior`             | Set to `floating` to float above UI instead of attached to bottom. |
| `shape`                | Customize corners and border. |
| `margin`               | Set space around the snackbar (useful with floating). |
| `duration`             | Controls how long it's visible. |

---

## 🚫 Avoiding Multiple Snackbars

Before showing a new one, dismiss the old:

```dart
ScaffoldMessenger.of(context)
  ..hideCurrentSnackBar()
  ..showSnackBar(SnackBar(content: Text('New Snackbar')));
```

---

## ✅ Helper Method for Reuse

You can write a utility method to avoid code repetition:

```dart
void showSnackbar(BuildContext context, String message, {Color? color}) {
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(
      content: Text(message),
      backgroundColor: color ?? Colors.blue,
    ),
  );
}
```

Usage:

```dart
showSnackbar(context, 'Login Successful', color: Colors.green);
```

---

## ⚠️ Common Mistakes

| Mistake | Fix |
|--------|-----|
| Using `Scaffold.of(context)` | Use `ScaffoldMessenger.of(context)` (recommended after Flutter 2.0) |
| Not checking context validity | Make sure you're using the right context (not from a disposed widget) |

---
