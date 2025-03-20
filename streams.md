# 🚀 **Streams in Dart**  

A **Stream** in Dart is a sequence of asynchronous data events.  
- It allows you to handle a flow of data over time (like listening to real-time updates).  
- You can **listen** to a stream to receive data and act upon it.  

---

## ✅ **Why Use Streams?**  
- Handle real-time data (e.g., user input, sensor data, WebSockets).  
- Manage continuous or periodic events.  
- Efficient handling of large datasets or continuous updates.  

---

## 🎯 **Types of Streams**  
Dart supports two types of streams:  

| Type | Description | Example Use Case |
|-------|-------------|------------------|
| **Single Subscription Stream** | Can be listened to only **once** | API call, file reading |
| **Broadcast Stream** | Can be listened to **multiple times** | WebSocket, sensor data |

---

## ✅ **1. Single Subscription Stream**  
- Default type of stream.  
- Can only have **one listener** at a time.  
- Once a stream is listened to, it **cannot be listened to again**.  

### **Example: Single Subscription Stream**  
```dart
Stream<int> singleSubscriptionStream() async* {
  for (int i = 0; i < 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i; // Emit values
  }
}

void main() async {
  print('Start');
  
  // Listen to the stream
  await for (var value in singleSubscriptionStream()) {
    print('Value: $value');
  }
  
  print('End');
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
1. `singleSubscriptionStream` is created using `async*` and `yield`.  
2. The `await for` loop listens to the stream.  
3. The stream emits values one by one.  
4. After completion, the stream closes.  

---

## ✅ **2. Broadcast Stream**  
- Can have **multiple listeners** at the same time.  
- Useful for real-time data (e.g., WebSocket, user input).  

### **Example: Broadcast Stream**  
```dart
Stream<int> broadcastStream = Stream<int>.periodic(
  Duration(seconds: 1), 
  (count) => count,
).take(5).asBroadcastStream();

void main() {
  print('Start');

  // First Listener
  broadcastStream.listen((value) {
    print('Listener 1: $value');
  });

  // Second Listener
  broadcastStream.listen((value) {
    print('Listener 2: $value');
  });
}
```

### ✅ **Output:**  
```
Start  
Listener 1: 0  
Listener 2: 0  
Listener 1: 1  
Listener 2: 1  
Listener 1: 2  
Listener 2: 2  
Listener 1: 3  
Listener 2: 3  
Listener 1: 4  
Listener 2: 4  
```

### ✅ **How It Works:**  
1. `Stream<int>.periodic` generates values every second.  
2. `asBroadcastStream()` makes the stream broadcast-capable.  
3. Multiple listeners receive the same data simultaneously.  

---

## ✅ **How to Create Streams**  
There are three ways to create a stream in Dart:  

### **1. Using `Stream.fromIterable()`**  
Creates a stream from an iterable collection.  
```dart
Stream<int> stream = Stream.fromIterable([1, 2, 3, 4, 5]);

void main() async {
  await for (var value in stream) {
    print(value);
  }
}
```

---

### **2. Using `Stream.periodic()`**  
Generates events periodically.  
```dart
Stream<int> stream = Stream.periodic(Duration(seconds: 1), (count) => count).take(5);

void main() async {
  await for (var value in stream) {
    print(value);
  }
}
```

---

### **3. Using `async*` and `yield`**  
Creates a stream that emits values asynchronously.  
```dart
Stream<int> countStream() async* {
  for (int i = 0; i < 5; i++) {
    await Future.delayed(Duration(seconds: 1));
    yield i;
  }
}

void main() async {
  await for (var value in countStream()) {
    print(value);
  }
}
```

---

## ✅ **Listening to Streams**  
You can listen to a stream in three ways:  

### **1. Using `await for`**  
```dart
await for (var value in stream) {
  print(value);
}
```

---

### **2. Using `stream.listen()`**  
```dart
stream.listen((value) {
  print(value);
});
```

---

### **3. Using `stream.toList()`**  
```dart
List<int> values = await stream.toList();
print(values);
```

---

## ✅ **Handling Errors in Streams**  
You can handle errors using `onError` or `try-catch`.  

### **Example: Handling Errors**  
```dart
Stream<int> errorStream() async* {
  yield 1;
  throw Exception('Something went wrong');
}

void main() async {
  try {
    await for (var value in errorStream()) {
      print(value);
    }
  } catch (e) {
    print('Caught Error: $e');
  }
}
```

### ✅ **Output:**  
```
1  
Caught Error: Exception: Something went wrong  
```

---

## ✅ **Transforming Streams**  
You can transform stream data using:  

### **1. `map()`** – Transform data  
```dart
stream.map((value) => value * 2).listen(print);
```

---

### **2. `where()`** – Filter data  
```dart
stream.where((value) => value % 2 == 0).listen(print);
```

---

### **3. `take()`** – Take the first N values  
```dart
stream.take(3).listen(print);
```

---

### **4. `skip()`** – Skip the first N values  
```dart
stream.skip(2).listen(print);
```

---

### **5. `distinct()`** – Remove duplicate values  
```dart
stream.distinct().listen(print);
```

---

## ✅ **Pausing and Resuming Streams**  
You can control a stream using `pause()` and `resume()`.

### **Example:**  
```dart
var subscription = stream.listen((value) {
  print(value);
});

Future.delayed(Duration(seconds: 2), () {
  subscription.pause(); // Pause after 2 seconds
});

Future.delayed(Duration(seconds: 4), () {
  subscription.resume(); // Resume after 4 seconds
});
```

---

## 🚀 **When to Use Streams**  
| Scenario | Use Stream? |  
|----------|-------------|  
| Real-time data (e.g., WebSocket) | ✅ |  
| Periodic events (e.g., Timer) | ✅ |  
| One-time data fetch | ❌ (use `Future`) |  
| Continuous UI updates (e.g., sensor data) | ✅ |  

---

## 🌟 **Best Practices**  
✅ Use `async*` when you need to generate a stream.  
✅ Use `broadcast` for multiple listeners.  
✅ Always **close streams** to avoid memory leaks.  
✅ Handle errors with `onError` or `try-catch`.  
✅ Use `transform()` methods (`map`, `where`, etc.) to filter or modify data.  

---

## 🏆 **Summary**  
| Type | Description | Example |  
|-------|-------------|---------|  
| **Single Subscription Stream** | One-time stream, single listener | API call, file reading |  
| **Broadcast Stream** | Multiple listeners, real-time data | WebSocket, user input |  
| **Periodic Stream** | Emits data at regular intervals | Timer, clock |  
| **Error Handling** | Try-catch, onError | Network failure |  

---

### 🚀 **Quick Rule of Thumb:**  
- ✅ Use **Futures** → for a single result.  
- ✅ Use **Streams** → for a continuous flow of data. 😎