# Explain Flexible widget in Flutter

In Flutter, `Flexible` is a widget used inside **Flex containers** like `Row`, `Column`, or `Flex`. It helps you control how a child of a `Flex` layout (e.g., `Row` or `Column`) **expands or shrinks** to occupy available space.

### 🔧 Purpose:

It gives a child widget **flexibility** to expand and fill the available space **proportionally** based on a `flex` factor.

---

### 🧱 Basic Syntax:

```dart
Flexible(
  flex: 1,
  fit: FlexFit.loose, // or FlexFit.tight
  child: YourWidget(),
)
```

---

### 🧠 Key Parameters:

| Parameter | Description                                                                                                                                                         |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `flex`    | Integer value representing how much space this child should take **relative to siblings**. Default is 1.                                                            |
| `fit`     | Either `FlexFit.loose` or `FlexFit.tight`: <br> - `loose`: child can be smaller than the allocated space. <br> - `tight`: forces child to fill the allocated space. |

---

### 📦 Example:

```dart
Row(
  children: [
    Flexible(
      flex: 2,
      child: Container(color: Colors.red, height: 100),
    ),
    Flexible(
      flex: 1,
      child: Container(color: Colors.blue, height: 100),
    ),
  ],
)
```

🔍 In this example:

* The red container takes **2 parts** of space.
* The blue container takes **1 part**.
* Total parts = 2 + 1 = 3 → Red takes **2/3**, Blue takes **1/3** of horizontal space.

---

### 🆚 `Flexible` vs `Expanded`:

`Expanded` is a **shorthand** for:

```dart
Flexible(flex: 1, fit: FlexFit.tight)
```

So:

* Use `Expanded` when the child **must** take all available space.
* Use `Flexible` when the child **may** take less space (especially with `FlexFit.loose`).

---

### ✅ When to Use `Flexible`:

* When you want a child in a `Row` or `Column` to **share space proportionally**.
* When you want **more control** over how much space a widget can use compared to others.
* When you want to **avoid overflow errors** in flexible layouts.
