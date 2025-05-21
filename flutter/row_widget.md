# Explain Row widget in Flutter

In Flutter, the `Row` widget is used to display its child widgets in a **horizontal direction** (from left to right). It's commonly used for layouts where you want to place elements side by side.

---

## 📦 Constructor

```dart
Row({
  Key? key,
  MainAxisAlignment mainAxisAlignment = MainAxisAlignment.start,
  MainAxisSize mainAxisSize = MainAxisSize.max,
  CrossAxisAlignment crossAxisAlignment = CrossAxisAlignment.center,
  TextDirection? textDirection,
  VerticalDirection verticalDirection = VerticalDirection.down,
  TextBaseline? textBaseline,
  List<Widget> children = const <Widget>[],
})
```

---

## 🧩 Important Properties

### 1. `children` ✅ *(Required)*

* A list of widgets arranged horizontally.

```dart
Row(
  children: [
    Icon(Icons.star),
    Text('Rating'),
  ],
)
```

---

### 2. `mainAxisAlignment`

* Controls how the children are placed along the **main axis** (horizontal).
* Enum: `MainAxisAlignment`

```dart
MainAxisAlignment.start       // default
MainAxisAlignment.center
MainAxisAlignment.end
MainAxisAlignment.spaceBetween
MainAxisAlignment.spaceAround
MainAxisAlignment.spaceEvenly
```

---

### 3. `crossAxisAlignment`

* Controls alignment **vertically** (cross axis) inside the Row.
* Enum: `CrossAxisAlignment`

```dart
CrossAxisAlignment.start
CrossAxisAlignment.center     // default
CrossAxisAlignment.end
CrossAxisAlignment.stretch
CrossAxisAlignment.baseline   // needs textBaseline to be set
```

---

### 4. `mainAxisSize`

* Determines how much horizontal space the `Row` should occupy.
* Enum: `MainAxisSize`

```dart
MainAxisSize.max   // default - takes full width
MainAxisSize.min   // fits to the content
```

---

### 5. `textDirection`

* Decides the direction of text and child widgets: LTR or RTL.

```dart
TextDirection.ltr  // default
TextDirection.rtl
```

---

### 6. `verticalDirection`

* Controls the order of vertical layout (when used with `crossAxisAlignment.start/end`).

```dart
VerticalDirection.down   // default
VerticalDirection.up
```

---

### 7. `textBaseline`

* Required if you use `CrossAxisAlignment.baseline`.

```dart
TextBaseline.alphabetic
TextBaseline.ideographic
```

---

## ✅ Example

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: [
    Icon(Icons.home),
    Text('Home'),
    Icon(Icons.settings),
  ],
)
```
