# What are platform channels in Flutter ?

In Flutter, **Platform Channels** are used to communicate between **Flutter (Dart)** and **native platforms** like **Android (Java/Kotlin)** and **iOS (Swift/Objective-C)**.

---

## 🚀 **What Are Platform Channels?**  
Flutter’s code runs on a **Dart VM** (virtual machine), but sometimes you need to access native platform-specific features (like camera, GPS, notifications, etc.) that are not available directly in Flutter.  

👉 **Platform Channels** act as a **bridge** between Flutter and native code, allowing Flutter to send messages to native code and get a response back.

---

## ✅ **How It Works**  
1. Flutter creates a `MethodChannel` and sends a message to the native platform.  
2. Native platform code listens for this message and processes it.  
3. The platform sends a result back to Flutter through the same channel.  

---

## 🎯 **Types of Platform Channels**  
| Channel Type | Purpose | Use Case |
|-------------|---------|----------|
| **MethodChannel** | Calls native methods and gets a result | Get battery level, Open native activity |
| **EventChannel** | Establishes a continuous stream of events from native to Flutter | Sensor updates, Location tracking |
| **BasicMessageChannel** | For lightweight message passing | JSON or simple data exchange |

---

## 🏷️ **1. MethodChannel**  
→ Used to call native methods and return a single result.

---

### **Example: Getting Battery Level Using MethodChannel**  
### 🔹 Flutter Code (Dart)  
```dart
import 'package:flutter/services.dart';

class BatteryLevel {
  static const platform = MethodChannel('com.example.battery');

  Future<String> getBatteryLevel() async {
    try {
      final int result = await platform.invokeMethod('getBatteryLevel');
      return 'Battery level: $result%';
    } on PlatformException catch (e) {
      return 'Failed to get battery level: ${e.message}';
    }
  }
}
```

---

### 🔹 Android Code (Kotlin)  
```kotlin
class MainActivity : FlutterActivity() {
    private val CHANNEL = "com.example.battery"

    override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
        MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL).setMethodCallHandler { call, result ->
            if (call.method == "getBatteryLevel") {
                val batteryLevel = getBatteryLevel()
                if (batteryLevel != -1) {
                    result.success(batteryLevel)
                } else {
                    result.error("UNAVAILABLE", "Battery level not available.", null)
                }
            } else {
                result.notImplemented()
            }
        }
    }

    private fun getBatteryLevel(): Int {
        val batteryManager = getSystemService(BATTERY_SERVICE) as BatteryManager
        return batteryManager.getIntProperty(BatteryManager.BATTERY_PROPERTY_CAPACITY)
    }
}
```

---

### 🔹 iOS Code (Swift)  
```swift
import Flutter
import UIKit

@UIApplicationMain
@objc class AppDelegate: FlutterAppDelegate {
  override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    let controller = window?.rootViewController as! FlutterViewController
    let batteryChannel = FlutterMethodChannel(name: "com.example.battery",
                                              binaryMessenger: controller.binaryMessenger)
    batteryChannel.setMethodCallHandler { (call, result) in
      if call.method == "getBatteryLevel" {
        result(self.getBatteryLevel())
      } else {
        result(FlutterMethodNotImplemented)
      }
    }
    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }

  private func getBatteryLevel() -> Int {
    UIDevice.current.isBatteryMonitoringEnabled = true
    return Int(UIDevice.current.batteryLevel * 100)
  }
}
```

---

### ✅ **How It Works:**  
- Flutter calls `invokeMethod('getBatteryLevel')`.  
- Native side (Kotlin/Swift) listens to the channel and executes the native code.  
- Result is returned to Flutter through the same channel.  

---

## 🏷️ **2. EventChannel**  
→ Used for **continuous streams** of data from native to Flutter.  
→ Example: Location updates, sensor readings, connectivity changes.  

---

### **Example: Getting Accelerometer Data Using EventChannel**  
### 🔹 Flutter Code (Dart)  
```dart
import 'package:flutter/services.dart';

class SensorData {
  static const EventChannel _eventChannel = EventChannel('com.example.sensors');

  Stream<double> get sensorDataStream =>
      _eventChannel.receiveBroadcastStream().map((event) => event as double);
}
```

---

### 🔹 Android Code (Kotlin)  
```kotlin
class MainActivity : FlutterActivity() {
    private val SENSOR_CHANNEL = "com.example.sensors"
    private var eventSink: EventChannel.EventSink? = null

    override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
        EventChannel(flutterEngine.dartExecutor.binaryMessenger, SENSOR_CHANNEL)
            .setStreamHandler(object : EventChannel.StreamHandler {
                override fun onListen(arguments: Any?, events: EventChannel.EventSink?) {
                    eventSink = events
                    // Send data to Flutter periodically
                    startListeningToSensor()
                }

                override fun onCancel(arguments: Any?) {
                    eventSink = null
                }
            })
    }

    private fun startListeningToSensor() {
        // Send mock data
        Handler(Looper.getMainLooper()).postDelayed({
            eventSink?.success(9.81) // Example accelerometer value
        }, 1000)
    }
}
```

---

### ✅ **How It Works:**  
- Flutter starts a stream using `receiveBroadcastStream()`.  
- Native code listens for the stream and sends data periodically using `success()`.  
- Flutter UI gets updated with the streamed data.  

---

## 🏷️ **3. BasicMessageChannel**  
→ Used for **lightweight message passing** between Flutter and native code.  
→ Example: Sending JSON or simple string data.  

---

### **Example: Sending JSON Using BasicMessageChannel**  
### 🔹 Flutter Code (Dart)  
```dart
import 'package:flutter/services.dart';

class MessageChannel {
  static const _channel = BasicMessageChannel<String>('com.example.message', StringCodec());

  Future<void> sendMessage(String message) async {
    final reply = await _channel.send(message);
    print('Reply from native: $reply');
  }
}
```

---

### 🔹 Android Code (Kotlin)  
```kotlin
class MainActivity : FlutterActivity() {
    private val CHANNEL = "com.example.message"

    override fun configureFlutterEngine(@NonNull flutterEngine: FlutterEngine) {
        BasicMessageChannel(
            flutterEngine.dartExecutor.binaryMessenger,
            CHANNEL,
            StringCodec.INSTANCE
        ).setMessageHandler { message, reply ->
            Log.d("FlutterMessage", "Received message: $message")
            reply.reply("Message received: $message")
        }
    }
}
```

---

### ✅ **How It Works:**  
- Flutter sends a string using `send()`.  
- Native code receives it and responds back.  
- Flutter receives the response.  

---

## 🎯 **Platform Channel Types – When to Use What?**  
| Type | Best For | Direction | Complexity |
|-------|----------|-----------|------------|
| **MethodChannel** | Calling native functions | Flutter → Native → Flutter | Moderate |
| **EventChannel** | Continuous data stream | Native → Flutter | High |
| **BasicMessageChannel** | Lightweight messages (JSON, Strings) | Flutter ↔️ Native | Low |

---

## ✅ **Best Practices**  
✔️ Use a consistent channel name (`com.example.app/feature`).  
✔️ Handle platform exceptions properly.  
✔️ Keep channel handling lightweight (avoid complex logic).  
✔️ Use `MethodChannel` for most platform integrations.  
✔️ Use `EventChannel` for real-time data streams.  
✔️ Use `BasicMessageChannel` for simple data passing.  

---

## 🚀 **Summary**  
| Platform Channel | Purpose | Complexity | Example |
|------------------|---------|------------|---------|
| **MethodChannel** | Execute native methods | Moderate | Get battery level |
| **EventChannel** | Continuous data streams | High | Location updates |
| **BasicMessageChannel** | Lightweight messaging | Low | Send JSON/string |

---

🔥 **Platform Channels** are the backbone of Flutter-native integration! 😎