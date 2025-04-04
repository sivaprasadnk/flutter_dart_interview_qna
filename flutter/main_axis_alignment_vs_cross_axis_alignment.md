# What is the difference between MainAxisAlignment and CrossAxisAlignment in Flutter?

In Flutter, **`MainAxisAlignment`** and **`CrossAxisAlignment`** are used to align widgets inside a **Row** or **Column**.


### 1. **Main Axis vs Cross Axis**
   - **Main Axis** → The primary direction of the layout.
     - In a **Row**, the main axis is **horizontal** (left to right).
     - In a **Column**, the main axis is **vertical** (top to bottom).
   - **Cross Axis** → The perpendicular direction to the main axis.
     - In a **Row**, the cross axis is **vertical** (top to bottom).
     - In a **Column**, the cross axis is **horizontal** (left to right).

---

### 2. **MainAxisAlignment**
   - Controls how widgets are positioned **along** the main axis.
   - Used inside **Row** (horizontal) and **Column** (vertical).

   ```dart
   Row(
     mainAxisAlignment: MainAxisAlignment.center, // Centers children horizontally
     children: [
       Text("A"),
       Text("B"),
       Text("C"),
     ],
   )
   ```

   **Options:**
   - `MainAxisAlignment.start` → Aligns at the start.
   - `MainAxisAlignment.end` → Aligns at the end.
   - `MainAxisAlignment.center` → Centers all widgets.
   - `MainAxisAlignment.spaceBetween` → Spaces widgets with no padding at start and end.
   - `MainAxisAlignment.spaceAround` → Spaces widgets with equal padding around them.
   - `MainAxisAlignment.spaceEvenly` → Spaces widgets with equal gaps including edges.

---

### 3. **CrossAxisAlignment**
   - Controls how widgets are positioned **along** the cross axis.
   - Used inside **Row** (vertical alignment) and **Column** (horizontal alignment).

   ```dart
   Column(
     crossAxisAlignment: CrossAxisAlignment.start, // Aligns children to the left
     children: [
       Text("A"),
       Text("B"),
       Text("C"),
     ],
   )
   ```

   **Options:**
   - `CrossAxisAlignment.start` → Aligns to the start (left in a Column, top in a Row).
   - `CrossAxisAlignment.end` → Aligns to the end (right in a Column, bottom in a Row).
   - `CrossAxisAlignment.center` → Centers all widgets.
   - `CrossAxisAlignment.stretch` → Expands widgets to fill the cross axis.
   - `CrossAxisAlignment.baseline` (only for **Row**) → Aligns based on the text baseline.

---

### 4. **Example Combining Both**
```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center,  // Aligns children to the center vertically
  crossAxisAlignment: CrossAxisAlignment.end, // Aligns children to the right
  children: [
    Text("A"),
    Text("B"),
    Text("C"),
  ],
)
```

### 5. **Summary**
|  | Row (Horizontal) | Column (Vertical) |
|---|---|---|
| **MainAxisAlignment** | Controls horizontal alignment | Controls vertical alignment |
| **CrossAxisAlignment** | Controls vertical alignment | Controls horizontal alignment |

Let me know if you need any examples or further clarification! 🚀
