# Explain GridViewBuilder in Flutter

`GridView.builder` in Flutter is a constructor for creating a scrollable, 2D array of widgets that are built on demand (lazy loading), similar to `ListView.builder`. It’s highly efficient when you have a large number of items to display in a grid format because only the visible widgets are created.

---

### 📌 Syntax:

```dart
GridView.builder({
  required SliverGridDelegate gridDelegate,
  required IndexedWidgetBuilder itemBuilder,
  int itemCount,
  ScrollPhysics? physics,
  bool shrinkWrap = false,
  EdgeInsetsGeometry? padding,
})
```

---

### 🧱 Key Parameters:

* **`gridDelegate`**: Defines how the grid should be laid out. Use `SliverGridDelegateWithFixedCrossAxisCount` or `SliverGridDelegateWithMaxCrossAxisExtent`.
* **`itemBuilder`**: A function that builds each item in the grid based on its index.
* **`itemCount`**: Total number of items in the grid.
* **`shrinkWrap`**: Whether the grid should take only as much space as it needs (typically `true` when nested).
* **`physics`**: Controls the scrolling behavior.

---

### 🧩 Example: Grid of Images

```dart
GridView.builder(
  itemCount: 20,
  gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 2, // 2 items per row
    crossAxisSpacing: 10,
    mainAxisSpacing: 10,
  ),
  itemBuilder: (context, index) {
    return Container(
      color: Colors.blue,
      child: Center(
        child: Text('Item $index'),
      ),
    );
  },
)
```

---

### 🛠 When to Use:

* When you want a grid layout that dynamically builds widgets on scroll.
* When optimizing performance for long lists of grid items.
