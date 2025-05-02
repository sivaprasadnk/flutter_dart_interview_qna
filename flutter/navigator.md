# Explain Navigator in Flutter

In Flutter, the `Navigator` is a widget that manages a stack of route objects and allows navigation between different pages (or **screens/views**) in your app.

---

### 🧭 **What is Navigator?**

Think of `Navigator` as a **stack** (like a pile of plates):

* You **push** a new route (screen) onto the stack to go forward.
* You **pop** the top route off the stack to go back.

Flutter uses `Navigator` to transition between pages in an app.

---

### ✅ **Key Methods of Navigator**

| Method                                                       | Description                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `Navigator.push(context, route)`                             | Pushes a new screen onto the stack.                                      |
| `Navigator.pop(context)`                                     | Pops the current screen off the stack and goes back.                     |
| `Navigator.pushReplacement(context, route)`                  | Replaces the current screen with a new one.                              |
| `Navigator.pushAndRemoveUntil(context, newRoute, predicate)` | Pushes a new route and removes all previous routes based on a condition. |
| `Navigator.popUntil(context, predicate)`                     | Pops routes until the condition is true.                                 |

---

### 🔧 **Example: Basic Push and Pop**

```dart
// Navigate to SecondPage
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SecondPage()),
);

// Go back to previous screen
Navigator.pop(context);
```

---

### 🧱 **Navigator 1.0 vs Navigator 2.0**

* **Navigator 1.0** (most commonly used): Uses imperative-style navigation (`push`, `pop`).
* **Navigator 2.0**: Declarative, gives more control over the navigation stack (used for complex apps like web apps with browser URL sync).

---

### 📌 Common Use Case in Scaffold

Usually placed inside `MaterialApp`:

```dart
MaterialApp(
  home: FirstPage(),
);
```

---
