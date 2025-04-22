# Explain TextFormField & TextField in Flutter


## 🔷 `TextField`

`TextField` is the **basic widget** for taking text input in Flutter.

### ✅ Features:
- Used for simple input like name, email, etc.
- Allows you to listen to changes via `onChanged`, `controller`, etc.
- Doesn’t support built-in validation or form integration.

### 🔧 Example:
```dart
TextField(
  decoration: InputDecoration(labelText: 'Enter your name'),
  onChanged: (value) {
    print('User typed: $value');
  },
)
```

---

## 🔷 `TextFormField`

`TextFormField` is a **wrapper around `TextField`** with added features for **form handling and validation**.

### ✅ Features:
- Built-in support for **validation** (`validator` property)
- Works well inside a `Form` widget using a `GlobalKey<FormState>`
- Can save and validate form fields easily

### 🔧 Example:
```dart
final _formKey = GlobalKey<FormState>();

Form(
  key: _formKey,
  child: Column(
    children: [
      TextFormField(
        decoration: InputDecoration(labelText: 'Enter email'),
        validator: (value) {
          if (value == null || value.isEmpty) {
            return 'Please enter your email';
          }
          return null;
        },
      ),
      ElevatedButton(
        onPressed: () {
          if (_formKey.currentState!.validate()) {
            // Process data
          }
        },
        child: Text('Submit'),
      ),
    ],
  ),
)
```

---

## 🆚 Summary Table:

| Feature               | `TextField`        | `TextFormField`         |
|----------------------|--------------------|-------------------------|
| Simple Input          | ✅                 | ✅                      |
| Form Validation       | ❌                 | ✅                      |
| Requires `Form` Widget | ❌                | Usually ✅              |
| Use Case              | Basic Input Fields | Validated Form Inputs   |

---

If you're building a form with validation (like login or registration), go with `TextFormField`.  
If you're just collecting a simple input (like a search bar), `TextField` is enough.
