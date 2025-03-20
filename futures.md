# 🚀 **What Is a Future?**  

A `Future<T>` represents a **potential value** or **error** that will be available after an asynchronous operation completes.  
- `T` → Type of value returned when the operation succeeds.  
- If the operation fails, the `Future` completes with an **error** instead of a value.  

---

### ✅ **When to Use Futures**  
- Fetching data from the internet.  
- Reading files from disk.  
- Waiting for user input.  
- Performing expensive calculations.  

---

## 🏷️ **Creating a Future**  

### 🔹 1. **Using `Future.value()`**  
Creates a Future that returns a value immediately.  
```dart
Future<int> getValue() {
  return Future.value(42);
}

void main() async {
  int result = await getValue();
  print(result); // Output: 42
}
```

---

### 🔹 2. **Using `Future.error()`**  
Creates a Future that returns an error immediately.  
```dart
Future<int> getValue() {
  return Future.error('Something went wrong');
}

void main() async {
  try {
    int result = await getValue();
    print(result);
  } catch (e) {
    print('Error: $e'); // Output: Error: Something went wrong
  }
}
```

---

### 🔹 3. **Using `Future.delayed()`**  
Creates a Future that completes after a specified delay.  
```dart
Future<String> fetchData() {
  return Future.delayed(Duration(seconds: 2), () => 'Data Loaded');
}

void main() async {
  print('Fetching data...');
  String data = await fetchData();
  print(data); // Output after 2 seconds: Data Loaded
}
```

---

### 🔹 4. **Using `async` Keyword**  
`async` makes a function return a Future automatically.  
```dart
Future<String> fetchData() async {
  await Future.delayed(Duration(seconds: 2));
  return 'Data Loaded';
}

void main() async {
  print('Fetching data...');
  String data = await fetchData();
  print(data); // Output after 2 seconds: Data Loaded
}
```

---

## 🏷️ **Consuming Futures**  

### 🔹 1. **Using `await`**  
Use `await` to pause execution until the Future completes.  
```dart
void main() async {
  String data = await fetchData();
  print(data);
}
```

---

### 🔹 2. **Using `.then()`**  
Use `.then()` to handle the result when the Future completes.  
```dart
fetchData().then((data) {
  print(data);
}).catchError((error) {
  print('Error: $error');
});
```

---

### 🔹 3. **Using `try-catch`**  
Use `try-catch` to handle errors when using `await`.  
```dart
void main() async {
  try {
    String data = await fetchData();
    print(data);
  } catch (e) {
    print('Error: $e');
  }
}
```

---

## 🏷️ **Example with Success and Error Handling**  
```dart
Future<String> fetchData(bool throwError) async {
  await Future.delayed(Duration(seconds: 2));
  if (throwError) {
    throw 'Failed to load data';
  }
  return 'Data Loaded';
}

void main() async {
  try {
    String data = await fetchData(false);
    print(data);
  } catch (e) {
    print('Error: $e');
  }
}
```

### ✅ Output (if `throwError` is `false`)  
```
Data Loaded
```

### ✅ Output (if `throwError` is `true`)  
```
Error: Failed to load data
```

---

## 🏷️ **Chaining Futures**  
You can chain multiple Futures using `.then()` and `.catchError()`.

```dart
Future<int> add(int a, int b) {
  return Future.value(a + b);
}

void main() {
  add(2, 3)
      .then((value) => value * 2)
      .then((value) => print(value)) // Output: 10
      .catchError((error) => print('Error: $error'));
}
```

---

## 🏷️ **Completer**  
You can manually create and complete a Future using `Completer`.

### 🔹 Example  
```dart
Future<String> getData() {
  final completer = Completer<String>();

  Future.delayed(Duration(seconds: 2), () {
    completer.complete('Data Loaded');
  });

  return completer.future;
}

void main() async {
  String data = await getData();
  print(data); // Output after 2 seconds: Data Loaded
}
```

- `Completer.complete()` → Completes the future with a value.  
- `Completer.completeError()` → Completes the future with an error.  

---

## 🏷️ **Handling Multiple Futures**  

### 🔹 1. **Future.wait()**  
Waits for multiple Futures to complete.  
```dart
Future<String> fetchUser() async => 'User data';
Future<String> fetchPosts() async => 'Posts data';

void main() async {
  final results = await Future.wait([fetchUser(), fetchPosts()]);
  print(results); // Output: [User data, Posts data]
}
```

---

### 🔹 2. **Future.any()**  
Completes with the result of the first Future to finish.  
```dart
Future<String> getFastestData() {
  return Future.any([
    Future.delayed(Duration(seconds: 3), () => 'Slow Data'),
    Future.delayed(Duration(seconds: 1), () => 'Fast Data'),
  ]);
}

void main() async {
  String data = await getFastestData();
  print(data); // Output: Fast Data
}
```

---

### 🔹 3. **Future.forEach()**  
Runs a function on each element in a list, one by one.  
```dart
Future<void> printItems(List<int> items) async {
  await Future.forEach(items, (item) async {
    await Future.delayed(Duration(seconds: 1));
    print(item);
  });
}

void main() async {
  await printItems([1, 2, 3]);
  // Output:
  // 1
  // 2
  // 3
}
```

---

## ✅ **Future Lifecycle**  
| State | Description |
|-------|-------------|
| **Uncompleted** | Future is created but hasn’t completed yet. |
| **Completed with Value** | Future is completed successfully with a value. |
| **Completed with Error** | Future is completed with an error. |

---

## 🚀 **Best Practices**  
✔️ Use `await` for better readability.  
✔️ Handle errors using `try-catch` or `.catchError()`.  
✔️ Use `Future.wait()` for parallel execution.  
✔️ Use `Completer` only when manual control over a Future is needed.  
✔️ Avoid using `.then()` and `await` together on the same Future.  

---

## 🎯 **Summary**  
| Concept | Description |
|---------|-------------|
| `Future.value()` | Creates a completed Future with a value |
| `Future.error()` | Creates a completed Future with an error |
| `Future.delayed()` | Creates a Future that completes after a delay |
| `async/await` | Handles Futures in a readable way |
| `.then()` | Chains Futures |
| `Completer` | Manually controls Future completion |
| `Future.wait()` | Waits for multiple Futures to complete |
| `Future.any()` | Completes with the first Future to finish |

---

🔥 **Futures** are at the core of Dart’s async model — master them, and you’ll handle async tasks like a pro! 😎