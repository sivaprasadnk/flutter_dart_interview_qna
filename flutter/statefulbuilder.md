# Explain Statefulbuilder in Flutter

`StatefulBuilder` in Flutter is a widget that allows you to rebuild only a portion of the widget tree **without needing to convert the whole widget to a StatefulWidget**. It's especially useful in places like `showDialog`, `showModalBottomSheet`, or any other context where you need to update part of the UI based on user interaction but don’t want to or can’t manage a full `StatefulWidget`.

---

### 🔧 Syntax

```dart
StatefulBuilder(
  builder: (BuildContext context, StateSetter setState) {
    return // your UI here
  },
)
```

---

### ✅ Use Case Example — Inside a Dialog

```dart
showDialog(
  context: context,
  builder: (context) {
    int counter = 0;

    return AlertDialog(
      title: Text("Counter Dialog"),
      content: StatefulBuilder(
        builder: (context, setState) {
          return Column(
            mainAxisSize: MainAxisSize.min,
            children: [
              Text("Counter: $counter"),
              ElevatedButton(
                onPressed: () {
                  setState(() {
                    counter++;
                  });
                },
                child: Text("Increment"),
              ),
            ],
          );
        },
      ),
    );
  },
);
```

---

### ⚙️ How It Works

* `StatefulBuilder` provides a local `setState()` method (from `StateSetter`) that can rebuild just the widget inside its `builder`.
* It **does not** rebuild the parent widget or dialog—just the part inside `StatefulBuilder`.

---

### ✅ When to Use It

* You need minimal state management for small UI updates.
* You're working inside a `StatelessWidget` or a method like `showDialog`.
* You want to avoid creating a separate StatefulWidget just for local state changes.

---
