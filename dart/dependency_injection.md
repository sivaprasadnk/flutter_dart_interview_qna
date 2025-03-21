# 🏆 **Dependency Injection (DI) in Flutter**

Dependency Injection (DI) is a design pattern where an object receives its dependencies from an external source rather than creating them internally. This improves **modularity**, **testability**, and **maintainability** of the code.

---

## 🌟 **Why Dependency Injection in Flutter?**
✅ Reduces tight coupling between components  
✅ Makes unit testing easier by allowing mock dependencies  
✅ Allows better state and lifecycle management  
✅ Improves scalability and flexibility  

---

## 🎯 **Types of Dependency Injection**
1. **Constructor Injection** – Dependencies are passed through the constructor.  
2. **Setter Injection** – Dependencies are assigned using setters.  
3. **Service Locator Pattern** – Dependencies are retrieved from a globally available service container.  

---

## 🏗️ **1. Constructor Injection**
- Dependencies are passed when an object is created.
- Clean and easy to test.

### ✅ Example:
```dart
class ApiService {
  void fetchData() {
    print("Fetching data...");
  }
}

class MyRepository {
  final ApiService apiService;

  MyRepository(this.apiService);

  void getData() {
    apiService.fetchData();
  }
}

void main() {
  final apiService = ApiService();
  final repository = MyRepository(apiService);

  repository.getData();
}
```

### 🔍 **How It Works:**
- `ApiService` is injected into `MyRepository` through the constructor.
- Easy to mock for testing:
```dart
class MockApiService extends ApiService {
  @override
  void fetchData() {
    print("Mocked data fetch");
  }
}

void main() {
  final mockService = MockApiService();
  final repository = MyRepository(mockService);

  repository.getData(); // Outputs: Mocked data fetch
}
```

---

## 🏗️ **2. Setter Injection**
- Dependencies are assigned using a setter method.
- Useful when you don’t want to pass dependencies at construction.

### ✅ Example:
```dart
class ApiService {
  void fetchData() {
    print("Fetching data...");
  }
}

class MyRepository {
  late ApiService apiService;

  void setApiService(ApiService service) {
    apiService = service;
  }

  void getData() {
    apiService.fetchData();
  }
}

void main() {
  final repository = MyRepository();
  repository.setApiService(ApiService());

  repository.getData();
}
```

### 🔍 **How It Works:**
- `setApiService()` assigns the dependency at runtime.
- Easy to switch or mock dependencies.

---

## 🏗️ **3. Service Locator Pattern**
- A global registry where dependencies are registered and retrieved.
- Flutter’s **GetIt** package is widely used for this.

### ✅ Example using **GetIt**:
1. **Install GetIt**  
Add dependency to `pubspec.yaml`:
```yaml
dependencies:
  get_it: ^7.6.0
```

2. **Register Dependencies**:
```dart
import 'package:get_it/get_it.dart';

final getIt = GetIt.instance;

void setup() {
  getIt.registerSingleton<ApiService>(ApiService());
}
```

3. **Use Dependencies**:
```dart
class MyRepository {
  final ApiService apiService = getIt<ApiService>();

  void getData() {
    apiService.fetchData();
  }
}

void main() {
  setup();
  final repository = MyRepository();

  repository.getData(); // Output: Fetching data...
}
```

### 🔍 **How It Works:**
- `GetIt` creates a global instance.
- You can register different types:
  - `registerSingleton` – Same instance used everywhere.
  - `registerLazySingleton` – Created only when accessed for the first time.
  - `registerFactory` – New instance created every time.

---

## 🌟 **Using Dependency Injection with Flutter BLoC**
BLoC encourages constructor injection for passing dependencies.

### ✅ Example:
1. **Define Dependency:**
```dart
class ApiService {
  String fetchData() => "Data fetched";
}
```

2. **Register with GetIt:**
```dart
final getIt = GetIt.instance;

void setup() {
  getIt.registerSingleton<ApiService>(ApiService());
}
```

3. **Inject into BLoC:**
```dart
class MyBloc extends Bloc<MyEvent, MyState> {
  final ApiService apiService;

  MyBloc(this.apiService) : super(MyInitialState());

  @override
  Stream<MyState> mapEventToState(MyEvent event) async* {
    if (event is FetchDataEvent) {
      final data = apiService.fetchData();
      yield MyLoadedState(data);
    }
  }
}
```

4. **Provide BLoC:**
```dart
void main() {
  setup();

  runApp(
    BlocProvider(
      create: (context) => MyBloc(getIt<ApiService>()),
      child: MyApp(),
    ),
  );
}
```

---

## 🌟 **Using Dependency Injection with Provider**
1. **Register Dependency:**
```dart
void main() {
  runApp(
    MultiProvider(
      providers: [
        Provider<ApiService>(create: (_) => ApiService()),
      ],
      child: MyApp(),
    ),
  );
}
```

2. **Access Dependency:**
```dart
class MyRepository {
  final ApiService apiService;

  MyRepository(this.apiService);

  void fetchData() {
    apiService.fetchData();
  }
}

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final apiService = Provider.of<ApiService>(context, listen: false);
    apiService.fetchData();

    return Container();
  }
}
```

---

## 🌟 **Using Dependency Injection with Riverpod**
1. **Define Provider:**
```dart
final apiServiceProvider = Provider((ref) => ApiService());
```

2. **Access Provider:**
```dart
class MyWidget extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final apiService = ref.read(apiServiceProvider);
    apiService.fetchData();

    return Container();
  }
}
```

---

## 🌟 **Best Practices for DI**
✅ Use **constructor injection** for better testability.  
✅ Prefer **GetIt** for globally accessible services.  
✅ Use **Provider/Riverpod** for state-dependent dependencies.  
✅ Keep dependencies loosely coupled.  
✅ Avoid passing context to non-UI layers.  

---

## 🏆 **Comparison of DI Methods**
| Method | Pros | Cons |
|--------|------|------|
| **Constructor Injection** | Clean, testable | Requires passing objects manually |
| **Setter Injection** | Flexible, dynamic assignment | Harder to test |
| **GetIt (Service Locator)** | Global access, minimal boilerplate | Harder to track dependencies |
| **Provider/Riverpod** | Lifecycle-aware, testable | Requires setup |

---

## 🚀 **Summary**
✔️ DI improves modularity and testability.  
✔️ Constructor Injection → Clean and testable.  
✔️ GetIt → Best for global access and singletons.  
✔️ Provider/Riverpod → Best for lifecycle and state management.  
✔️ BLoC + DI → Scalable and maintainable code. 😎