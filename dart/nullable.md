# **What is Nullable in Dart?**  

A **nullable** variable is one that **can hold a `null` value**. In Dart, you make a variable nullable by adding `?` after the type.  

---

### ✅ **Nullable vs Non-Nullable**  

```dart
String name = "Flutter";  // Non-nullable (Cannot be null)
String? nullableName;     // Nullable (Can be null)

nullableName = null; // ✅ Allowed
name = null;        // ❌ Error: Non-nullable variables cannot be null
```

---

### **Why Use Nullable Variables?**  
- To represent **optional** values (e.g., user input, API responses).  
- To handle **missing or unknown data** safely.  

---

### **How to Work with Nullable Variables?**  

1️⃣ **Null Check (`if` Statement)**  
```dart
if (nullableName != null) {
  print(nullableName.length);
}
```

2️⃣ **Null-Aware Operator (`?.`)**  
```dart
print(nullableName?.length); // ✅ Returns null instead of an error
```

3️⃣ **Default Value (`??`)**  
```dart
print(nullableName ?? "Default Name"); // ✅ Uses default if null
```

---

### **Final Thoughts**  
By default, **Dart does not allow null values** unless explicitly marked as nullable (`?`). This prevents null-related crashes and makes code **safer and more predictable**.  