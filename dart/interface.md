# 🏆 **Interface in Dart**

In Dart, **interfaces** define a contract that a class must follow. Unlike other languages like Java or C#, Dart **does not have a separate `interface` keyword** — instead, **abstract classes** can be used as interfaces.

---

## 📌 **Why Use Interfaces?**  
✅ To define a consistent contract that classes must follow.  
✅ To achieve **polymorphism** — objects of different types can be treated uniformly.  
✅ To enable **multiple inheritance** — a class can implement multiple interfaces.  
✅ To separate **behavior from implementation**.  

---

## 🧠 **How to Create an Interface in Dart:**  
- Create an **abstract class** with abstract methods.  
- Implement the interface using the `implements` keyword.  
- The class implementing the interface **MUST override all methods** of the interface.  

---

## 🚀 **Example:**  
```dart
// Interface (using an abstract class)
abstract class Animal {
  void makeSound(); // Abstract method (interface-like)
}

// Implementing the interface
class Dog implements Animal {
  @override
  void makeSound() {
    print('Bark!');
  }
}

class Cat implements Animal {
  @override
  void makeSound() {
    print('Meow!');
  }
}

void main() {
  Dog dog = Dog();
  dog.makeSound(); // Output: Bark!

  Cat cat = Cat();
  cat.makeSound(); // Output: Meow!
}
```

---

## 🎯 **Explanation:**  
1. `Animal` acts as an **interface** since it’s an abstract class with an abstract method.  
2. `Dog` and `Cat` implement the `Animal` interface using `implements`.  
3. Both `Dog` and `Cat` **override** the `makeSound()` method.  
4. Interfaces **do not provide implementations** — only contracts.  

---

## 🏗️ **Interfaces vs Abstract Classes**  
| Feature | Abstract Class | Interface |
|---------|----------------|-----------|
| **Keyword** | `abstract class` | `abstract class` (using `implements`) |
| **Method Implementation** | Can have both abstract and concrete methods | All methods must be abstract |
| **Instantiation** | Cannot be instantiated directly | Cannot be instantiated directly |
| **Inheritance** | Can extend only one abstract class | Can implement multiple interfaces |
| **Purpose** | To provide base functionality | To define a contract for behavior |

---

## 🌟 **Example of Multiple Interfaces:**  
Dart allows a class to **implement multiple interfaces**:

```dart
abstract class Flyable {
  void fly();
}

abstract class Walkable {
  void walk();
}

class Bird implements Flyable, Walkable {
  @override
  void fly() {
    print('Bird is flying');
  }

  @override
  void walk() {
    print('Bird is walking');
  }
}

void main() {
  Bird bird = Bird();
  bird.fly(); // Output: Bird is flying
  bird.walk(); // Output: Bird is walking
}
```

### ✅ **Explanation:**  
- `Flyable` and `Walkable` act as interfaces.  
- `Bird` implements both interfaces using `implements`.  
- All methods of `Flyable` and `Walkable` must be **overridden**.  

---

## 🏆 **When to Use Interfaces:**  
✅ When you want to define a contract for other classes.  
✅ When you want to enable **polymorphism** (treat different objects similarly).  
✅ When you need **multiple inheritance** (Dart supports only single inheritance but allows multiple interfaces).  

---

## 😎 **Best Practices:**  
✅ Use **abstract classes** when you want to provide default behavior.  
✅ Use **interfaces** when you want to enforce a consistent structure without default behavior.  
✅ Keep interfaces **small and focused** — avoid adding too many methods.  