# What is MediaQuery in Flutter ?

In Flutter, **MediaQuery** provides information about the **device's screen size**, **orientation**, **padding**, **safe area**, **text scaling**, and **device-specific dimensions**.

---

## 🚀 **What is MediaQuery?**
- A widget that **inherits** device-specific properties from the **widget tree**.  
- It allows you to adapt the UI to **different screen sizes** and **orientations** dynamically.  
- You can access `MediaQuery` using `MediaQuery.of(context)`.  

---
s
## ✅ **Example:**
```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var size = MediaQuery.of(context).size; // Get screen size

    return Container(
      width: size.width * 0.8,
      height: size.height * 0.3,
      color: Colors.blue,
      child: Center(
        child: Text(
          'Width: ${size.width}, Height: ${size.height}',
          style: TextStyle(color: Colors.white),
          textAlign: TextAlign.center,
        ),
      ),
    );
  }
}
```

### 🔎 **Explanation:**
- `MediaQuery.of(context).size` → Returns the screen's **width** and **height**.  
- The `Container` size is defined as a **percentage** of the screen size.  

---

## 🚀 **Common Properties of MediaQuery**
| Property | Type | Description | Example |
|----------|------|-------------|---------|
| **size** | `Size` | Total screen width and height | `MediaQuery.of(context).size.width` |
| **orientation** | `Orientation` | Current screen orientation | `Orientation.portrait` |
| **padding** | `EdgeInsets` | Safe area padding (top, bottom, left, right) | `MediaQuery.of(context).padding.top` |
| **viewInsets** | `EdgeInsets` | Area where the keyboard or system overlays appear | `MediaQuery.of(context).viewInsets.bottom` |
| **devicePixelRatio** | `double` | Ratio of device pixels to logical pixels | `MediaQuery.of(context).devicePixelRatio` |
| **textScaleFactor** | `double` | Current text scaling (based on user settings) | `MediaQuery.of(context).textScaleFactor` |
| **viewPadding** | `EdgeInsets` | Total padding including areas under status and navigation bars | `MediaQuery.of(context).viewPadding.top` |

---

## 🚀 **1. Getting Screen Size**
You can get the **width** and **height** of the screen like this:

```dart
var size = MediaQuery.of(context).size;
double width = size.width;
double height = size.height;
```

### ✅ **Example:**
```dart
Container(
  width: MediaQuery.of(context).size.width * 0.8, // 80% of screen width
  height: MediaQuery.of(context).size.height * 0.3, // 30% of screen height
  color: Colors.blue,
);
```

---

## 🚀 **2. Detecting Orientation**
You can check if the device is in **portrait** or **landscape** mode using `orientation`.

```dart
var orientation = MediaQuery.of(context).orientation;
if (orientation == Orientation.portrait) {
  print('Portrait Mode');
} else {
  print('Landscape Mode');
}
```

### ✅ **Example:**
```dart
@override
Widget build(BuildContext context) {
  return MediaQuery.of(context).orientation == Orientation.portrait
      ? Text('Portrait Mode')
      : Text('Landscape Mode');
}
```

---

## 🚀 **3. Handling Safe Area (Notch, Status Bar, Navigation Bar)**
Use `MediaQuery.of(context).padding` to get safe area values.

### ✅ **Example:**
```dart
@override
Widget build(BuildContext context) {
  return Padding(
    padding: EdgeInsets.only(top: MediaQuery.of(context).padding.top),
    child: Text('Safe Area Example'),
  );
}
```

### 🔎 **Explanation:**
- `padding.top` → Top safe area (for notch or status bar).  
- `padding.bottom` → Bottom safe area (for navigation bar).  

---

## 🚀 **4. Handling Keyboard/Overlays Using `viewInsets`**
Use `viewInsets.bottom` to adjust for the keyboard height.

### ✅ **Example:**
```dart
Padding(
  padding: EdgeInsets.only(bottom: MediaQuery.of(context).viewInsets.bottom),
  child: TextField(),
)
```

### 🔎 **Explanation:**
- `viewInsets.bottom` returns the height of the on-screen keyboard.  
- Helps avoid overlapping widgets with the keyboard.  

---

## 🚀 **5. Handling Text Scaling**
Use `textScaleFactor` to adjust text size based on user settings.

### ✅ **Example:**
```dart
Text(
  'Hello Flutter!',
  style: TextStyle(fontSize: 16 * MediaQuery.of(context).textScaleFactor),
)
```

### 🔎 **Explanation:**
- `textScaleFactor = 1.0` → Default text size  
- `textScaleFactor = 1.5` → 50% larger text size  
- Helps create **accessible** UIs.  

---

## 🚀 **6. Handling High-Resolution Devices**
Use `devicePixelRatio` for pixel-perfect rendering on high-DPI screens.

### ✅ **Example:**
```dart
double pixelRatio = MediaQuery.of(context).devicePixelRatio;
print('Pixel Ratio: $pixelRatio');
```

### 🔎 **Example Output:**
- `1.0` → Normal screen  
- `2.0` → Retina/HD screen  
- `3.0` → High-density screen  

---

## 🚀 **7. MediaQuery Inside Builder**
You can use `LayoutBuilder` or `MediaQuery` to get dynamic screen sizes.

### ✅ **Example with `LayoutBuilder`:**
```dart
LayoutBuilder(
  builder: (context, constraints) {
    return Container(
      width: constraints.maxWidth * 0.8,
      height: constraints.maxHeight * 0.3,
      color: Colors.blue,
    );
  },
);
```

### 🔎 **Difference:**
| Approach | Use Case |
|----------|----------|
| `MediaQuery` | For device-level properties (size, orientation, safe area) |
| `LayoutBuilder` | For widget-level properties (constraints of parent widget) |

---

## 🚀 **8. Example: Responsive UI Using MediaQuery**
```dart
class ResponsiveWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double width = MediaQuery.of(context).size.width;
    
    return Scaffold(
      appBar: AppBar(title: Text('Responsive Example')),
      body: Center(
        child: width > 600
            ? Text('Tablet Layout', style: TextStyle(fontSize: 24))
            : Text('Mobile Layout', style: TextStyle(fontSize: 18)),
      ),
    );
  }
}
```

### 🔎 **Explanation:**
- If the screen width is greater than `600dp`, it shows a **tablet layout**.  
- Otherwise, it shows a **mobile layout**.  

---

## 🔥 **Common Mistakes with MediaQuery**
| Mistake | Issue | Solution |
|---------|-------|----------|
| Using `MediaQuery.of(context)` in `initState()` | Context not available yet | Use `addPostFrameCallback()` |
| Overlapping with the keyboard | Input hidden by keyboard | Use `viewInsets.bottom` to adjust |
| Ignoring safe area | Content under notch or navigation bar | Use `padding` for adjustment |

---

## 🎯 **Summary**
| Property | Description | Example |
|----------|-------------|---------|
| **size** | Screen size | `MediaQuery.of(context).size.width` |
| **orientation** | Portrait/Landscape mode | `MediaQuery.of(context).orientation` |
| **padding** | Safe area padding | `MediaQuery.of(context).padding.top` |
| **viewInsets** | Overlay (like keyboard) size | `MediaQuery.of(context).viewInsets.bottom` |
| **devicePixelRatio** | Device pixel density | `MediaQuery.of(context).devicePixelRatio` |
| **textScaleFactor** | User text scaling factor | `MediaQuery.of(context).textScaleFactor` |

---

## ✅ **Best Practices**
✅ Use `MediaQuery` for screen size and orientation-based layouts.  
✅ Use `safe area padding` to handle notches and system UI.  
✅ Use `LayoutBuilder` for responsive widget constraints.  
✅ Use `textScaleFactor` for scalable text sizes.  
