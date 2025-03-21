# 🚀 **Singleton in Dart**  

A **Singleton** is a design pattern that ensures a class has **only one instance** throughout the lifecycle of an application and provides a global access point to that instance.

### ✅ **Why Use Singleton?**  
- Ensures a single instance of a class.  
- Saves memory and improves performance by reusing the same instance.  
- Useful for:  
  - Caching  
  - Database connections  
  - Network clients  
  - App configuration  

---

## ✅ **Creating a Singleton in Dart**  
There are **three main ways** to create a singleton in Dart:  

---

### **1. Eager Initialization**  
Create a singleton instance **immediately** when the class is loaded.  

```dart
class Singleton {
  // Create a static instance at the time of class loading
  static final Singleton _instance = Singleton._internal();

  // Private constructor
  Singleton._internal();

  // Factory constructor returns the existing instance
  factory Singleton() {
    return _instance;
  }

  void display() {
    print('Singleton instance accessed');
  }
}

void main() {
  var singleton1 = Singleton();
  var singleton2 = Singleton();

  singleton1.display();

  print(singleton1 == singleton2); // true
}
```

### ✅ **Output:**  
```
Singleton instance accessed  
true  
```

### ✅ **How It Works:**  
- `_instance` is created when the class is loaded.  
- `factory` constructor returns the same instance each time.  
- Ensures that only **one instance** exists across the app lifecycle.  

---

### **2. Lazy Initialization**  
Create a singleton instance **only when it is first accessed**.  

```dart
class Singleton {
  // Create a static instance
  static Singleton? _instance;

  // Private constructor
  Singleton._internal();

  // Factory constructor creates the instance when accessed
  factory Singleton() {
    _instance ??= Singleton._internal();
    return _instance!;
  }

  void display() {
    print('Lazy Singleton instance accessed');
  }
}

void main() {
  var singleton1 = Singleton();
  var singleton2 = Singleton();

  singleton1.display();

  print(singleton1 == singleton2); // true
}
```

### ✅ **Output:**  
```
Lazy Singleton instance accessed  
true  
```

### ✅ **How It Works:**  
- `_instance` is created **only when first accessed**.  
- Ensures that the object is created **only when needed** (saves resources).  
- `??=` assigns value only if it's `null`.  

---

### **3. Singleton Using `static` Getter**  
You can create a singleton using a `static` getter.  

```dart
class Singleton {
  static final Singleton _instance = Singleton._internal();

  Singleton._internal();

  static Singleton get instance => _instance;

  void display() {
    print('Static getter singleton accessed');
  }
}

void main() {
  var singleton1 = Singleton.instance;
  var singleton2 = Singleton.instance;

  singleton1.display();

  print(singleton1 == singleton2); // true
}
```

### ✅ **Output:**  
```
Static getter singleton accessed  
true  
```

### ✅ **How It Works:**  
- `_instance` is created eagerly.  
- `instance` getter returns the same instance.  
- Ensures a single global access point to the instance.  

---

## ✅ **When to Use Each Approach**  

| Method | When to Use | Example |  
|--------|-------------|---------|  
| **Eager Initialization** | When you always need the instance | Logger, configuration |  
| **Lazy Initialization** | When the instance is needed only under certain conditions | Database connection |  
| **Static Getter** | When you need a global access point | Shared Preferences |  

---

## ✅ **Example: Singleton for Database Connection**  
A common use case is using Singleton for managing database connections.  

```dart
class Database {
  static final Database _instance = Database._internal();

  Database._internal() {
    print('Database connection established');
  }

  factory Database() {
    return _instance;
  }

  void query(String sql) {
    print('Executing query: $sql');
  }
}

void main() {
  var db1 = Database();
  var db2 = Database();

  db1.query('SELECT * FROM users');
  db2.query('INSERT INTO users VALUES ("John", 30)');

  print(db1 == db2); // true
}
```

### ✅ **Output:**  
```
Database connection established  
Executing query: SELECT * FROM users  
Executing query: INSERT INTO users VALUES ("John", 30)  
true  
```

---

## ✅ **Example: Singleton for Network Client**  
Singleton ensures that the network client is reused, improving performance.  

```dart
class ApiClient {
  static final ApiClient _instance = ApiClient._internal();

  ApiClient._internal();

  factory ApiClient() {
    return _instance;
  }

  void getData() {
    print('Fetching data from server...');
  }
}

void main() {
  var client1 = ApiClient();
  var client2 = ApiClient();

  client1.getData();
  client2.getData();

  print(client1 == client2); // true
}
```

### ✅ **Output:**  
```
Fetching data from server...  
Fetching data from server...  
true  
```

---

## 🚀 **Best Practices**  
✅ Keep the constructor **private** to prevent direct instantiation.  
✅ Use **factory constructors** to control instance creation.  
✅ Make the instance **static** to store it globally.  
✅ Use **lazy initialization** when the instance is resource-intensive.  

---

## 🏆 **Summary**  
| Type | How It Works | Example |  
|-------|--------------|---------|  
| **Eager Initialization** | Instance created immediately | Logger, Config |  
| **Lazy Initialization** | Instance created when first accessed | Database, API Client |  
| **Static Getter** | Access instance using `get` | Shared Preferences, Cache |  

---

### 🚀 **Rule of Thumb:**  
- ✅ Use **Eager Initialization** → When the instance is lightweight and always required.  
- ✅ Use **Lazy Initialization** → When the instance is resource-heavy or conditional.  
- ✅ Use **Static Getter** → When you need global access to the instance. 😎