# Explain PageView Widget in Flutter

The `PageView` widget in Flutter is a scrollable list that works page by page—similar to how onboarding screens, carousels, or tab views behave. It allows horizontal (or vertical) swiping between child widgets, and each child occupies the entire viewport (one full "page" at a time).

---

### 🔹 Basic Syntax

```dart
PageView(
  children: [
    Container(color: Colors.red),
    Container(color: Colors.green),
    Container(color: Colors.blue),
  ],
)
```

---

### 🔹 Key Properties

| Property          | Description                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------- |
| `children`        | List of widgets to display as pages.                                                           |
| `scrollDirection` | Axis of scroll – `Axis.horizontal` (default) or `Axis.vertical`.                               |
| `controller`      | A `PageController` to control the view programmatically.                                       |
| `onPageChanged`   | Callback triggered when the user swipes to a new page.                                         |
| `physics`         | Determines scroll behavior, like `BouncingScrollPhysics`, `NeverScrollableScrollPhysics`, etc. |
| `pageSnapping`    | If `true` (default), snaps to pages instead of stopping mid-scroll.                            |

---

### 🔹 Example with `PageController`

```dart
PageController _controller = PageController(initialPage: 0);

PageView(
  controller: _controller,
  onPageChanged: (index) {
    print('Current Page: $index');
  },
  children: [
    Center(child: Text('Page 1')),
    Center(child: Text('Page 2')),
    Center(child: Text('Page 3')),
  ],
)
```

You can use `_controller.jumpToPage(index)` or `_controller.animateToPage(index, ...)` to switch pages programmatically.

---

### 🔹 When to Use

* Onboarding screens
* Image carousels or galleries
* Step-based forms or surveys
* Custom tab navigation
