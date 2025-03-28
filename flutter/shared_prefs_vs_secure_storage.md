# What's the difference between shared preferences and secure storage in Flutter ?

Both **Shared Preferences** and **Flutter Secure Storage** are used for local data storage in Flutter, but they serve different purposes based on security needs.

### **1. Shared Preferences**
- **Package:** [`shared_preferences`](https://pub.dev/packages/shared_preferences)
- **Storage Location:** Stores data in plain text within app storage.
- **Security:** Not encrypted, making it vulnerable to reverse engineering.
- **Use Cases:**
  - Storing non-sensitive user preferences (theme mode, language settings).
  - Saving basic app configurations.

### **2. Secure Storage**
- **Package:** [`flutter_secure_storage`](https://pub.dev/packages/flutter_secure_storage)
- **Storage Location:** Uses platform-specific secure storage:
  - **Android:** EncryptedSharedPreferences or Keystore.
  - **iOS:** Keychain.
- **Security:** Fully encrypted, providing better protection.
- **Use Cases:**
  - Storing authentication tokens, API keys, and passwords.
  - Storing sensitive user data securely.

### **Which One to Use?**
| Feature                | Shared Preferences | Secure Storage |
|------------------------|-------------------|---------------|
| **Encryption**        | ❌ No             | ✅ Yes        |
| **Security Level**    | Low               | High         |
| **Platform-Specific Storage** | No | Yes |
| **Best For**         | Non-sensitive data | Sensitive data |

👉 **Use Shared Preferences** for general app settings.  
👉 **Use Secure Storage** for sensitive data like login tokens.