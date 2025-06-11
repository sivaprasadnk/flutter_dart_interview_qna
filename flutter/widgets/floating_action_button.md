# Explain FloatingActionButton in Flutter

In Flutter, the `FloatingActionButton` (FAB) is a circular button typically used for a **primary action** on a screen. It "floats" above the main UI and is most commonly placed in the **bottom-right corner** of the screen in a `Scaffold`.

---

### ✅ Basic Syntax:
```dart
FloatingActionButton(
  onPressed: () {
    // Define the action here
  },
  child: Icon(Icons.add), // or any widget like Text, Image, etc.
)
```

---

### ✅ Common Usage:
You usually place it inside a `Scaffold` like this:
```dart
Scaffold(
  appBar: AppBar(title: Text('FAB Example')),
  body: Center(child: Text('Hello, World!')),
  floatingActionButton: FloatingActionButton(
    onPressed: () {
      // Action to perform when FAB is pressed
    },
    child: Icon(Icons.add),
    backgroundColor: Colors.blue,
    tooltip: 'Add',
  ),
);
```

---

### 🔧 Key Properties:

| Property         | Description                                                |
|------------------|------------------------------------------------------------|
| `onPressed`      | Required. Callback when the FAB is tapped.                 |
| `child`          | Typically an `Icon` or `Text`.                             |
| `tooltip`        | Text shown on long press for accessibility.                |
| `backgroundColor`| Sets the background color of the button.                   |
| `foregroundColor`| Sets the color of the child (icon/text).                   |
| `heroTag`        | Used for hero animations. Must be unique if multiple FABs. |
| `shape`          | Custom shape (e.g., RoundedRectangleBorder).               |
| `elevation`      | Shadow elevation.                                          |
| `mini`           | If `true`, creates a smaller version of the FAB.           |

---

### 🔄 Variants:
- `FloatingActionButton.extended`: Used when you want a **text label with an icon**.

```dart
FloatingActionButton.extended(
  onPressed: () {},
  icon: Icon(Icons.navigation),
  label: Text("Navigate"),
)
```

---
