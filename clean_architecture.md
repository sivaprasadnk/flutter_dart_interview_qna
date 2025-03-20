# 🏛️ **Clean Architecture in Flutter**  

Clean Architecture is a design pattern introduced by **Robert C. Martin (Uncle Bob)** that helps build **scalable, maintainable, and testable** applications by organizing code into **independent layers** with clear separation of concerns.

---

## 🎯 **Goals of Clean Architecture**  
✅ Separation of Concerns  
✅ Independence of Frameworks (Flutter, Firebase, etc.)  
✅ Independence of UI and Business Logic  
✅ Easy to Test and Maintain  
✅ Highly Scalable  

---

## 🏗️ **Layered Structure of Clean Architecture**  
Clean Architecture is organized into **four main layers**:

```
Presentation Layer  ---> UI Components (Stateless, Stateful Widgets)
------------------
Application Layer   ---> State Management (BLoC, Provider)
------------------
Domain Layer        ---> Business Logic (Use Cases, Entities)
------------------
Data Layer          ---> Repositories, Data Sources (API, Database)
```

---

## 🔎 **1. Presentation Layer**  
- Handles the **UI** and **state** of the app.  
- Communicates with the **Application Layer** to receive data.  
- Contains:  
   - `Widgets` (Stateless/Stateful)  
   - `State Management` (BLoC, Provider)  
   - `UI Logic`  

✅ **Example:**  
```dart
class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: BlocBuilder<LoginBloc, LoginState>(
        builder: (context, state) {
          if (state is LoginLoading) {
            return CircularProgressIndicator();
          } else if (state is LoginSuccess) {
            return Text('Welcome!');
          } else {
            return Text('Login Failed');
          }
        },
      ),
    );
  }
}
```

---

## 🎯 **2. Application Layer**  
- Handles **state management** and **business flow**.  
- Contains:  
   - `BLoC` or `Provider`  
   - **Event Handling**  
   - **State Updates**  

✅ **Example (BLoC):**  
```dart
class LoginEvent {
  final String username;
  final String password;

  LoginEvent(this.username, this.password);
}
```

```dart
class LoginBloc extends Bloc<LoginEvent, LoginState> {
  final LoginUseCase _loginUseCase;

  LoginBloc(this._loginUseCase) : super(LoginInitial()) {
    on<LoginEvent>((event, emit) async {
      emit(LoginLoading());
      final result = await _loginUseCase(event.username, event.password);
      result.fold(
        (failure) => emit(LoginFailed(failure.message)),
        (_) => emit(LoginSuccess()),
      );
    });
  }
}
```

---

## 🔥 **3. Domain Layer**  
- **Heart of the application** – contains the business logic.  
- Independent from UI and data sources.  
- Contains:  
   - **Entities** – Core business models.  
   - **Use Cases** – Business logic.  
   - **Repositories (Interfaces)** – Contracts for data handling.  

✅ **Entity:**  
```dart
class User {
  final String id;
  final String name;

  User({required this.id, required this.name});
}
```

✅ **Use Case:**  
```dart
class LoginUseCase {
  final UserRepository repository;

  LoginUseCase(this.repository);

  Future<Either<Failure, User>> call(String username, String password) {
    return repository.login(username, password);
  }
}
```

✅ **Repository Interface:**  
```dart
abstract class UserRepository {
  Future<Either<Failure, User>> login(String username, String password);
}
```

---

## 🗄️ **4. Data Layer**  
- Handles **data fetching** and **storage**.  
- Contains:  
   - **Repositories (Implementation)** – Communicate with remote/local sources.  
   - **Data Sources** – REST API, Firebase, SQLite, etc.  
   - **Models** – Convert between business and data models.  

✅ **Repository Implementation:**  
```dart
class UserRepositoryImpl implements UserRepository {
  final RemoteDataSource remoteDataSource;

  UserRepositoryImpl(this.remoteDataSource);

  @override
  Future<Either<Failure, User>> login(String username, String password) async {
    try {
      final userModel = await remoteDataSource.login(username, password);
      return Right(userModel.toEntity());
    } catch (e) {
      return Left(ServerFailure());
    }
  }
}
```

✅ **Remote Data Source:**  
```dart
class RemoteDataSource {
  final HttpClient client;

  RemoteDataSource(this.client);

  Future<UserModel> login(String username, String password) async {
    final response = await client.post(
      Uri.parse('https://api.example.com/login'),
      body: {'username': username, 'password': password},
    );
    return UserModel.fromJson(json.decode(response.body));
  }
}
```

✅ **Model:**  
```dart
class UserModel {
  final String id;
  final String name;

  UserModel({required this.id, required this.name});

  factory UserModel.fromJson(Map<String, dynamic> json) {
    return UserModel(
      id: json['id'],
      name: json['name'],
    );
  }

  User toEntity() {
    return User(id: id, name: name);
  }
}
```

---

## 🛠️ **Dependency Injection (Service Locator)**  
- Use `get_it` to inject dependencies across layers.  
- Keeps the code loosely coupled and easier to test.  

✅ **Setup:**  
```dart
final sl = GetIt.instance;

void setup() {
  sl.registerLazySingleton(() => HttpClient());
  sl.registerLazySingleton(() => RemoteDataSource(sl()));
  sl.registerLazySingleton<UserRepository>(() => UserRepositoryImpl(sl()));
  sl.registerLazySingleton(() => LoginUseCase(sl()));
  sl.registerFactory(() => LoginBloc(sl()));
}
```

---

## 📂 **Folder Structure**  
Here's how a Clean Architecture folder structure typically looks:

```
lib/
├── core/
│   ├── errors/
│   ├── usecases/
├── data/
│   ├── models/
│   ├── repositories/
│   ├── sources/
├── domain/
│   ├── entities/
│   ├── repositories/
│   ├── usecases/
├── presentation/
│   ├── blocs/
│   ├── pages/
│   ├── widgets/
├── main.dart
```

---

## 🎯 **Summary of Clean Architecture**  

| Layer | Purpose | Example |
|-------|---------|---------|
| **Presentation** | Handles UI & State | `BlocBuilder`, `StatelessWidget` |
| **Application** | Handles State & Business Flow | `Bloc`, `Cubit` |
| **Domain** | Core Business Logic | `Use Case`, `Entity` |
| **Data** | Data Handling | `Repository`, `RemoteDataSource` |

---

## 🚀 **Why Clean Architecture?**  
✅ Reduces coupling between layers  
✅ Easy to test and maintain  
✅ Improves scalability  
✅ Works well with state management (BLoC, Provider)  

---

## 🎯 **Best Practices**  
✔️ Keep the domain layer independent from Flutter or other frameworks.  
✔️ Keep repository interfaces in the domain layer and implementations in the data layer.  
✔️ Ensure business logic is separate from the UI layer.  
✔️ Inject dependencies using `get_it` or `riverpod`.  

---

## 🌟 **Clean Architecture = Scalability + Testability + Maintainability** 😎