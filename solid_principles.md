# Explain SOLID principles

The **SOLID principles** are five design principles that help create more maintainable, scalable, and testable code. These principles, originally defined for object-oriented programming, apply well to Flutter development because Flutter uses Dart, which is an object-oriented language.

### ✅ **S – Single Responsibility Principle (SRP)**
> *A class should have one and only one reason to change.*

### 🔹 In Flutter:
- Each class should focus on doing one thing only.
- A widget should handle only one part of the UI or logic.
- Avoid combining business logic and UI code in the same class.

### **Example:**
Instead of mixing UI and business logic:

❌ **Bad Approach:**
```dart
class UserProfileWidget extends StatelessWidget {
  final User user;

  UserProfileWidget(this.user);

  void saveUserToDatabase(User user) {
    // Logic to save user to DB
  }

  @override
  Widget build(BuildContext context) {
    return Text(user.name);
  }
}
```

✅ **Good Approach:**
- Separate UI and business logic using BLoC or Provider:

```dart
class UserRepository {
  void saveUserToDatabase(User user) {
    // Logic to save user to DB
  }
}

class UserProfileWidget extends StatelessWidget {
  final User user;

  UserProfileWidget(this.user);

  @override
  Widget build(BuildContext context) {
    return Text(user.name);
  }
}
```

---

### ✅ **O – Open/Closed Principle (OCP)**
> *Software entities (classes, modules, functions) should be open for extension but closed for modification.*

### 🔹 In Flutter:
- Instead of modifying existing code, create new classes or extend them.
- Use **abstract classes** and **inheritance** to extend functionality without changing existing code.

### **Example:**
❌ **Bad Approach:**
Modifying existing class directly:
```dart
class Payment {
  void payWithCreditCard() {
    // Payment logic
  }
}
```

✅ **Good Approach:**
Use abstraction to extend behavior:
```dart
abstract class Payment {
  void pay();
}

class CreditCardPayment extends Payment {
  @override
  void pay() {
    // Payment logic
  }
}

class RazorpayPayment extends Payment {
  @override
  void pay() {
    // Razorpay payment logic
  }
}
```

---

### ✅ **L – Liskov Substitution Principle (LSP)**
> *Derived classes must be substitutable for their base classes without altering program correctness.*

### 🔹 In Flutter:
- Subclasses should work as a drop-in replacement for their parent class without breaking functionality.

### **Example:**
❌ **Bad Approach:**
Breaking parent behavior:
```dart
class Bird {
  void fly() {
    print('Flying');
  }
}

class Penguin extends Bird {
  @override
  void fly() {
    throw Exception('Penguins cannot fly');
  }
}
```

✅ **Good Approach:**
Create a separate hierarchy:
```dart
abstract class Bird {
  void eat();
}

class FlyingBird extends Bird {
  void fly() => print('Flying');
}

class Penguin extends Bird {
  void swim() => print('Swimming');
}
```

---

### ✅ **I – Interface Segregation Principle (ISP)**
> *Clients should not be forced to depend on methods they do not use.*

### 🔹 In Flutter:
- Split large interfaces into smaller, more specific ones.

### **Example:**
❌ **Bad Approach:**
Forcing a class to implement unnecessary methods:
```dart
abstract class Worker {
  void work();
  void eat();
}

class Robot implements Worker {
  @override
  void work() {
    print('Working');
  }

  @override
  void eat() {
    throw Exception('Robots don’t eat');
  }
}
```

✅ **Good Approach:**
Create separate interfaces:
```dart
abstract class Workable {
  void work();
}

abstract class Eatable {
  void eat();
}

class Robot implements Workable {
  @override
  void work() => print('Working');
}
```

---

### ✅ **D – Dependency Inversion Principle (DIP)**
> *Depend on abstractions, not on concrete implementations.*

### 🔹 In Flutter:
- Use **dependency injection** and **service locators**.
- Pass dependencies via constructors instead of creating them directly.

### **Example:**
❌ **Bad Approach:**
```dart
class UserService {
  final Database _database = Database();

  void saveUser(User user) {
    _database.save(user);
  }
}
```

✅ **Good Approach:**
Inject dependency using abstraction:
```dart
abstract class Database {
  void save(User user);
}

class FirebaseDatabase implements Database {
  @override
  void save(User user) {
    // Firebase logic
  }
}

class UserService {
  final Database database;

  UserService(this.database);

  void saveUser(User user) {
    database.save(user);
  }
}
```

---

## 🚀 **How SOLID Applies to Flutter:**
| Principle | Application in Flutter |
|----------|------------------------|
| **SRP** | Separate UI, business logic, and data layers using BLoC or Provider. |
| **OCP** | Create new widgets instead of modifying existing ones. |
| **LSP** | Ensure subclasses can replace parent classes without breaking functionality. |
| **ISP** | Create smaller, focused interfaces. |
| **DIP** | Use constructor injection and service locators (like GetIt). |

---

### ✅ **Best Practices in Flutter:**
- Use **BLoC** or **Provider** for state management.  
- Follow **Clean Architecture** to separate data, domain, and presentation layers.  
- Use **abstract classes** and **interfaces** to avoid tight coupling.  
- Keep widgets and business logic **independent**.  
- Write **unit tests** to ensure LSP and DIP are followed.  
