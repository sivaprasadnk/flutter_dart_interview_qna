# Explain LayoutBuilder in Flutter

`LayoutBuilder` in Flutter is a powerful widget that helps you build responsive UIs by giving you access to the **constraints** of its parent widget. This allows you to create different layouts depending on the available width and height.

---

### 📦 Constructor:

```dart
LayoutBuilder({
  required Widget Function(BuildContext, BoxConstraints) builder,
})
```

---

### 🧠 How it works:

* `LayoutBuilder` takes a `builder` function with:

  * `BuildContext context`
  * `BoxConstraints constraints`

This lets you dynamically build child widgets based on the **constraints** passed by the parent (e.g., screen size, available space).

---

### ✅ Use Cases:

* Creating **responsive UIs** (e.g., different layouts for mobile vs. tablet)
* Conditionally displaying widgets based on available **width/height**
* Building custom widgets that adapt to space

---

### 📱 Example:

```dart
LayoutBuilder(
  builder: (context, constraints) {
    if (constraints.maxWidth > 600) {
      return Row(
        children: [
          Expanded(child: Sidebar()),
          Expanded(flex: 3, child: Content()),
        ],
      );
    } else {
      return Column(
        children: [
          Content(),
          BottomNav(),
        ],
      );
    }
  },
)
```

In this example:

* For wide screens (like tablets), it shows a `Row` with sidebar + content.
* For narrow screens (like phones), it shows a `Column`.

---

### 📌 Notes:

* `LayoutBuilder` is different from `MediaQuery`:

  * `MediaQuery` provides **screen dimensions**.
  * `LayoutBuilder` provides **widget constraints** (more precise in nested layouts).
* Use it **only when needed**, as it rebuilds every time the layout constraints change.

---
