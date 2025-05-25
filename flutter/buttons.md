# Explain Buttons in Flutter

Flutter provides several built-in button widgets for different use cases. Here's a quick overview of the most commonly used buttons in Flutter:

---

### 🔹 1. **ElevatedButton**

* Used for prominent actions.
* Has elevation (shadow) by default.

```dart
ElevatedButton(
  onPressed: () {
    print('Pressed');
  },
  child: Text('Elevated Button'),
),
```

---

### 🔹 2. **TextButton**

* Flat button with no elevation.
* Used for less important actions.

```dart
TextButton(
  onPressed: () {
    print('Pressed');
  },
  child: Text('Text Button'),
),
```

---

### 🔹 3. **OutlinedButton**

* Similar to `TextButton` but with an outline border.

```dart
OutlinedButton(
  onPressed: () {
    print('Pressed');
  },
  child: Text('Outlined Button'),
),
```

---

### 🔹 4. **IconButton**

* A clickable icon (no text).

```dart
IconButton(
  icon: Icon(Icons.favorite),
  onPressed: () {
    print('Icon pressed');
  },
),
```

---

### 🔹 5. **FloatingActionButton**

* A circular button usually used for primary actions in `Scaffold`.

```dart
FloatingActionButton(
  onPressed: () {
    print('FAB pressed');
  },
  child: Icon(Icons.add),
),
```

---

### 🔹 6. **Custom Button (Using InkWell or GestureDetector)**

You can make custom-shaped or styled buttons:

```dart
InkWell(
  onTap: () {
    print('Tapped');
  },
  child: Container(
    padding: EdgeInsets.all(12),
    decoration: BoxDecoration(
      color: Colors.blue,
      borderRadius: BorderRadius.circular(8),
    ),
    child: Text('Custom Button', style: TextStyle(color: Colors.white)),
  ),
),
```

---

### 🛠️ Customization

All buttons can be customized using:

* `style:` for `ElevatedButton`, `TextButton`, `OutlinedButton`
* Use `ButtonStyle` to change padding, shape, background color, etc.

```dart
ElevatedButton(
  onPressed: () {},
  style: ElevatedButton.styleFrom(
    backgroundColor: Colors.green,
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.circular(16),
    ),
  ),
  child: Text('Styled Button'),
),
```

---
