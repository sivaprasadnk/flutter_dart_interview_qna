# Explain Slider widget in Flutter

In Flutter, a **`Slider`** is a Material Design widget used to select a **value from a range** by moving a thumb (a circular button) along a horizontal line. It's commonly used for settings like volume, brightness, or anything that needs continuous numeric input.

---

### 🔧 Basic Slider Syntax

```dart
Slider(
  value: _currentSliderValue,
  min: 0,
  max: 100,
  divisions: 10,
  label: _currentSliderValue.round().toString(),
  onChanged: (double value) {
    setState(() {
      _currentSliderValue = value;
    });
  },
)
```

---

### 🧠 Key Properties

| Property        | Description                                                            |
| --------------- | ---------------------------------------------------------------------- |
| `value`         | Current position of the slider (double).                               |
| `min`           | Minimum value of the slider.                                           |
| `max`           | Maximum value of the slider.                                           |
| `divisions`     | (Optional) Number of discrete divisions — makes it a discrete slider.  |
| `label`         | (Optional) Label to show above the thumb when user is sliding.         |
| `onChanged`     | Called every time the value changes (used to update UI).               |
| `activeColor`   | (Optional) Color of the track between the thumb and the minimum value. |
| `inactiveColor` | (Optional) Color of the track between the thumb and the maximum value. |

---

### 📦 Example: Simple Slider in a StatefulWidget

```dart
class SliderExample extends StatefulWidget {
  @override
  _SliderExampleState createState() => _SliderExampleState();
}

class _SliderExampleState extends State<SliderExample> {
  double _sliderValue = 20;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Slider Example')),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Text('Value: ${_sliderValue.toStringAsFixed(1)}'),
          Slider(
            value: _sliderValue,
            min: 0,
            max: 100,
            divisions: 20,
            label: _sliderValue.round().toString(),
            onChanged: (double newValue) {
              setState(() {
                _sliderValue = newValue;
              });
            },
          ),
        ],
      ),
    );
  }
}
```

---

### 🎨 Customization

* Use `SliderTheme` to fully customize the appearance (thumb shape, track height, colors, etc).
* Use `RangeSlider` if you want to select a range (min and max value together).
