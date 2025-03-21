# What are Stateful and stateless widgets in Flutter ?

In Flutter, **widgets** are the building blocks of the UI. They are broadly divided into two types:

1. **StatelessWidget** – Used for static content (doesn't change over time).  
2. **StatefulWidget** – Used for dynamic content (can change over time based on user interaction or state changes).  

---

## 🚀 **StatelessWidget**
- A widget that **doesn't require mutable state**.  
- Once created, it cannot change its properties or appearance.  
- If you want to change the widget’s state, you need to recreate it.  

---

### ✅ **Example: StatelessWidget**
```dart
class MyStatelessWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Stateless Example')),
      body: Center(
        child: Text('This is a StatelessWidget'),
      ),
    );
  }
}
```

### 🔎 **Explanation:**
- `MyStatelessWidget` is created once.  
- If any value changes, the widget **cannot reflect it** unless rebuilt.  
- Good for **static** content like text, images, or icons.  

---

### 🚀 **Use Cases of StatelessWidget**
✅ Displaying static data  
✅ Showing icons, static text, or images  
✅ Layouts that do not depend on user interaction or state  

---

## 🚀 **StatefulWidget**
- A widget that **can hold mutable state**.  
- Uses a `State` object to track changes and rebuild the UI when the state changes.  
- If the state changes, Flutter automatically calls `setState()` to rebuild the widget.  

---

### ✅ **Example: StatefulWidget**
```dart
class MyStatefulWidget extends StatefulWidget {
  @override
  State<MyStatefulWidget> createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Stateful Example')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Counter: $_counter'),
            ElevatedButton(
              onPressed: _incrementCounter,
              child: Text('Increment'),
            ),
          ],
        ),
      ),
    );
  }
}
```

### 🔎 **Explanation:**
- `_counter` is stored in the `State` object (`_MyStatefulWidgetState`).  
- When `_incrementCounter()` is called, `setState()` updates the state and **rebuilds the widget**.  
- The updated value of `_counter` is shown in the `Text` widget.  

---

### 🚀 **Use Cases of StatefulWidget**
✅ Managing user input  
✅ Interactive UI components (e.g., buttons, sliders)  
✅ Real-time updates (e.g., counters, timers)  
✅ Handling dynamic themes or locale changes  

---

## 🚀 **Key Differences**
| Feature | StatelessWidget | StatefulWidget |
|---------|-----------------|----------------|
| **State** | Immutable (cannot change) | Mutable (can change) |
| **Performance** | High (since no state handling) | Slightly lower (due to state tracking) |
| **Rebuild Trigger** | Rebuilds only if parent rebuilds | Rebuilds when `setState()` is called |
| **Use Cases** | Static content | Dynamic content |
| **Constructor Called** | When created | When created |
| **Build Method Called** | When widget is created | When `setState()` is called |

---

## 🚀 **When to Use Stateful vs Stateless**
✅ Use **StatelessWidget** when the widget’s state **does not change** during its lifecycle.  
✅ Use **StatefulWidget** when the widget’s state **needs to change** based on user interaction or external factors.  

---

## 🚀 **Example to Compare Stateless vs Stateful**
### ✅ Stateless Example:
```dart
class StaticText extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text('This is static text');
  }
}
```

### ✅ Stateful Example:
```dart
class DynamicText extends StatefulWidget {
  @override
  State<DynamicText> createState() => _DynamicTextState();
}

class _DynamicTextState extends State<DynamicText> {
  String text = 'Initial text';

  void updateText() {
    setState(() {
      text = 'Updated text';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text(text),
        ElevatedButton(
          onPressed: updateText,
          child: Text('Update Text'),
        ),
      ],
    );
  }
}
```

---

## 🚀 **Lifecycle of StatefulWidget**
1. **createState()** → Creates the `State` object.  
2. **initState()** → Called once when the widget is inserted into the tree.  
3. **build()** → Called every time the widget is rebuilt.  
4. **setState()** → Triggers a rebuild by calling `build()`.  
5. **dispose()** → Called when the widget is removed from the tree.  

---

### ✅ **Lifecycle Example:**
```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  void initState() {
    super.initState();
    print('initState called');
  }

  @override
  void dispose() {
    print('dispose called');
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    print('build called');
    return Text('Hello');
  }
}
```

### 🔎 **Output:**
```
initState called
build called
dispose called
```

---

## 🚀 **Best Practices**
✅ Use `StatelessWidget` whenever possible for better performance.  
✅ Use `StatefulWidget` only if the state **needs to change**.  
✅ Keep state management logic in the `State` object, not the widget itself.  
✅ Use `const` constructors for `StatelessWidget` to improve performance by reducing rebuilds.  

---

## 🎯 **Summary**
| Aspect | StatelessWidget | StatefulWidget |
|--------|-----------------|----------------|
| **State** | Immutable | Mutable |
| **Performance** | High | Slightly lower |
| **Rebuild** | On parent rebuild | On `setState()` |
| **Lifecycle** | Create → Build → Done | Create → Build → SetState → Dispose |
| **Use Cases** | Static content, text, icons | Interactive content, animation, data updates |

---

**🔥 Quick Rule:**  
➡️ If the widget depends on **data that doesn’t change**, use `StatelessWidget`.  
➡️ If the widget depends on **data that changes over time**, use `StatefulWidget`.  
