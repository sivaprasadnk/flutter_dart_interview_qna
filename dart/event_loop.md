# **🚀 What is the Event Loop in Dart?**  

The **Event Loop** in Dart is a mechanism that manages the execution of asynchronous tasks like **Futures**, **Streams**, **Timers**, and **I/O operations** while keeping Dart **single-threaded**.

---

## **🛠 How the Event Loop Works?**
Dart has **two queues** for handling asynchronous tasks:

1. **Microtask Queue** (High Priority)  
   - Executes **before** the event queue.  
   - Includes **`scheduleMicrotask()`** and some **Future-based** tasks.

2. **Event Queue** (Lower Priority)  
   - Handles **Future.delayed()**, **I/O operations**, **Timers**, and **Streams**.  
   - Runs **after microtasks are completed**.  

---

## **🛠 Example: Understanding the Event Loop**
```dart
import 'dart:async';

void main() {
  print("1️⃣ Start");

  Future(() => print("3️⃣ Future task")); // Added to event queue

  scheduleMicrotask(() => print("2️⃣ Microtask")); // Added to microtask queue

  Future.delayed(Duration(seconds: 1), () => print("5️⃣ Delayed Future")); // Delayed event

  print("4️⃣ End");
}
```
### **📝 Output Order:**
```
1️⃣ Start
4️⃣ End
2️⃣ Microtask       // (Microtask runs first)
3️⃣ Future task     // (Event queue executes next)
5️⃣ Delayed Future  // (Executes after 1 second)
```

✔ **Synchronous code executes first**  
✔ **Microtasks (`scheduleMicrotask`) run before event queue tasks**  
✔ **Event queue tasks execute after microtasks finish**  
✔ **Delayed Futures (`Future.delayed()`) run after their delay**  

---

## **🛠 Example: Chained Futures Execution in the Event Loop**
```dart
void main() {
  print("1️⃣ Start");

  Future(() => print("3️⃣ Future task"))
      .then((_) => print("4️⃣ Then task"))
      .then((_) => Future(() => print("5️⃣ Nested Future task")))
      .then((_) => print("6️⃣ After nested future"));

  print("2️⃣ End");
}
```
### **📝 Output:**
```
1️⃣ Start
2️⃣ End
3️⃣ Future task
4️⃣ Then task
5️⃣ Nested Future task
6️⃣ After nested future
```
✔ **Futures execute after synchronous code**  
✔ **`then()` executes when the previous Future completes**  

---

## **🚀 Key Takeaways About the Event Loop**
✅ **Dart is single-threaded but non-blocking.**  
✅ **Microtasks execute before event queue tasks.**  
✅ **Future-based tasks run in the event queue.**  
✅ **Delays (`Future.delayed`) wait before execution.**  
