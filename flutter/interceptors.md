# What are interceptors in Flutter ?

Interceptors in Flutter are commonly used in networking to intercept and manipulate requests and responses before they reach the API or UI. In Flutter, the most popular way to implement interceptors is with the **Dio** package.

---

## 🚀 **What are Interceptors?**
Interceptors allow you to:
- Modify **outgoing requests** before they are sent.
- Inspect or modify **responses** before they reach the app.
- Handle **errors** and retry failed requests.

---

## 📌 **Using Interceptors with Dio**
Dio is a powerful HTTP client that supports interceptors.

### **Step 1: Add Dio to `pubspec.yaml`**
```yaml
dependencies:
  dio: ^5.4.0  # Use the latest version
```

### **Step 2: Implement Interceptors**
```dart
import 'package:dio/dio.dart';

class DioClient {
  final Dio dio = Dio(BaseOptions(
    baseUrl: "https://api.example.com",
    connectTimeout: const Duration(seconds: 10),
    receiveTimeout: const Duration(seconds: 10),
  ));

  DioClient() {
    dio.interceptors.add(
      InterceptorsWrapper(
        onRequest: (options, handler) {
          // Modify request (e.g., add headers)
          options.headers['Authorization'] = 'Bearer YOUR_ACCESS_TOKEN';
          print("🚀 Request: ${options.method} ${options.uri}");
          return handler.next(options); // Continue request
        },
        onResponse: (response, handler) {
          // Modify response before passing to UI
          print("✅ Response: ${response.statusCode}");
          return handler.next(response);
        },
        onError: (DioException e, handler) {
          // Handle errors globally
          print("❌ Error: ${e.message}");
          return handler.next(e); // Continue error propagation
        },
      ),
    );
  }

  Future<Response> getData(String endpoint) async {
    return await dio.get(endpoint);
  }
}
```

---

## 🎯 **Advanced Interceptor Usage**
### 1️⃣ **Logging Interceptor**
Use `LogInterceptor` to print request/response details:
```dart
dio.interceptors.add(LogInterceptor(
  request: true,
  requestBody: true,
  responseBody: true,
  error: true,
));
```

### 2️⃣ **Retry Failed Requests**
If a request fails (e.g., due to a network issue), you can retry it:
```dart
onError: (DioException e, handler) {
  if (e.type == DioExceptionType.connectionTimeout) {
    print("🔄 Retrying request...");
    return dio.request(e.requestOptions.path, options: e.requestOptions);
  }
  return handler.next(e);
},
```

### 3️⃣ **Token Refresh Handling**
If a request fails due to an expired token, refresh it and retry:
```dart
onError: (DioException e, handler) async {
  if (e.response?.statusCode == 401) {
    // Call refresh token API and update token
    String newToken = await refreshToken();
    e.requestOptions.headers['Authorization'] = 'Bearer $newToken';

    // Retry original request with new token
    return dio.request(e.requestOptions.path, options: e.requestOptions);
  }
  return handler.next(e);
},
```

---

## 🎯 **Use Case Scenarios**
✅ **Authentication** – Attach JWT tokens automatically.  
✅ **Logging** – Log API requests and responses.  
✅ **Error Handling** – Handle errors globally instead of scattered try-catch.  
✅ **Caching** – Store and reuse API responses.  
✅ **Retry Logic** – Automatically retry failed requests.  

---

## 🏆 **Conclusion**
Interceptors in Flutter (via Dio) help streamline network requests by modifying, handling, and optimizing API calls before they reach the app or backend. They improve **code maintainability, error handling, and debugging**.
