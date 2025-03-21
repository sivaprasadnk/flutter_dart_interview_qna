# What are Packages and plugins in Flutter ?

In Flutter, **packages** and **plugins** are both used to extend the functionality of an app, but they serve different purposes:

### ✅ **Package**  
- A **package** contains **Dart code** that can be used to add functionality to a Flutter app.  
- It doesn’t include any platform-specific (Android/iOS) native code.  
- Packages are purely written in **Dart** and are independent of the underlying platform.  
- Example:  
   - `provider` – State management  
   - `http` – Networking  
   - `intl` – Date and number formatting  

### ✅ **Plugin**  
- A **plugin** is a type of package that includes **platform-specific code** (Android, iOS, web, etc.) to interact with native APIs.  
- It contains both **Dart** code and **native code** (Java/Kotlin for Android, Swift/Objective-C for iOS).  
- Plugins act as a bridge between Flutter and the native platform.  
- Example:  
   - `url_launcher` – Opens a URL using native platform capabilities  
   - `path_provider` – Access to device file system  
   - `camera` – Access to camera hardware  

### **Key Difference**  
| Feature | Package | Plugin |  
|---------|---------|--------|  
| Code Type | Pure Dart code | Dart + Native (Java/Kotlin/Swift) |  
| Platform Dependency | No | Yes |  
| Example | `http`, `provider` | `camera`, `path_provider` |  

👉 **Use a package** when you only need Dart code.  
👉 **Use a plugin** when you need to access platform-specific features.  