# Explain where and any for lists in Dart

In Dart, `where` and `any` are both used to **evaluate elements in a list** based on a condition — but their **intent and return types are different**:

---

### 🔍 `where` – **Filter elements**

* **Returns an `Iterable`** of elements that match the condition.
* Use it when you want **all matching items**.

#### ✅ Example:

```dart
List<int> numbers = [1, 2, 3, 4];
var evens = numbers.where((n) => n.isEven);
print(evens); // Output: (2, 4)
```

---

### ❓ `any` – **Check if any element matches**

* **Returns a `bool`** (true or false).
* Use it when you just want to know: “**Is there at least one match?**”

#### ✅ Example:

```dart
List<int> numbers = [1, 3, 5];
bool hasEven = numbers.any((n) => n.isEven);
print(hasEven); // Output: false
```

---

### 📌 Summary Table:

| Method  | Purpose                              | Return Type   | Use Case                              |
| ------- | ------------------------------------ | ------------- | ------------------------------------- |
| `where` | Filter and **return matching items** | `Iterable<T>` | You want to get all matching elements |
| `any`   | **Check if any item matches**        | `bool`        | You just want to check for a match    |

