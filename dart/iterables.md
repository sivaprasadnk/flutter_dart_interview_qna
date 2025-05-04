# Explain Iterables in Dart

In Dart, an **`Iterable`** is a collection of elements that can be **traversed sequentially**. It is the core class for working with lists, sets, and other sequences of data.

---

### 🧠 What is an Iterable?

An `Iterable<T>` represents a **sequence of items of type `T`**, which you can loop through using a `for-in` loop, `forEach()`, or iterators.

```dart
Iterable<int> numbers = [1, 2, 3];
```

Here, `List<int>` is an `Iterable<int>`, because lists in Dart implement the `Iterable` interface.

---

### 🔁 Common Ways to Use Iterables:

#### 1. **For-in loop:**

```dart
for (var number in numbers) {
  print(number);
}
```

#### 2. **forEach method:**

```dart
numbers.forEach((number) => print(number));
```

#### 3. **Using Iterator manually:**

```dart
var iterator = numbers.iterator;
while (iterator.moveNext()) {
  print(iterator.current);
}
```

---

### 📦 Common Iterable Methods:

* `map()`: transforms each element.
* `where()`: filters elements.
* `reduce()`: combines elements into a single value.
* `any()` / `every()`: boolean checks.
* `toList()` / `toSet()`: converts to concrete collections.

#### Example:

```dart
var evenNumbers = numbers.where((n) => n.isEven);
print(evenNumbers); // (2)
```

---

### 🔧 Custom Iterable Example:

You can even create your own iterable:

```dart
class MyIterable extends Iterable<int> {
  @override
  Iterator<int> get iterator => [10, 20, 30].iterator;
}
```

---

### 📌 Note:

* **Iterables are lazy** – operations like `map()` or `where()` don’t compute results until you iterate over them.
* Once iterated, they can be collected into a `List` or `Set` for repeated access.
