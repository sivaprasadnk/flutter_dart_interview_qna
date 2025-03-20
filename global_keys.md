# What are Global Keys ?

In Flutter, **GlobalKeys** are used to uniquely identify widgets across the entire widget tree, not just within a specific parent. They allow widgets to:

✅ Access the state of a widget from anywhere in the app.  
✅ Trigger rebuilds or updates on widgets from outside their scope.  
✅ Maintain widget state even when the widget tree changes.  

---

## 🏷️ **How GlobalKey Works**
A `GlobalKey` keeps a reference to the widget, its state, and the `BuildContext` even when the widget tree rebuilds.

### 📌 **Common Use Cases:**
- Accessing or modifying the state of a widget.  
- Retrieving `BuildContext` for showing snackbars or dialogs.  
- Maintaining widget state when reordering or rebuilding the widget tree.  
- Working with `Navigator`, `Form`, `Scaffold`, etc.  

---

## 🚀 **Types of GlobalKeys**
### 1. **GlobalKey<FormState>** – Access form state  
### 2. **GlobalKey<ScaffoldState>** – Access scaffold state  
### 3. **GlobalKey<CustomWidgetState>** – Access custom widget state  

---

## 📝 **Examples**
### 1. **GlobalKey with Form**
You can use `GlobalKey<FormState>` to validate or reset a form from outside the form itself.

### **Example:**
```dart
class MyForm extends StatelessWidget {
  final _formKey = GlobalKey<FormState>();

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        children: [
          TextFormField(
            validator: (value) {
              if (value == null || value.isEmpty) {
                return 'Please enter text';
              }
              return null;
            },
          ),
          ElevatedButton(
            onPressed: () {
              if (_formKey.currentState!.validate()) {
                print('Form is valid');
              }
            },
            child: Text('Submit'),
          ),
        ],
      ),
    );
  }
}
```

🔎 **How It Works:**  
- `_formKey.currentState!.validate()` validates the form using the key.  
- `_formKey.currentState!.reset()` can reset the form state.  

---

### 2. **GlobalKey with Scaffold (Showing Snackbar)**
You can use `GlobalKey<ScaffoldState>` to show a snackbar from outside the `Scaffold`.

### **Example:**
```dart
class MyHomePage extends StatelessWidget {
  final _scaffoldKey = GlobalKey<ScaffoldState>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldKey,
      appBar: AppBar(title: Text('GlobalKey Example')),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            _scaffoldKey.currentState!.showSnackBar(
              SnackBar(content: Text('This is a snackbar!')),
            );
          },
          child: Text('Show Snackbar'),
        ),
      ),
    );
  }
}
```

🔎 **How It Works:**  
- `_scaffoldKey.currentState!.showSnackBar()` allows you to trigger the snackbar from outside the `Scaffold`’s `BuildContext`.

---

### 3. **GlobalKey with Custom StatefulWidget**
You can use `GlobalKey<CustomWidgetState>` to access and modify the state of a custom widget.

### **Example:**
```dart
class CounterWidget extends StatefulWidget {
  @override
  CounterWidgetState createState() => CounterWidgetState();
}

class CounterWidgetState extends State<CounterWidget> {
  int _count = 0;

  void incrementCounter() {
    setState(() {
      _count++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Text('Count: $_count');
  }
}

class MyHomePage extends StatelessWidget {
  final GlobalKey<CounterWidgetState> _counterKey = GlobalKey<CounterWidgetState>();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('GlobalKey Example')),
      body: Column(
        children: [
          CounterWidget(key: _counterKey),
          ElevatedButton(
            onPressed: () {
              _counterKey.currentState?.incrementCounter();
            },
            child: Text('Increment Counter'),
          ),
        ],
      ),
    );
  }
}
```

🔎 **How It Works:**  
- `GlobalKey<CounterWidgetState>` gives access to the `CounterWidgetState`.  
- `_counterKey.currentState?.incrementCounter()` updates the widget state directly.  

---

## 🎯 **Why Use GlobalKey?**
1. **Direct State Access:** Helps access a widget’s state from outside its tree.  
2. **Reusability:** Preserves widget state even when the widget tree is rebuilt.  
3. **Performance:** Prevents unnecessary rebuilds by preserving state.  

---

## 🚨 **Best Practices**
✅ Use `GlobalKey` when you **must access widget state** directly.  
✅ Use `ValueKey` or `ObjectKey` for **list items** instead of `GlobalKey` for better performance.  
✅ Avoid creating multiple `GlobalKeys` unless necessary — they are expensive in terms of performance.  
✅ For state management, prefer **Provider** or **BLoC** over `GlobalKey` where possible.  

---

## 🆚 **LocalKey vs GlobalKey**
| Feature | LocalKey | GlobalKey |
|---------|----------|-----------|
| Scope | Limited to the widget tree where it's defined | Accessible across the entire app |
| State Access | Cannot access state directly | Can access widget state directly |
| Example | `ValueKey`, `ObjectKey`, `UniqueKey` | `GlobalKey<FormState>`, `GlobalKey<ScaffoldState>` |
| Use Case | Preserving widget identity in lists | Accessing state, showing snackbar, handling form state |

---

## 🚀 **Summary**
| Key Type | Use Case |
|----------|----------|
| **ValueKey** | Track widgets by a specific value (e.g., string or int) |
| **ObjectKey** | Track widgets by object reference |
| **UniqueKey** | Force rebuild every time |
| **GlobalKey<FormState>** | Access form state |
| **GlobalKey<ScaffoldState>** | Show snackbar or drawer |
| **GlobalKey<CustomWidgetState>** | Access custom widget state |
