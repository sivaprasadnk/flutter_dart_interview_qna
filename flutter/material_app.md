# Explain MaterialApp in Flutter

The `MaterialApp` widget in Flutter is the **entry point** for any material design-based app. It sets up things like navigation, themes, and localization—basically, it's the **root of your app** and gives access to many core features provided by the material design library.

---

### ✅ Basic Example

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My First Flutter App',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Home')),
      body: Center(child: Text('Welcome to Flutter!')),
    );
  }
}
```

---

### 🧠 Key Properties of `MaterialApp`

| Property            | Description |
|---------------------|-------------|
| `home`              | The default screen of the app. |
| `routes`            | A map of route names to widget builders. Used for named navigation. |
| `initialRoute`      | The first route to load (use with `routes`). |
| `navigatorKey`      | A global key for controlling navigation. |
| `theme`             | App-wide styling (colors, fonts, etc.). |
| `darkTheme`         | Theme for dark mode. |
| `themeMode`         | Controls whether to use light/dark theme. |
| `title`             | The app title shown in task switcher. |
| `debugShowCheckedModeBanner` | Hides the debug banner in development. |

---

### 🧭 Navigation Example using Routes

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomePage(),
    '/about': (context) => AboutPage(),
  },
);
```

Then to navigate:

```dart
Navigator.pushNamed(context, '/about');
```
