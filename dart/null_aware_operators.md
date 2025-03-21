# 🚀 **Null-Aware Operators in Dart**  

Null-aware operators in Dart are used to handle `null` values gracefully and avoid `null` reference errors. They help simplify the code by reducing the need for explicit `if-else` checks.

---

## 🔥 **1. `??` (Null Coalescing Operator)**
The `??` operator returns the **left-hand value** if it's **non-null**; otherwise, it returns the **right-hand value**.

### ✅ **Syntax:**
```dart
value ?? fallbackValue
```

### ✅ **Example:**
```dart
String? name;
String displayName = name ?? 'Guest';
print(displayName); // Output: Guest
```

👉 If `name` is `null`, `'Guest'` is used as the fallback value.

---

## 🔥 **2. `??=` (Null Assignment Operator)**
The `??=` operator assigns a value to a variable **only if it is currently null**.

### ✅ **Syntax:**
```dart
variable ??= value;
```

### ✅ **Example:**
```dart
String? name;
name ??= 'Guest';
print(name); // Output: Guest
```

👉 If `name` is `null`, `'Guest'` will be assigned to `name`.

---

## 🔥 **3. `?.` (Null-Aware Access Operator)**
The `?.` operator allows you to access properties or call methods on an object **only if it is not null**.  
- If the object is `null`, it returns `null` instead of throwing an error.

### ✅ **Syntax:**
```dart
object?.property
```

### ✅ **Example:**
```dart
String? name;
print(name?.length); // Output: null
```

👉 If `name` is `null`, `name.length` will not be accessed, and `null` will be returned.

---

## 🔥 **4. `!` (Non-Null Assertion Operator)**
The `!` operator **asserts** that a value is non-null.  
- If the value is `null`, it will throw a runtime error.  
- Use it only when you're certain that the value will never be `null`.

### ✅ **Syntax:**
```dart
value!
```

### ✅ **Example:**
```dart
String? name = 'John';
print(name!.length); // Output: 4
```

👉 If `name` is `null`, it will throw an error:
```dart
String? name;
print(name!.length); // Throws error: Null check operator used on a null value
```

---

## 🔥 **5. `...?` (Null-Aware Spread Operator)**
The `...?` operator allows you to spread elements from a list **only if the list is not null**.  
- If the list is `null`, nothing is added.

### ✅ **Syntax:**
```dart
[...?collection]
```

### ✅ **Example:**
```dart
List<int>? numbers;
List<int> allNumbers = [1, 2, ...?numbers];
print(allNumbers); // Output: [1, 2]
```

👉 If `numbers` is `null`, the spread operation is ignored without an error.

---

## 🌟 **Example Using All Operators**
```dart
void main() {
  String? name;
  int? age;

  // ?? operator
  print(name ?? 'Guest'); // Output: Guest
  
  // ??= operator
  name ??= 'John';
  print(name); // Output: John

  // ?. operator
  print(name?.length); // Output: 4

  // ! operator
  print(name!.length); // Output: 4

  // ...? operator
  List<int>? numbers;
  List<int> finalNumbers = [1, 2, ...?numbers];
  print(finalNumbers); // Output: [1, 2]
}
```

---

## ✅ **Summary**
| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `??` | Returns the right side if the left side is `null` | `name ?? 'Guest'` | `'Guest'` |
| `??=` | Assigns value only if the variable is `null` | `name ??= 'Guest'` | `'Guest'` |
| `?.` | Accesses a property/method only if the object is not `null` | `name?.length` | `null` (if `name` is null) |
| `!` | Asserts that the value is not `null` | `name!.length` | Throws error if `null` |
| `...?` | Spreads elements from a list only if it's not `null` | `[...?numbers]` | Skips if `numbers` is `null` |

---

👉 **Best Practice:**  
- ✅ Use `??` and `?.` for safe null handling.  
- ✅ Use `!` only if you're 100% sure the value won’t be `null`.  
- ✅ `...?` is useful for handling optional lists without boilerplate code. 😎