In Flutter (and Dart), `static`, `final`, and `const` are used to define how variables and properties are stored and accessed. They have different purposes related to memory allocation, value assignment, and immutability.

---

## 🚀 **1. `static`**  
- Used to declare **class-level variables** and methods.  
- The value is shared across all instances of the class.  
- Allocated only **once in memory** (shared across all objects).  

### ✅ **Use Cases:**
- For constants or values that don’t depend on object instances.  
- For utility methods or functions that are independent of object state.  

### **Example:**
```dart
class MyClass {
  static int counter = 0;

  static void incrementCounter() {
    counter++;
    print('Counter: $counter');
  }
}

void main() {
  MyClass.incrementCounter(); // Counter: 1
  MyClass.incrementCounter(); // Counter: 2
}
```

### 🔎 **Explanation:**
- `counter` is shared across all instances of `MyClass`.  
- `incrementCounter()` can be accessed directly using the class name without creating an instance.  

---

### ❌ **Without `static`**
If `counter` is not static, each object of `MyClass` would have its own `counter` value.

```dart
class MyClass {
  int counter = 0;

  void incrementCounter() {
    counter++;
    print('Counter: $counter');
  }
}

void main() {
  MyClass obj1 = MyClass();
  MyClass obj2 = MyClass();

  obj1.incrementCounter(); // Counter: 1
  obj2.incrementCounter(); // Counter: 1 (Separate value)
}
```

---

## 🚀 **2. `final`**  
- Used to declare a variable whose value **can’t be reassigned** after being set.  
- The value is assigned at **runtime**.  
- The object itself is immutable, but the **internal state** of an object is mutable (if not `const`).  

### ✅ **Use Cases:**
- When the value is known only at runtime.  
- When the value doesn’t need to change after initialization.  

### **Example:**
```dart
class MyClass {
  final int value;

  MyClass(this.value);
}

void main() {
  final obj = MyClass(10);
  print(obj.value); // 10

  // obj.value = 20; // ❌ Error - Can't reassign a final variable
}
```

### 🔎 **Explanation:**
- `value` is assigned when `MyClass` is instantiated.  
- After assignment, `value` **cannot be changed**.  

---

### ✅ **Final with Collections**
The object reference is immutable, but the contents can be changed (unless `const`).  
```dart
final list = [1, 2, 3];
list.add(4); // ✅ Allowed
print(list); // [1, 2, 3, 4]

// list = [5, 6, 7]; // ❌ Error - Can't reassign the reference
```

---

## 🚀 **3. `const`**  
- Used to declare a variable whose value is known at **compile-time**.  
- The value is assigned at **compile-time** and is immutable.  
- Both the object and its internal state are **completely immutable**.  

### ✅ **Use Cases:**
- For defining constant values (e.g., API keys, app settings).  
- When you want to define an immutable object at compile-time.  

### **Example:**
```dart
const pi = 3.14;
const appName = 'MyApp';

void main() {
  print(pi); // 3.14
  print(appName); // MyApp
}
```

### 🔎 **Explanation:**
- The value is known at compile-time and stored in memory as a constant.  
- Cannot be modified at runtime.  

---

### ✅ **Const with Objects**
```dart
class MyClass {
  final String name;
  const MyClass(this.name);
}

void main() {
  const obj = MyClass('Flutter');
  print(obj.name); // Flutter

  // obj.name = 'Dart'; // ❌ Error - Immutable value
}
```

- `const` creates an **immutable object**.
- If you want to create multiple objects with the same values, Dart will **reuse the object** from memory to improve performance.

---

### ✅ **Const with Collections**
```dart
const list = [1, 2, 3];

// list.add(4); // ❌ Error - Can't modify a const list
```

- A `const` list cannot be modified after initialization.  

---

## 🆚 **Differences Between `final` and `const`**
| Feature | `final` | `const` |
|---------|---------|---------|
| Assignment | Assigned at runtime | Assigned at compile-time |
| Mutability | Value can't be reassigned, but content can be modified | Completely immutable |
| When to Use | When the value is known at runtime | When the value is known at compile-time |
| Object State | State can change if object isn’t constant | State cannot change |

---

## 🆚 **Differences Between `static`, `final`, and `const`**
| Feature | `static` | `final` | `const` |
|---------|---------|---------|---------|
| Storage | Allocated once (class level) | Instance-specific | Compile-time allocated |
| Value Assignment | Can be changed | Can’t be reassigned | Fixed at compile-time |
| Access | Accessed using class name | Requires instance (unless static) | Requires instance (unless static) |
| Immutability | Value can be changed | Value can’t be reassigned, but state can change | Completely immutable |

---

## 🔥 **Example Combining All Three**
```dart
class MyClass {
  static int count = 0; // Shared among all instances
  final String name; // Immutable after assignment
  static const double pi = 3.14; // Compile-time constant

  MyClass(this.name);

  void display() {
    print('Name: $name, Count: $count, Pi: $pi');
  }
}

void main() {
  var obj1 = MyClass('Flutter');
  var obj2 = MyClass('Dart');

  MyClass.count = 5; // ✅ Can change static value
  obj1.display(); // Name: Flutter, Count: 5, Pi: 3.14
  obj2.display(); // Name: Dart, Count: 5, Pi: 3.14

  // obj1.name = 'New Name'; // ❌ Error - Can't modify final value
  // MyClass.pi = 3.1415; // ❌ Error - Can't modify const value
}
```

### ✅ **How It Works:**
1. `count` is shared between all instances of `MyClass`.  
2. `final name` is assigned during object creation and can’t be changed.  
3. `const pi` is fixed at compile-time and cannot be modified.  

---

## 🎯 **Best Practices**
✅ Use `static` for class-level properties or methods.  
✅ Use `final` for values that are known only at runtime but shouldn’t be reassigned.  
✅ Use `const` for values that are fixed at compile-time and immutable.  
✅ Use `const` constructors when possible to improve performance and reduce memory usage.  

---

## 🚀 **Summary**
| Keyword | Purpose | When to Use | Example |
|---------|---------|-------------|---------|
| `static` | Class-level value or method | When the value is shared across all instances | `int count = 0;` |
| `final` | Immutable after assignment | When the value is known at runtime | `final name = 'Flutter';` |
| `const` | Immutable and compile-time constant | When the value is fixed at compile-time | `const pi = 3.14;` |
