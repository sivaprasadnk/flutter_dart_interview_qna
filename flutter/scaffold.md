# Explain Scaffold widget in Flutter

The `Scaffold` widget in Flutter is a fundamental part of creating a visual layout for material design apps. It provides a high-level structure for your screen, making it easier to implement common UI elements like app bars, drawers, snack bars, floating action buttons, and bottom navigation bars.

---

### 🧱 Basic Structure

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Scaffold Example'),
      ),
      body: Center(
        child: Text('Hello, Scaffold!'),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          // Action goes here
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

---

### ✨ Common Properties

| Property                | Description |
|------------------------|-------------|
| `appBar`               | Top bar typically used for titles, actions, etc. |
| `body`                 | The main content of the screen. |
| `floatingActionButton`| A button that floats above the content. |
| `drawer`               | A side navigation menu. |
| `bottomNavigationBar` | A bar at the bottom for navigation. |
| `bottomSheet`          | Persistent or modal content at the bottom. |
| `backgroundColor`      | Sets the background color of the scaffold. |
| `resizeToAvoidBottomInset` | Avoids keyboard overlapping content when set to true. |

---

### 📝 Example with More Widgets

```dart
Scaffold(
  appBar: AppBar(title: Text("My App")),
  drawer: Drawer(
    child: ListView(
      children: [
        DrawerHeader(child: Text("Header")),
        ListTile(title: Text("Item 1")),
        ListTile(title: Text("Item 2")),
      ],
    ),
  ),
  body: Center(child: Text("Main Content")),
  floatingActionButton: FloatingActionButton(
    onPressed: () {},
    child: Icon(Icons.add),
  ),
  bottomNavigationBar: BottomNavigationBar(
    items: [
      BottomNavigationBarItem(icon: Icon(Icons.home), label: "Home"),
      BottomNavigationBarItem(icon: Icon(Icons.settings), label: "Settings"),
    ],
  ),
)
```
