# 🚀 **async vs async\*** in Dart  

In Dart, `async` and `async*` are used to work with **asynchronous code**, but they handle data differently:

- `async` → Returns a **Future** (single value).  
- `async*` → Returns a **Stream** (multiple values over time).  

---

## ✅ **1. `async` – Returns a Future**  
- `async` is used when you want to return **a single result** in the future.  
- The function marked with `async` will **return a `Future`**.  
- `await` can be used inside an `async` function to wait for the result.  

### 🎯 **Syntax**
```dart
Future<int> getNumber() async {
  await Future.delayed(Duration(seconds: 2));
  return 42;
}
```

### ✅ **Example: Using async**  
```dart
void main() async {
  print('Start');
  int result = await getNumber();
  print('Result: $result');
  print('End');
}

Future<int> getNumber() async {
  await Future.delayed(Duration(seconds: 2));
  return 42;
}
```

### ✅ **Output:**  
```
Start  
Result: 42  
End  
```

### ✅ **How It Works:**  
1. `getNumber()` is marked as `async`, so it returns a `Future<int>`.  
2. `await` pauses execution until the `Future` completes.  
3. After 2 seconds, the value `42` is returned and printed.  

---

## ✅ **2. `async*` – Returns a Stream**  
- `async*` is used when you want to return **multiple values** over time.  
- The function marked with `async*` will **return a `Stream`**.  
- `yield` is used to emit values to the stream.  
- The function continues execution after each `yield`.  

### 🎯 **Syntax**
```dart
Stream<int> countStream() async* {
  for (int i = 0; i < 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}
```

### ✅ **Example: Using async***  
```dart
void main() async {
  print('Start');
  await for (var value in countStream()) {
    print('Value: $value');
  }
  print('End');
}

Stream<int> countStream() async* {
  for (int i = 0; i < 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i; // Emit value to the stream
  }
}
```

### ✅ **Output:**  
```
Start  
Value: 0  
Value: 1  
Value: 2  
Value: 3  
Value: 4  
End  
```

### ✅ **How It Works:**  
1. `countStream()` is marked as `async*`, so it returns a `Stream<int>`.  
2. The `await for` loop listens to the stream.  
3. `yield` emits values one at a time.  
4. After each `yield`, the function execution continues.  

---

## 🌟 **Key Differences**  
| Feature | `async` | `async*` |
|---------|---------|----------|
| **Return Type** | `Future<T>` | `Stream<T>` |
| **Use Case** | Single value | Multiple values over time |
| **Keyword** | `await` | `yield` |
| **Usage** | `await function()` | `await for (var x in function())` |
| **Execution** | Completes when the future completes | Continues until the stream closes |
| **Error Handling** | `try-catch` | `try-catch` |

---

## 🎯 **Example: Handling Errors**  
👉 Error handling works the same way for both `async` and `async*` using `try-catch`.

### ✅ `async`
```dart
Future<int> getNumber() async {
  try {
    throw Exception('Error occurred');
  } catch (e) {
    print('Caught error: $e');
    return -1;
  }
}

void main() async {
  int result = await getNumber();
  print('Result: $result');
}
```

### ✅ `async*`
```dart
Stream<int> countStream() async* {
  try {
    for (int i = 0; i < 5; i++) {
      if (i == 3) throw Exception('Error at $i');
      yield i;
    }
  } catch (e) {
    print('Caught error: $e');
  }
}

void main() async {
  await for (var value in countStream()) {
    print('Value: $value');
  }
}
```

### ✅ **Output:**  
```
Value: 0  
Value: 1  
Value: 2  
Caught error: Exception: Error at 3  
```

---

## 🚀 **When to Use `async` vs `async*`**  
| Scenario | Use `async` | Use `async*` |
|----------|-------------|--------------|
| Single value result | ✅ | ❌ |
| Multiple values over time | ❌ | ✅ |
| Fetching data from API | ✅ | ❌ |
| Generating a sequence of values | ❌ | ✅ |
| Listening for real-time events | ❌ | ✅ |
| Background processing | ✅ | ❌ |
| WebSocket communication | ❌ | ✅ |

---

## ✅ **Best Practices**  
✅ Use `async` for short-lived, single-result tasks.  
✅ Use `async*` for continuous streams of data (e.g., live data).  
✅ Always handle errors with `try-catch`.  
✅ Use `await for` to listen to a stream from `async*`.  
✅ Close streams properly to avoid memory leaks.  

---

## 🏆 **Summary**  
| Feature | `async` | `async*` |
|---------|---------|----------|
| Returns | `Future` | `Stream` |
| Values | Single result | Multiple results |
| Emitting Data | `return` | `yield` |
| Error Handling | `try-catch` | `try-catch` |
| Example Use | Fetching data, calculations | Live data, real-time updates |

---

### 🚀 **Quick Rule of Thumb:**  
- ✅ Use `async` → for single value tasks (e.g., API calls).  
- ✅ Use `async*` → for multiple value tasks (e.g., WebSocket or data streams). 😎