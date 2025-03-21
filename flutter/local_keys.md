# What are local keys? What are its types ?

In Flutter, **local keys** are used to uniquely identify widgets within the widget tree. They help Flutter understand which widgets should be preserved and updated rather than rebuilt when the widget tree changes.

## 🏷️ **Types of Local Keys**
Flutter provides three main types of local keys:

### 1. **ValueKey**
- A `ValueKey` is based on a specific value (like a string or integer).  
- Useful when you need to distinguish widgets based on a fixed value.

### **Example:**
```dart
List<String> items = ['Apple', 'Banana', 'Orange'];

ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return ListTile(
      key: ValueKey(items[index]), // Uses the string value as a key
      title: Text(items[index]),
    );
  },
);
```

🔎 **How It Works:**
- Flutter will compare the `ValueKey` values when the list changes.
- If the value matches an existing key, Flutter will preserve the widget state instead of rebuilding it.

---

### 2. **ObjectKey**
- Similar to `ValueKey`, but works with objects instead of primitive values.  
- Useful when the object might change but still represents the same logical entity.

### **Example:**
```dart
class Person {
  final String name;
  Person(this.name);
}

List<Person> persons = [Person('John'), Person('Doe')];

ListView.builder(
  itemCount: persons.length,
  itemBuilder: (context, index) {
    return ListTile(
      key: ObjectKey(persons[index]), // Uses the object reference as a key
      title: Text(persons[index].name),
    );
  },
);
```

🔎 **How It Works:**
- If the object reference remains the same, Flutter will preserve the widget.
- If the object changes, Flutter will rebuild the widget.

---

### 3. **UniqueKey**
- A `UniqueKey` generates a random key that’s always unique.  
- Forces Flutter to treat a widget as a new widget every time, even if it logically represents the same data.  
- Useful for dynamic content where preserving state is not required.

### **Example:**
```dart
List<String> items = ['Apple', 'Banana', 'Orange'];

ListView.builder(
  itemCount: items.length,
  itemBuilder: (context, index) {
    return ListTile(
      key: UniqueKey(), // Generates a new key each time
      title: Text(items[index]),
    );
  },
);
```

🔎 **How It Works:**
- Flutter will **always rebuild** the widget because the key is different every time.

---

## 🆚 **When to Use Which Key**
| Key Type | Use Case | Example | Preserves State? |
|----------|----------|---------|------------------|
| **ValueKey** | When you need to track items by a unique value | `ValueKey('Apple')` | ✅ Yes |
| **ObjectKey** | When you need to track items by object identity | `ObjectKey(Person('John'))` | ✅ Yes |
| **UniqueKey** | When you want to force Flutter to treat the widget as new | `UniqueKey()` | ❌ No |

---

## 🌟 **Example: Updating List with Keys**
Here's an example showing how `ValueKey` helps preserve state when the list order changes:

```dart
class MyHomePage extends StatefulWidget {
  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  List<String> items = ['Apple', 'Banana', 'Orange'];

  void shuffleItems() {
    setState(() {
      items.shuffle();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Local Keys Example')),
      body: ReorderableListView(
        onReorder: (oldIndex, newIndex) {
          if (newIndex > oldIndex) newIndex--;
          setState(() {
            final item = items.removeAt(oldIndex);
            items.insert(newIndex, item);
          });
        },
        children: [
          for (var item in items)
            ListTile(
              key: ValueKey(item), // Preserve state while reordering
              title: Text(item),
            ),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: shuffleItems,
        child: Icon(Icons.shuffle),
      ),
    );
  }
}
```

### ✅ **What Happens:**
- If you use `ValueKey`, the state of each `ListTile` will be preserved when reordering or shuffling.  
- If you use `UniqueKey`, the state will be lost because Flutter treats them as different widgets every time.

---

## 🚀 **Best Practices**
✅ Use **ValueKey** when the value is stable and unique.  
✅ Use **ObjectKey** when you need to track object identity.  
✅ Use **UniqueKey** when you want Flutter to rebuild a widget every time.  
✅ Prefer keys when working with **lists**, **reorderable lists**, and **stateful widgets** to improve performance.  
