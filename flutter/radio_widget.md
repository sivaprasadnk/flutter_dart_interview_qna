# Explain Radio Widget in Flutter  

In Flutter, a **`RadioButton`** is created using the `Radio` widget. It's used when you want users to select a **single option from a group**.

### 📌 Basic Usage

Here’s a simple example of how to use `Radio` in Flutter:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

enum Gender { male, female }

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: RadioExample(),
    );
  }
}

class RadioExample extends StatefulWidget {
  @override
  _RadioExampleState createState() => _RadioExampleState();
}

class _RadioExampleState extends State<RadioExample> {
  Gender? _selectedGender = Gender.male;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Radio Button Example')),
      body: Column(
        children: [
          ListTile(
            title: Text('Male'),
            leading: Radio<Gender>(
              value: Gender.male,
              groupValue: _selectedGender,
              onChanged: (Gender? value) {
                setState(() {
                  _selectedGender = value;
                });
              },
            ),
          ),
          ListTile(
            title: Text('Female'),
            leading: Radio<Gender>(
              value: Gender.female,
              groupValue: _selectedGender,
              onChanged: (Gender? value) {
                setState(() {
                  _selectedGender = value;
                });
              },
            ),
          ),
        ],
      ),
    );
  }
}
```

### 🔍 Key Points

* `value`: The value this radio button represents.
* `groupValue`: The value currently selected in the group.
* `onChanged`: Callback when selection changes.

