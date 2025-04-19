# Explain ThemeData in Flutter

The `ThemeData` class in Flutter is a core part of Flutter’s **themability system**. It lets you define the look and feel of your entire app — including colors, typography, button styles, icon themes, and more — in one place.

---

### 🔹 What is `ThemeData`?

It's a class that holds **theme configuration**. You pass it to your `MaterialApp` to apply a consistent style throughout the app.

```dart
MaterialApp(
  title: 'MyApp',
  theme: ThemeData(
    primarySwatch: Colors.blue,
    brightness: Brightness.light,
    textTheme: TextTheme(
      bodyLarge: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
    ),
  ),
  home: MyHomePage(),
)
```

---

### 🔸 Commonly Used Properties

| Property            | Description                                  |
|---------------------|----------------------------------------------|
| `primaryColor`      | Main color of the app                        |
| `primarySwatch`     | Material color palette (shades of one color) |
| `brightness`        | Light or dark theme                          |
| `accentColor`       | Secondary color (Deprecated: use `colorScheme.secondary`) |
| `textTheme`         | Styles for text (headlines, body, etc.)      |
| `appBarTheme`       | Custom AppBar style                          |
| `iconTheme`         | Icon styling                                 |
| `buttonTheme`       | Legacy button styles                         |
| `colorScheme`       | Defines full color system for your theme     |
| `cardTheme`         | Theme for `Card` widgets                     |
| `inputDecorationTheme` | Styling for `TextField` and `InputDecorator` |

---

### 🔹 Dark Theme

You can specify both `theme` and `darkTheme`:

```dart
MaterialApp(
  theme: ThemeData.light(),
  darkTheme: ThemeData.dark(),
  themeMode: ThemeMode.system, // light/dark based on system setting
)
```

---

### 🔸 Accessing ThemeData in Widgets

You can access the current theme anywhere in your widget tree using:

```dart
Theme.of(context).primaryColor
TextStyle? style = Theme.of(context).textTheme.bodyLarge
```

---

### 🔹 Custom Theme Example

```dart
final ThemeData customTheme = ThemeData(
  colorScheme: ColorScheme.fromSeed(seedColor: Colors.teal),
  textTheme: GoogleFonts.latoTextTheme(),
  elevatedButtonTheme: ElevatedButtonThemeData(
    style: ElevatedButton.styleFrom(
      backgroundColor: Colors.teal,
      foregroundColor: Colors.white,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
    ),
  ),
);
```

---
