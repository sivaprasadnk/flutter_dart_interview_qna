# What are the layout widgets in Flutter?

In Flutter, **layout widgets** are used to position, align, and size other widgets on the screen. They are essential for building responsive UIs. Here's a breakdown of some common layout widgets in Flutter:

---

### 📦 **Single-child Layout Widgets**
These can have only one child.

| Widget        | Description |
|---------------|-------------|
| **`Container`** | A box model with padding, margin, border, color, etc. |
| **`Padding`**   | Adds padding around a child. |
| **`Align`**     | Aligns child within itself using `Alignment`. |
| **`Center`**    | Centers its child in the available space. |
| **`SizedBox`**  | Sets fixed width/height or adds space between widgets. |
| **`Expanded`**  | Expands to fill available space in a `Row`/`Column`. |
| **`Flexible`**  | Like `Expanded` but with more control over fit. |
| **`AspectRatio`** | Forces a child's aspect ratio (e.g., 16:9). |
| **`ConstrainedBox`** | Applies additional constraints on its child. |
| **`FittedBox`** | Scales and positions its child within itself. |

---

### 🧱 **Multi-child Layout Widgets**
These accept multiple children.

| Widget        | Description |
|---------------|-------------|
| **`Column`**   | Arranges children vertically. |
| **`Row`**      | Arranges children horizontally. |
| **`Stack`**    | Overlaps widgets on top of each other (like Z-axis). |
| **`Wrap`**     | Wraps children into multiple rows or columns. |
| **`ListView`** | Scrollable list of widgets vertically or horizontally. |
| **`GridView`** | Displays children in a 2D grid format. |
| **`Table`**    | Displays data in a table layout (rows & columns). |
| **`CustomScrollView`** | Combines different scrollable widgets like Slivers. |

---

### 🧰 **Other Useful Layout Widgets**

| Widget            | Description |
|-------------------|-------------|
| **`Spacer`**        | Creates adjustable empty space in Row/Column. |
| **`IntrinsicWidth` / `IntrinsicHeight`** | Sizes children based on their intrinsic dimensions (not performant). |
| **`Stack + Positioned`** | Places children at absolute positions within a Stack. |
| **`LayoutBuilder`** | Builds widget tree based on parent constraints. |
| **`MediaQuery`**    | Gets screen dimensions for responsive layouts. |

---

### 🧩 Example: Using `Row`, `Column`, `Expanded`, and `Padding`

```dart
Column(
  children: [
    Row(
      children: [
        Expanded(child: Container(color: Colors.red, height: 100)),
        Container(width: 100, height: 100, color: Colors.blue),
      ],
    ),
    Padding(
      padding: const EdgeInsets.all(8.0),
      child: Text("Hello Layout!"),
    ),
  ],
)
```
