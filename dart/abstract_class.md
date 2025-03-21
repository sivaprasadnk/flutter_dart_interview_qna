# 🏆 **Abstract Classes in Dart**

An **abstract class** in Dart is a class that **cannot be instantiated** directly. It is used as a **blueprint** for other classes to extend and define their own implementations. Abstract classes help enforce a certain structure and behavior across multiple subclasses.

---

## 📌 **Why Use Abstract Classes?**  
✅ To define a common interface or behavior that subclasses must implement.  
✅ To prevent direct object creation from the abstract class.  
✅ To enable **polymorphism** (calling the same method on different types of objects).  
✅ Helps achieve **code reusability** and **loose coupling**.  

---

## 🧠 **Syntax:**  
- Use the `abstract` keyword before the class definition.  
- Abstract classes **can have both implemented and abstract methods** (methods without a body).  
- Abstract methods **must be implemented** by the subclasses.  

```dart
abstract class Animal {
  void makeSound(); // Abstract method (no body)
  
  void eat() {
    // Concrete method (implemented)
    print('Animal is eating');
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print('Bark!');
  }
}

void main() {
  // Animal animal = Animal(); // ❌ Error: Cannot instantiate abstract class
  Dog dog = Dog();
  dog.makeSound(); // Output: Bark!
  dog.eat();       // Output: Animal is eating
}
```

---

## 🎯 **Explanation:**  
1. `Animal` is an abstract class.  
2. `makeSound()` is an abstract method — no body provided.  
3. `eat()` is a concrete method — body is defined.  
4. `Dog` extends `Animal` and implements the `makeSound()` method.  
5. You **cannot create an object** of an abstract class (`Animal`), but you **can create an object** of its subclass (`Dog`).  

---

## 🚀 **Use Cases**  
✅ When you want to define a base class but don't want it to be instantiated directly.  
✅ When you want to define a template for other classes to follow.  
✅ When you want to provide some common behavior while forcing subclasses to implement specific methods.  

---

## 🛠️ **Example with Multiple Subclasses:**  
```dart
abstract class Shape {
  void draw(); // Abstract method
}

class Circle extends Shape {
  @override
  void draw() {
    print('Drawing a Circle');
  }
}

class Square extends Shape {
  @override
  void draw() {
    print('Drawing a Square');
  }
}

void main() {
  List<Shape> shapes = [Circle(), Square()];
  for (var shape in shapes) {
    shape.draw();
  }
}
```

**Output:**
```
Drawing a Circle  
Drawing a Square  
```

---

## 🌟 **Key Points to Remember:**  
✔️ Abstract classes **cannot be instantiated** directly.  
✔️ Abstract classes can have both **abstract and concrete methods**.  
✔️ Subclasses **must implement** all abstract methods of the abstract class.  
✔️ Abstract classes are useful for **code organization** and **polymorphism**.  

---

## 😎 **When to Use Abstract Classes:**  
✅ When you have a base class that should not be instantiated directly.  
✅ When you want to enforce a certain structure across multiple subclasses.  
✅ When you want to provide some default behavior but still require subclasses to implement certain methods.