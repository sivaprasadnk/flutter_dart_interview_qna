# How to send notifications in Flutter ?

Sending notifications in Flutter can be done in multiple ways, depending on your requirements:

## 🔔 **Local Notifications (On-device, No Internet Required)**
If you want to show notifications locally within the app, use the [`flutter_local_notifications`](https://pub.dev/packages/flutter_local_notifications) package.

### Steps:
1. **Add dependency** in `pubspec.yaml`:
   ```yaml
   dependencies:
     flutter_local_notifications: ^17.0.0
   ```
   
2. **Initialize the plugin** in `main.dart`:
   ```dart
   import 'package:flutter_local_notifications/flutter_local_notifications.dart';

   final FlutterLocalNotificationsPlugin flutterLocalNotificationsPlugin =
       FlutterLocalNotificationsPlugin();

   Future<void> main() async {
     WidgetsFlutterBinding.ensureInitialized();
     
     const AndroidInitializationSettings androidSettings =
         AndroidInitializationSettings('@mipmap/ic_launcher');

     const InitializationSettings settings =
         InitializationSettings(android: androidSettings);

     await flutterLocalNotificationsPlugin.initialize(settings);
     
     runApp(MyApp());
   }
   ```

3. **Show a notification**:
   ```dart
   Future<void> showNotification() async {
     const AndroidNotificationDetails androidDetails = AndroidNotificationDetails(
       'channel_id', 'channel_name',
       importance: Importance.high,
       priority: Priority.high,
     );

     const NotificationDetails details = NotificationDetails(android: androidDetails);

     await flutterLocalNotificationsPlugin.show(
       0,
       'Hello!',
       'This is a test notification.',
       details,
     );
   }
   ```

---

## 📡 **Push Notifications (Firebase Cloud Messaging - FCM)**
If you want to send notifications from a server or cloud, use **Firebase Cloud Messaging (FCM)**.

### Steps:
1. **Add dependencies**:
   ```yaml
   dependencies:
     firebase_core: latest_version
     firebase_messaging: latest_version
   ```

2. **Initialize Firebase** (inside `main.dart`):
   ```dart
   import 'package:firebase_core/firebase_core.dart';
   import 'package:firebase_messaging/firebase_messaging.dart';

   Future<void> main() async {
     WidgetsFlutterBinding.ensureInitialized();
     await Firebase.initializeApp();
     runApp(MyApp());
   }
   ```

3. **Request notification permissions** (for iOS):
   ```dart
   Future<void> requestPermission() async {
     FirebaseMessaging messaging = FirebaseMessaging.instance;
     NotificationSettings settings = await messaging.requestPermission(
       alert: true,
       badge: true,
       sound: true,
     );
     print('Permission granted: ${settings.authorizationStatus}');
   }
   ```

4. **Listen to incoming notifications**:
   ```dart
   FirebaseMessaging.onMessage.listen((RemoteMessage message) {
     print('Received message: ${message.notification?.title}');
   });
   ```

5. **Get FCM Token for sending notifications**:
   ```dart
   Future<void> getToken() async {
     String? token = await FirebaseMessaging.instance.getToken();
     print('FCM Token: $token');
   }
   ```

6. **Send a test notification**:
   - Go to **Firebase Console → Cloud Messaging**.
   - Send a message to your FCM token.

---

### 🔥 **Which One Should You Use?**
- **Local Notifications** → Best for reminders, alarms, or app-generated notifications.
- **Push Notifications (FCM)** → Best for server-triggered messages (e.g., new messages, updates).