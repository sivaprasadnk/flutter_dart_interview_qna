# Explain Positioned widget in Flutter

---

## 🔧 `Positioned` Widget Constructor

```dart
Positioned({
  Key? key,
  double? left,
  double? top,
  double? right,
  double? bottom,
  double? width,
  double? height,
  required Widget child,
})
```

---

## ✅ Variants and Use Cases

### 1. **Basic Positioning (top, left, right, bottom)**

```dart
Positioned(
  top: 10,
  left: 20,
  child: YourWidget(),
)
```

* Positions the widget 10 px from the top and 20 px from the left.

---

### 2. **Positioning with Right and Bottom**

```dart
Positioned(
  right: 10,
  bottom: 20,
  child: YourWidget(),
)
```

* Places the widget 10 px from the right and 20 px from the bottom.

---

### 3. **Fixed Width and Height**

```dart
Positioned(
  top: 30,
  left: 30,
  width: 100,
  height: 50,
  child: YourWidget(),
)
```

* Forces the child to take the specified size regardless of its intrinsic size.

---

### 4. **Full Stretch (pin to all sides)**

```dart
Positioned(
  top: 0,
  left: 0,
  right: 0,
  bottom: 0,
  child: YourWidget(),
)
```

* Makes the child fill the `Stack` completely (like `Positioned.fill`).

---

### 5. **Only One Side Specified (auto-sizing)**

```dart
Positioned(
  top: 10,
  child: YourWidget(),
)
```

* Positions the widget 10 px from the top and lets it take its natural size and alignment horizontally.

---

### 6. **With `Positioned.fill` (Shortcut)**

```dart
Positioned.fill(
  child: YourWidget(),
)
```

* Equivalent to setting `top: 0, left: 0, right: 0, bottom: 0`.

---

### 7. **With `Positioned.directional` (RTL Support)**

```dart
Positioned.directional(
  top: 10,
  start: 20,
  child: YourWidget(),
)
```

* Uses `start` and `end` instead of `left` and `right` to support right-to-left languages (like Arabic or Hebrew).
* Requires a `Directionality` widget higher in the widget tree.

---

## 📦 Full Example:

```dart
Stack(
  children: [
    Container(width: 300, height: 300, color: Colors.grey[300]),
    Positioned(
      top: 20,
      left: 20,
      width: 100,
      height: 50,
      child: Container(color: Colors.red),
    ),
    Positioned.fill(
      child: Opacity(
        opacity: 0.1,
        child: Container(color: Colors.blue),
      ),
    ),
  ],
)
```
