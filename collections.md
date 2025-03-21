# **🚀 Collections in Dart**

Dart provides three main types of collections to store and manipulate data efficiently:
1. **List** (Ordered & Duplicates Allowed)
2. **Set** (Unordered & Unique)
3. **Map** (Key-Value Pairs)

---

# **📌 1. List in Dart (Ordered Collection)**
A **List** is an ordered collection that allows duplicate elements. It's similar to an array in other languages.

### **✅ Creating a List**
```dart
void main() {
  List<int> numbers = [1, 2, 3, 4, 5]; // List of integers
  print(numbers); // Output: [1, 2, 3, 4, 5]
}
```

### **✅ List Properties**
- **Ordered**: Elements are stored in a specific order.
- **Allows duplicates**: Same values can be stored multiple times.
- **Can be mutable (`List`) or immutable (`const List`)**.

### **✅ Adding Elements**
```dart
void main() {
  var names = ['Alice', 'Bob'];
  names.add('Charlie'); // Add a single element
  names.addAll(['David', 'Eve']); // Add multiple elements

  print(names); // Output: [Alice, Bob, Charlie, David, Eve]
}
```

### **✅ Removing Elements**
```dart
void main() {
  var numbers = [1, 2, 3, 4, 5];
  numbers.remove(3); // Removes value 3
  numbers.removeAt(0); // Removes element at index 0

  print(numbers); // Output: [2, 4, 5]
}
```

### **✅ Iterating Over a List**
```dart
void main() {
  var numbers = [10, 20, 30];

  for (var num in numbers) {
    print(num);
  }
}
```

### **✅ Checking Elements**
```dart
void main() {
  var numbers = [1, 2, 3];
  print(numbers.contains(2)); // Output: true
}
```

### **✅ Fixed-Length List**
```dart
void main() {
  var fixedList = List<int>.filled(3, 0); // Creates a list of length 3 with all elements set to 0
  print(fixedList); // Output: [0, 0, 0]
}
```

---

# **📌 2. Set in Dart (Unique & Unordered Collection)**
A **Set** is an unordered collection of unique elements.

### **✅ Creating a Set**
```dart
void main() {
  Set<int> numbers = {1, 2, 3, 4, 5};
  print(numbers); // Output: {1, 2, 3, 4, 5}
}
```

### **✅ Adding Elements**
```dart
void main() {
  var uniqueNumbers = {1, 2, 3};
  uniqueNumbers.add(3); // Ignored (Duplicate)
  uniqueNumbers.add(4);

  print(uniqueNumbers); // Output: {1, 2, 3, 4}
}
```

### **✅ Removing Elements**
```dart
void main() {
  var numbers = {1, 2, 3, 4};
  numbers.remove(3);

  print(numbers); // Output: {1, 2, 4}
}
```

### **✅ Set Operations**
```dart
void main() {
  var set1 = {1, 2, 3, 4};
  var set2 = {3, 4, 5, 6};

  print(set1.union(set2)); // {1, 2, 3, 4, 5, 6}
  print(set1.intersection(set2)); // {3, 4}
  print(set1.difference(set2)); // {1, 2}
}
```

---

# **📌 3. Map in Dart (Key-Value Pairs)**
A **Map** is a collection of key-value pairs where each key is unique.

### **✅ Creating a Map**
```dart
void main() {
  Map<String, int> studentMarks = {
    'Alice': 90,
    'Bob': 85,
    'Charlie': 92
  };

  print(studentMarks); // Output: {Alice: 90, Bob: 85, Charlie: 92}
}
```

### **✅ Adding and Accessing Elements**
```dart
void main() {
  var studentMarks = {'Alice': 90, 'Bob': 85};

  studentMarks['Charlie'] = 95; // Adding a new key-value pair
  print(studentMarks['Bob']); // Output: 85
}
```

### **✅ Removing Elements**
```dart
void main() {
  var studentMarks = {'Alice': 90, 'Bob': 85, 'Charlie': 95};

  studentMarks.remove('Bob');
  print(studentMarks); // Output: {Alice: 90, Charlie: 95}
}
```

### **✅ Checking Keys & Values**
```dart
void main() {
  var studentMarks = {'Alice': 90, 'Bob': 85};

  print(studentMarks.containsKey('Alice')); // true
  print(studentMarks.containsValue(100)); // false
}
```

---

# **📌 4. Special Collection Features**
### **✅ Spread Operator (`...` & `...?`)**
Used to combine multiple collections.
```dart
void main() {
  var list1 = [1, 2, 3];
  var list2 = [4, 5, 6];

  var mergedList = [...list1, ...list2];
  print(mergedList); // Output: [1, 2, 3, 4, 5, 6]
}
```
---
### **✅ Null-aware Spread Operator (`...?`)**
```dart
void main() {
  List<int>? nullableList;
  var newList = [...?nullableList, 10, 20];

  print(newList); // Output: [10, 20]
}
```

---

# **📌 5. Collection If & For**
### **✅ Using `if` in List**
```dart
void main() {
  bool isAdmin = true;

  var menu = [
    'Home',
    'Profile',
    if (isAdmin) 'Admin Panel' // Added conditionally
  ];

  print(menu); // Output: [Home, Profile, Admin Panel]
}
```

### **✅ Using `for` in List**
```dart
void main() {
  var numbers = [1, 2, 3];
  var doubledNumbers = [for (var num in numbers) num * 2];

  print(doubledNumbers); // Output: [2, 4, 6]
}
```

---

# **🚀 Summary**
| Collection Type | Ordered? | Allows Duplicates? | Key-Value? |
|----------------|---------|-------------------|------------|
| **List** | ✅ Yes | ✅ Yes | ❌ No |
| **Set** | ❌ No | ❌ No | ❌ No |
| **Map** | ❌ No | ✅ Yes (Values) | ✅ Yes (Keys) |

📌 **When to Use What?**
- **List** → When you need an **ordered collection** with duplicates.
- **Set** → When you need **unique values** and don’t care about order.
- **Map** → When you need to store **key-value pairs** for fast lookups.