# What are widget lifecycle methods in Flutter ?

Flutter widgets, especially **StatefulWidgets**, go through a specific lifecycle from creation to destruction. Understanding the lifecycle helps in managing state, resources, and UI updates efficiently.

---

## 🌳 **Types of Widgets**  
1. **StatelessWidget** → No lifecycle (build is the only method).  
2. **StatefulWidget** → Has a state object with a complete lifecycle.  

### ➡️ **Stateless Widget Example:**  
```dart
class MyStatelessWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child: Text('Stateless Widget')),
    );
  }
}
```

> ✅ **Stateless widgets** only have a `build()` method. The UI is rebuilt only when the parent widget changes.

---

## 🌟 **Stateful Widget Lifecycle**  
For **Stateful Widgets**, the state object (`State<T>`) controls the lifecycle.  

### ➡️ **Complete Lifecycle Flow:**  
1. `createState()`  
2. `initState()`  
3. `didChangeDependencies()`  
4. `build()`  
5. `setState()`  
6. `deactivate()`  
7. `dispose()`  

---

## 🔎 **1. createState()**  
- Called when a `StatefulWidget` is created.  
- Creates the `State` object.  
- Only called **once**.  

### ✅ Example:  
```dart
@override
State<MyWidget> createState() => _MyWidgetState();
```

---

## 🔎 **2. initState()**  
- Called when the state is initialized.  
- Use it to initialize resources (e.g., controllers, subscriptions).  
- Called only **once** in the widget's lifetime.  

### ✅ Example:  
```dart
@override
void initState() {
  super.initState();
  print('initState');
}
```

> 💡 Ideal for setting up initial data, starting animations, or opening database connections.

---

## 🔎 **3. didChangeDependencies()**  
- Called after `initState()`.  
- Called when dependencies (like `InheritedWidget`) change.  
- Can be called multiple times during the lifecycle.  

### ✅ Example:  
```dart
@override
void didChangeDependencies() {
  super.didChangeDependencies();
  print('didChangeDependencies');
}
```

> 💡 Use it when the widget depends on `InheritedWidget` or `MediaQuery`.

---

## 🔎 **4. build()**  
- Called when the widget needs to be built or rebuilt.  
- Must return a widget tree.  
- Called after `initState()` and `setState()`.  

### ✅ Example:  
```dart
@override
Widget build(BuildContext context) {
  print('build');
  return Scaffold(
    body: Center(child: Text('Stateful Widget')),
  );
}
```

> 💡 Should be fast — avoid heavy processing.

---

## 🔎 **5. setState()**  
- Triggers a rebuild of the widget.  
- Called when the state changes.  

### ✅ Example:  
```dart
void updateState() {
  setState(() {
    // State changes here
  });
}
```

> 💡 Only rebuilds the affected widget — not the entire tree.

---

## 🔎 **6. deactivate()**  
- Called when the widget is **removed** from the tree (temporarily).  
- Can be called multiple times if the widget is moved in the tree.  

### ✅ Example:  
```dart
@override
void deactivate() {
  print('deactivate');
  super.deactivate();
}
```

> 💡 Use it to release resources temporarily.

---

## 🔎 **7. dispose()**  
- Called when the widget is **permanently removed** from the tree.  
- Clean up resources (e.g., controllers, streams) here.  
- Called only **once**.  

### ✅ Example:  
```dart
@override
void dispose() {
  print('dispose');
  super.dispose();
}
```

> 💡 Ideal for closing database connections, stopping animations, or cancelling streams.

---

## 🔄 **🛠️ Complete Stateful Widget Example:**  
```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  void initState() {
    super.initState();
    print('initState');
  }

  @override
  void didChangeDependencies() {
    super.didChangeDependencies();
    print('didChangeDependencies');
  }

  @override
  Widget build(BuildContext context) {
    print('build');
    return Scaffold(
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            setState(() {
              print('setState');
            });
          },
          child: Text('Press Me'),
        ),
      ),
    );
  }

  @override
  void deactivate() {
    print('deactivate');
    super.deactivate();
  }

  @override
  void dispose() {
    print('dispose');
    super.dispose();
  }
}
```

---

## 🌲 **Lifecycle Flow**  
✅ `createState()` → ✅ `initState()` → ✅ `didChangeDependencies()` → ✅ `build()` →  
✅ `setState()` → ✅ `build()` → ✅ `deactivate()` → ✅ `dispose()`  

---

## 🏆 **Best Practices**  
✅ Initialize resources in `initState()`  
✅ Clean up resources in `dispose()`  
✅ Avoid heavy processing in `build()`  
✅ Use `setState()` carefully to avoid unnecessary rebuilds  
✅ Use `didChangeDependencies()` for inherited data updates  

---

## 🚀 **When Lifecycle Methods Are Called**  
| Method | When Called | Called Multiple Times? |
|--------|-------------|------------------------|
| **createState()** | When the widget is first created | ❌ No |
| **initState()** | When the state is initialized | ❌ No |
| **didChangeDependencies()** | When dependencies change | ✅ Yes |
| **build()** | When the widget is built or state changes | ✅ Yes |
| **setState()** | When state changes and UI needs updating | ✅ Yes |
| **deactivate()** | When the widget is removed temporarily | ✅ Yes |
| **dispose()** | When the widget is permanently destroyed | ❌ No |

---

## 🚀 **Summary**  
| **Stateless Widget** | **Stateful Widget** |
|---------------------|---------------------|
| Only has `build()` | Has a complete lifecycle |
| Cannot hold state | Can hold state |
| Immutable | Mutable |
| Fast and lightweight | Can be rebuilt based on state changes |