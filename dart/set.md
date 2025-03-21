# **🚀 Set in Dart**

A **Set** in Dart is a collection of **unique elements** that do not allow duplicates. Unlike lists, sets are **unordered** and optimized for **fast lookups**.

---

## **🔹 1. Creating a Set**
### ✅ **Using `{}` (Literal)**
```dart
void main() {
  var numbers = {1, 2, 3, 4, 5};
  print(numbers); // Output: {1, 2, 3, 4, 5}
}
```

### ✅ **Using `Set()` Constructor**
```dart
void main() {
  Set<String> names = Set();
  names.add("Alice");
  names.add("Bob");
  names.add("Alice"); // Duplicate (ignored)

  print(names); // Output: {Alice, Bob}
}
```

---

## **🔹 2. Key Properties of Sets**
✔ **Unordered** → Elements are stored without a specific order.  
✔ **Unique elements** → No duplicate values.  
✔ **Efficient** → Lookups and insertions are faster than lists.

---

## **🔹 3. Adding Elements**
### ✅ **`add()` - Adds a single element**
```dart
void main() {
  var numbers = {1, 2, 3};
  numbers.add(4);
  print(numbers); // Output: {1, 2, 3, 4}
}
```

### ✅ **`addAll()` - Adds multiple elements**
```dart
void main() {
  var set1 = {1, 2, 3};
  var set2 = {3, 4, 5};

  set1.addAll(set2);
  print(set1); // Output: {1, 2, 3, 4, 5}
}
```

---

## **🔹 4. Removing Elements**
### ✅ **`remove()` - Removes a specific element**
```dart
void main() {
  var numbers = {1, 2, 3, 4, 5};
  numbers.remove(3);
  print(numbers); // Output: {1, 2, 4, 5}
}
```

### ✅ **`removeWhere()` - Removes elements based on a condition**
```dart
void main() {
  var numbers = {1, 2, 3, 4, 5};
  numbers.removeWhere((num) => num % 2 == 0); // Remove even numbers

  print(numbers); // Output: {1, 3, 5}
}
```

### ✅ **`clear()` - Removes all elements**
```dart
void main() {
  var numbers = {1, 2, 3};
  numbers.clear();
  print(numbers); // Output: {}
}
```

---

## **🔹 5. Checking Elements**
### ✅ **`contains()` - Checks if an element exists**
```dart
void main() {
  var numbers = {1, 2, 3};
  print(numbers.contains(2)); // Output: true
  print(numbers.contains(5)); // Output: false
}
```

### ✅ **`isEmpty` & `isNotEmpty` - Checks if a set is empty**
```dart
void main() {
  var numbers = {};
  print(numbers.isEmpty); // Output: true

  var names = {"Alice"};
  print(names.isNotEmpty); // Output: true
}
```

---

## **🔹 6. Set Operations**
### ✅ **`union()` - Combines two sets**
```dart
void main() {
  var set1 = {1, 2, 3};
  var set2 = {3, 4, 5};

  print(set1.union(set2)); // Output: {1, 2, 3, 4, 5}
}
```

### ✅ **`intersection()` - Common elements between two sets**
```dart
void main() {
  var set1 = {1, 2, 3};
  var set2 = {3, 4, 5};

  print(set1.intersection(set2)); // Output: {3}
}
```

### ✅ **`difference()` - Elements in one set but not in another**
```dart
void main() {
  var set1 = {1, 2, 3, 4, 5};
  var set2 = {3, 4, 5, 6, 7};

  print(set1.difference(set2)); // Output: {1, 2}
}
```

---

## **🔹 7. Iterating Over a Set**
### ✅ **Using `forEach()`**
```dart
void main() {
  var numbers = {1, 2, 3};

  numbers.forEach((num) => print(num));
}
```

### ✅ **Using `for-in` loop**
```dart
void main() {
  var numbers = {1, 2, 3};

  for (var num in numbers) {
    print(num);
  }
}
```

---

## **🔹 8. Converting Between List and Set**
### ✅ **Convert List to Set (Remove Duplicates)**
```dart
void main() {
  List<int> numbers = [1, 2, 2, 3, 4, 4, 5];
  Set<int> uniqueNumbers = numbers.toSet();

  print(uniqueNumbers); // Output: {1, 2, 3, 4, 5}
}
```

### ✅ **Convert Set to List**
```dart
void main() {
  Set<String> names = {"Alice", "Bob", "Charlie"};
  List<String> nameList = names.toList();

  print(nameList); // Output: [Alice, Bob, Charlie]
}
```

---

## **🔹 9. HashSet for Faster Lookups**
- `HashSet` is optimized for **fast lookups** and **does not maintain order**.
- Faster than regular `Set` when dealing with large data.

```dart
import 'dart:collection';

void main() {
  HashSet<int> numbers = HashSet();
  numbers.addAll([1, 2, 3, 4, 5]);

  print(numbers.contains(3)); // Output: true
}
```

---

## **🚀 Summary**
| Feature | Description |
|---------|-------------|
| **Unique Elements** | ✅ No duplicates allowed |
| **Unordered** | ✅ Elements are not stored in a fixed order |
| **Fast Lookups** | ✅ Faster than a list for searching elements |
| **Union & Intersection** | ✅ Supports mathematical set operations |
| **Convert List to Set** | ✅ Removes duplicates automatically |

✅ **Use Sets when you need uniqueness and fast lookups!** 🚀