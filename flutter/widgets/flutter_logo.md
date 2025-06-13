# What is FlutterLogo widget in Flutter?

The `FlutterLogo` widget in Flutter is a built-in widget that displays the Flutter logo. It’s typically used for branding, splash screens, or placeholder UIs.

### 🔧 Syntax:

```dart
FlutterLogo({
  Key? key,
  double size = 24.0,
  FlutterLogoStyle style = FlutterLogoStyle.markOnly,
  Color? textColor,
  Duration duration = const Duration(milliseconds: 200),
  Curve curve = Curves.fastOutSlowIn,
})
```

### 🧩 Parameters:

* `size`: Size of the logo.
* `style`: The style of the logo. Options include:

  * `FlutterLogoStyle.markOnly`: Only the Flutter logo mark (default).
  * `FlutterLogoStyle.horizontal`: Logo with text in a horizontal layout.
  * `FlutterLogoStyle.stacked`: Logo with text stacked below the icon.
* `textColor`: Color of the "Flutter" text (only used if style includes text).
* `duration` & `curve`: For animating changes in the logo.

### 🔍 Example:

```dart
Center(
  child: FlutterLogo(
    size: 100,
    style: FlutterLogoStyle.horizontal,
    textColor: Colors.blue,
  ),
)
```

This displays the horizontal Flutter logo with the text colored blue.
