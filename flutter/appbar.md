# Explain Appbar widget in Flutter

The `AppBar` widget in Flutter is a **Material Design toolbar** that appears at the **top of the app screen**. It is used to display information such as:

- Title of the screen
- Navigation controls (back, drawer menu)
- Actions (search, settings, etc.)
- Tabs (`TabBar`)
- Custom widgets (like logos or avatars)

It's typically used inside a `Scaffold` widget, which provides the basic layout structure of a screen.

---

## 🔧 Constructor

```dart
AppBar({
  Key? key,
  this.leading,
  this.automaticallyImplyLeading = true,
  this.title,
  this.actions,
  this.flexibleSpace,
  this.bottom,
  this.elevation,
  this.shadowColor,
  this.shape,
  this.backgroundColor,
  this.foregroundColor,
  this.brightness,
  this.iconTheme,
  this.actionsIconTheme,
  this.textTheme,
  this.centerTitle,
  this.titleSpacing,
  this.toolbarHeight,
  this.toolbarOpacity = 1.0,
  this.bottomOpacity = 1.0,
})
```

---

## 📌 Common Properties Explained

| Property               | Description |
|------------------------|-------------|
| `title`                | The main widget in the AppBar, usually a `Text`. |
| `centerTitle`          | Center-aligns the title (useful for iOS look). |
| `leading`              | Widget at the start of the AppBar (menu, back button, etc.). |
| `automaticallyImplyLeading` | If true, shows a back button automatically. |
| `actions`              | A list of widgets (usually `IconButton`s) shown at the end (right side). |
| `backgroundColor`      | The background color of the AppBar. |
| `elevation`            | The shadow beneath the AppBar. |
| `bottom`               | Widget displayed below the AppBar (often `TabBar`). |
| `flexibleSpace`        | A widget behind the title/leading/actions (useful for gradients, images). |
| `toolbarHeight`        | Height of the AppBar. |
| `shape`                | Gives shape to the AppBar like rounded corners. |

---

## ✅ Example: Simple AppBar

```dart
Scaffold(
  appBar: AppBar(
    title: Text('Home Page'),
    centerTitle: true,
    backgroundColor: Colors.deepPurple,
    elevation: 4.0,
    leading: Icon(Icons.menu),
    actions: [
      IconButton(
        icon: Icon(Icons.search),
        onPressed: () {
          print('Search tapped!');
        },
      ),
      IconButton(
        icon: Icon(Icons.notifications),
        onPressed: () {
          print('Notifications tapped!');
        },
      ),
    ],
  ),
  body: Center(child: Text('Hello, World!')),
)
```

---

## ✨ Advanced Uses

### 1. **AppBar with TabBar**

```dart
DefaultTabController(
  length: 3,
  child: Scaffold(
    appBar: AppBar(
      title: Text('Tabs Demo'),
      bottom: TabBar(
        tabs: [
          Tab(icon: Icon(Icons.home)),
          Tab(icon: Icon(Icons.star)),
          Tab(icon: Icon(Icons.person)),
        ],
      ),
    ),
    body: TabBarView(
      children: [
        Center(child: Text('Home')),
        Center(child: Text('Favorites')),
        Center(child: Text('Profile')),
      ],
    ),
  ),
);
```

### 2. **AppBar with FlexibleSpace (e.g., background image)**

```dart
AppBar(
  title: Text('Flexible AppBar'),
  flexibleSpace: Container(
    decoration: BoxDecoration(
      gradient: LinearGradient(
        colors: [Colors.purple, Colors.blue],
        begin: Alignment.topLeft,
        end: Alignment.bottomRight,
      ),
    ),
  ),
)
```

---

## 🔄 Alternatives and Customizations

### 1. **Custom Height AppBar**

```dart
PreferredSize(
  preferredSize: Size.fromHeight(100),
  child: AppBar(
    title: Text('Custom Height'),
  ),
)
```

### 2. **SliverAppBar (Scrollable with body)**

Used inside a `CustomScrollView`.

```dart
SliverAppBar(
  floating: true,
  pinned: true,
  expandedHeight: 200.0,
  flexibleSpace: FlexibleSpaceBar(
    title: Text('Sliver AppBar'),
    background: Image.asset('assets/banner.jpg', fit: BoxFit.cover),
  ),
),
```

---

## 🧠 Summary

| Use Case                     | AppBar Feature                      |
|-----------------------------|-------------------------------------|
| Basic top bar               | `AppBar` with `title`, `actions`    |
| Back navigation             | `leading` or auto via `Navigator`   |
| Tabbed interface            | Use `bottom` with `TabBar`          |
| Fancy visuals or animation  | Use `flexibleSpace` or `SliverAppBar` |
| Custom height               | Wrap in `PreferredSize`             |

---
