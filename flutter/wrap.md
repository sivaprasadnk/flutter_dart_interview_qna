# Explain Wrap widget in Flutter

In Flutter, the **`Wrap`** widget is a layout widget that **displays its children in a horizontal or vertical flow** and **automatically wraps them** into the next line (or column) when there isn't enough space.

Think of it like **text wrapping** in a paragraph — when a word doesn't fit at the end of a line, it moves to the next line.  
Similarly, `Wrap` moves the widgets into the next row or column if space runs out.

---

### Basic Syntax:
```dart
Wrap(
  direction: Axis.horizontal, // or Axis.vertical
  spacing: 8.0,                // horizontal space between children
  runSpacing: 4.0,             // vertical space between lines
  children: [
    Chip(label: Text('Flutter')),
    Chip(label: Text('Dart')),
    Chip(label: Text('Widgets')),
    Chip(label: Text('Wrap')),
  ],
)
```

---

### Key Properties:
| Property        | Description                                                |
|-----------------|------------------------------------------------------------|
| `direction`      | The main axis direction (horizontal by default).           |
| `spacing`        | Horizontal gap between children.                          |
| `runSpacing`     | Vertical gap between the lines (or runs).                  |
| `alignment`      | How the children are aligned on the main axis.             |
| `runAlignment`   | How the lines themselves are aligned on the cross axis.    |
| `crossAxisAlignment` | Alignment of children within a line.                  |
| `textDirection`  | Text direction (LTR/RTL). Useful for internationalization. |
| `verticalDirection` | Determines the order of wrapping vertically (up/down). |

---

### When to Use `Wrap`:
- When you have **dynamic content** (e.g., a list of tags, categories, buttons) that might **overflow** if you use a `Row` or `Column`.
- Instead of getting an **overflow error**, `Wrap` arranges them nicely.

**Example:**  
If you used a `Row` instead of `Wrap` and the screen wasn't wide enough, you'd get an error like:

> **Bottom Overflowed by pixels**

But `Wrap` avoids that by moving widgets into a new line automatically.

---

### Quick Visual Example:
Suppose you have 5 buttons.  
- In a `Row`, they might overflow if they can't all fit horizontally.
- In a `Wrap`, the extra buttons move to the next line automatically!

---
