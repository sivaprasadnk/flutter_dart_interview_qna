# What are app life-cycle methods in Flutter ?

The **App-Level Lifecycle** in Flutter refers to the different states that the entire app goes through — from launching, backgrounding, resuming, to termination.

---

## 🌍 **1. AppLifecycleState**  
Flutter uses the `AppLifecycleState` enum to represent different app states:

| State | Description | Example |
|-------|-------------|---------|
| **`resumed`** | App is in the foreground and active | User is actively using the app |
| **`inactive`** | App is transitioning to or from the background | Receiving a phone call |
| **`paused`** | App is in the background but still in memory | User pressed the home button |
| **`detached`** | App is removed from memory or terminated | User swiped the app away from recent apps |

---

## 🔄 **2. How to Monitor App Lifecycle Changes**  
You can track app lifecycle changes by implementing `WidgetsBindingObserver`.

### 🌟 **Example: Tracking App State**  
```dart
class MyApp extends StatefulWidget {
  @override
  State<MyApp> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> with WidgetsBindingObserver {
  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void didChangeAppLifecycleState(AppLifecycleState state) {
    print('AppLifecycleState: $state');

    if (state == AppLifecycleState.resumed) {
      print('✅ App is visible');
    } else if (state == AppLifecycleState.inactive) {
      print('⚠️ App is inactive');
    } else if (state == AppLifecycleState.paused) {
      print('⏸️ App is in the background');
    } else if (state == AppLifecycleState.detached) {
      print('❌ App is terminated');
    }
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(body: Center(child: Text('App Lifecycle'))),
    );
  }
}
```

---

## 🔥 **3. When States Are Triggered**  

| Lifecycle State | When It Happens | Example |
|----------------|-----------------|---------|
| **`resumed`** | When the app comes to the foreground | Opening the app from recent apps |
| **`inactive`** | When the app is in an inactive state | Answering a phone call |
| **`paused`** | When the app is sent to the background | Pressing the home button |
| **`detached`** | When the app is closed or terminated | Removing the app from recent apps |

---

## 🏆 **4. Best Practices**  
✅ Use `resumed` to refresh UI or reload data.  
✅ Use `paused` to save state or stop background tasks.  
✅ Use `detached` to clean up resources and close connections.  
✅ Avoid heavy processing in `inactive` to avoid UI freezes.  

---

## 🚀 **5. Example Use Cases**  
✅ **Tracking user sessions:** Start a timer when the app is resumed and stop it when paused.  
✅ **Saving state:** Save user progress when the app is paused.  
✅ **Releasing resources:** Close database connections when the app is detached.  
✅ **Handling notifications:** Update notifications based on app state.  