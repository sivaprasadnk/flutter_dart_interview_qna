# What is the difference between var and dynamic in Flutter?

In Flutter (and Dart specifically), both `var` and `dynamic` are used for variable declarations, but they behave differently. Here's a clear breakdown:

---

### 🔹 `var`

- **Type Inference**: The type is inferred at **compile time** based on the assigned value.
- **Fixed Type**: Once inferred, the variable **can't change to another type**.
- **Safer**: You get compile-time checking and autocompletion.

```dart
var name = 'Flutter';  // inferred as String
name = 'Dart';         // ✅ OK
name = 123;            // ❌ Error: can't assign int to String
```

---

### 🔹 `dynamic`

- **No Type Checking**: The type is determined at **runtime**, and the variable can hold **any type**.
- **Less Safe**: No compile-time type checking; more prone to runtime errors.

```dart
dynamic name = 'Flutter';
name = 123;            // ✅ OK
name = true;           // ✅ OK

print(name.length);    // ❌ Runtime error if name isn't a String
```

---

### 🔸 Summary Table:

| Keyword | Type Inferred | Type Can Change | Compile-Time Safety |
|--------|----------------|------------------|----------------------|
| `var`  | ✅ Yes         | ❌ No            | ✅ Yes               |
| `dynamic` | ❌ No       | ✅ Yes           | ❌ No                |

---

### ✅ When to Use What?

- Use `**var**` when you know the type won’t change. It helps the compiler catch mistakes early.
- Use `**dynamic**` only when **you absolutely need flexibility**, like parsing JSON or handling loosely-typed data.

---
