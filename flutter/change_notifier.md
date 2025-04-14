# Explain Change Notifier in Flutter

`ChangeNotifier` in Flutter is part of the `flutter/foundation` package and is commonly used for state management, especially with `Provider`.

It works by notifying its listeners (typically widgets) when there's a change in its internal state, so they can rebuild accordingly.

---

### 🔹 Use Case
You’d use `ChangeNotifier` when:
- You want to manage and update state in your app.
- You want to notify multiple widgets when a value changes.
- You're using the `Provider` package.

---

### 🔧 Example

#### 1. Create a `ChangeNotifier` class:

```dart
import 'package:flutter/foundation.dart';

class CounterProvider extends ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners(); // Notifies listeners of the change
  }
}
```

---

#### 2. Provide it using `ChangeNotifierProvider`:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (_) => CounterProvider(),
      child: MyApp(),
    ),
  );
}
```

---

#### 3. Consume it in the widget tree:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: CounterScreen(),
    );
  }
}

class CounterScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final counterProvider = Provider.of<CounterProvider>(context);

    return Scaffold(
      appBar: AppBar(title: Text("ChangeNotifier Example")),
      body: Center(
        child: Text(
          'Count: ${counterProvider.count}',
          style: TextStyle(fontSize: 24),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: counterProvider.increment,
        child: Icon(Icons.add),
      ),
    );
  }
}
```

---

### 🔁 Alternatives
If your app grows more complex, consider:
- `Riverpod`
- `BLoC`
- `Redux`
- `GetX`
- `Cubit`
