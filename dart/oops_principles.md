# Explain OOPS principles in Dart

In Dart, **OOPs (Object-Oriented Programming) principles** follow the four main pillars of OOP:

### 1. **Encapsulation**  
Encapsulation is the bundling of data (fields) and methods that operate on the data into a single unit, typically a class. It also involves restricting direct access to some of an object's components.

**Example:**
```dart
class BankAccount {
  String _accountHolder; // Private variable (underscore makes it private)
  double _balance;

  BankAccount(this._accountHolder, this._balance);

  void deposit(double amount) {
    _balance += amount;
    print("Deposited $amount. New Balance: $_balance");
  }

  void withdraw(double amount) {
    if (amount <= _balance) {
      _balance -= amount;
      print("Withdrew $amount. New Balance: $_balance");
    } else {
      print("Insufficient funds!");
    }
  }

  double get balance => _balance; // Getter to access private variable
}

void main() {
  var account = BankAccount("John Doe", 1000);
  account.deposit(500);
  account.withdraw(300);
  print("Final Balance: ${account.balance}");
}
```

---

### 2. **Abstraction**  
Abstraction means hiding implementation details and exposing only essential features.

**Example using `abstract` class:**
```dart
abstract class Vehicle {
  void start(); // Abstract method (no implementation)
}

class Car extends Vehicle {
  @override
  void start() {
    print("Car is starting with key ignition.");
  }
}

void main() {
  var car = Car();
  car.start();
}
```

---

### 3. **Inheritance**  
Inheritance allows a class to acquire properties and behaviors of another class.

**Example:**
```dart
class Animal {
  void makeSound() {
    print("Animal makes a sound");
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print("Dog barks");
  }
}

void main() {
  var dog = Dog();
  dog.makeSound(); // Output: Dog barks
}
```

---

### 4. **Polymorphism**  
Polymorphism allows the same method to have different implementations.

**Example:**
```dart
class Shape {
  void draw() {
    print("Drawing a shape");
  }
}

class Circle extends Shape {
  @override
  void draw() {
    print("Drawing a circle");
  }
}

class Square extends Shape {
  @override
  void draw() {
    print("Drawing a square");
  }
}

void main() {
  Shape shape1 = Circle();
  Shape shape2 = Square();

  shape1.draw(); // Output: Drawing a circle
  shape2.draw(); // Output: Drawing a square
}
```

---

### Conclusion  
Dart fully supports **OOP principles**, making it an excellent choice for structured and reusable code in Flutter development. You can use **Encapsulation**, **Abstraction**, **Inheritance**, and **Polymorphism** to write efficient, scalable, and maintainable applications.