# Explain Text widget in Flutter

In Flutter, the `Text` widget is used to display a string of text with single style. It's one of the most commonly used widgets for UI development.

### 🔹 Basic Usage

```dart
Text('Hello, Flutter!')
```

---

### 🔹 Commonly Used Properties of `Text` Widget

#### 1. **`String data`**

* The text to display.
* Example: `Text('Welcome to Flutter')`

#### 2. **`TextStyle style`**

* Customizes the font, size, color, weight, etc.
* Example:

  ```dart
  Text(
    'Hello!',
    style: TextStyle(
      fontSize: 20,
      color: Colors.blue,
      fontWeight: FontWeight.bold,
    ),
  )
  ```

#### 3. **`TextAlign textAlign`**

* Aligns text horizontally.
* Values: `left`, `right`, `center`, `justify`, `start`, `end`
* Example: `Text('Centered Text', textAlign: TextAlign.center)`

#### 4. **`TextDirection textDirection`**

* Sets the direction of the text.
* Values: `TextDirection.ltr`, `TextDirection.rtl`

#### 5. **`int maxLines`**

* Limits the number of lines the text can occupy.
* Example: `Text('Long text...', maxLines: 2)`

#### 6. **`TextOverflow overflow`**

* Handles overflow if the text is too long.
* Values:

  * `TextOverflow.clip`
  * `TextOverflow.fade`
  * `TextOverflow.ellipsis`
  * `TextOverflow.visible`
* Example:

  ```dart
  Text(
    'This is a very long text...',
    maxLines: 1,
    overflow: TextOverflow.ellipsis,
  )
  ```

#### 7. **`bool softWrap`**

* If false, the text won’t wrap at soft line breaks.
* Example: `Text('No wrap', softWrap: false)`

#### 8. **`double textScaleFactor`**

* Scales the text size.
* Example: `Text('Scaled Text', textScaleFactor: 1.5)`

#### 9. **`StrutStyle strutStyle`**

* Defines minimum height of lines (for alignment with other widgets).

#### 10. **`Locale locale`**

* Overrides the inherited locale for this text.

#### 11. **`bool semanticsLabel`**

* Alternative label for screen readers.
* Example:

  ```dart
  Text(
    '1.5K',
    semanticsLabel: '1.5 thousand',
  )
  ```

---

### 🔹 Example with Multiple Properties

```dart
Text(
  'Hello, Flutter!',
  style: TextStyle(
    fontSize: 24,
    color: Colors.purple,
    fontWeight: FontWeight.w600,
    letterSpacing: 2.0,
  ),
  textAlign: TextAlign.center,
  overflow: TextOverflow.ellipsis,
  maxLines: 1,
)
```

