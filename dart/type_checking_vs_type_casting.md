# What is type-checking and type-casting in dart ?

In Dart, **type checking** and **type casting** are two different concepts used when dealing with types.

### 1. **Type Checking**  
Type checking is the process of verifying the type of an object at runtime using keywords like `is` and `is!`. This helps ensure that an object is of a certain type before performing operations on it.

#### Example:
```dart
void checkType(dynamic value) {
  if (value is String) {
    print('Value is a String with length: ${value.length}');
  } else {
    print('Value is not a String');
  }
}

void main() {
  checkType('Hello'); // Output: Value is a String with length: 5
  checkType(123);     // Output: Value is not a String
}
```

- `is` checks if an object is of a specific type.
- `is!` checks if an object is **not** of a specific type.

---

### 2. **Type Casting**  
Type casting is the process of converting an object from one type to another. In Dart, you can use the `as` keyword for explicit type casting.

#### Example:
```dart
void castType(dynamic value) {
  if (value is String) {
    String strValue = value; // Implicit casting
    print('String value: $strValue');
  }

  try {
    String castedValue = value as String; // Explicit casting
    print('Casted value: $castedValue');
  } catch (e) {
    print('Type casting failed: $e');
  }
}

void main() {
  castType('Hello'); // Works fine
  castType(123);     // Throws error: Type casting failed
}
```

- `as` performs explicit type casting.
- If the cast is not possible, it throws a `TypeError`.

---

### **Key Differences:**
| Feature        | Type Checking (`is`, `is!`) | Type Casting (`as`) |
|---------------|---------------------------|----------------------|
| Purpose       | Checks if an object is of a specific type | Converts an object to a specific type |
| Safety        | Safe, does not modify the object | Unsafe, throws an error if conversion fails |
| Usage         | Used for conditional checks before operations | Used when you are sure of the object's type |
| Example       | `if (value is String) {}` | `String s = value as String;` |

### **Best Practice:**
- **Use `is` before `as`** to avoid runtime errors.
```dart
if (value is String) {
  String str = value; // Safe
} else {
  print('Cannot cast');
}
```