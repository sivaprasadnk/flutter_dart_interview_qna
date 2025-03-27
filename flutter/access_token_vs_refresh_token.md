# **Access Token vs Refresh Token**

Access tokens and refresh tokens are both used in authentication and authorization mechanisms, primarily in OAuth 2.0 and OpenID Connect. They serve different purposes in securing API access.

---

### **1. Access Token**
🔹 **Purpose**:  
- Used to access protected resources (APIs, user data, etc.).  
- Sent with each request to authenticate the user/session.

🔹 **Characteristics**:  
- Short-lived (e.g., 15 minutes to 1 hour) for security reasons.  
- Usually a **JWT (JSON Web Token)** containing user claims/permissions.  
- Can be stored in memory, local storage, or a secure cookie.

🔹 **How It Works**:  
1. The user logs in and receives an **access token** from the authentication server.
2. The access token is included in API requests (usually in the `Authorization` header as `Bearer <token>`).
3. If the token is valid, the server allows access to resources.

🔹 **Security Concern**:  
- If stolen, it can be misused until it expires.
- Should not be stored in insecure locations like local storage.

---

### **2. Refresh Token**
🔹 **Purpose**:  
- Used to obtain a new access token **without requiring the user to log in again**.

🔹 **Characteristics**:  
- Long-lived (can last days, weeks, or even months).  
- **Not included in API requests** (only used to get a new access token).  
- Usually **stored securely** (e.g., in HTTP-only cookies).

🔹 **How It Works**:  
1. The user logs in and gets **both an access token and a refresh token**.
2. When the access token expires, the client sends the refresh token to the server.
3. If the refresh token is valid, the server issues a **new access token**.
4. This process continues until the refresh token expires or is revoked.

🔹 **Security Concern**:  
- If compromised, an attacker can continuously get new access tokens.
- Should always be stored securely (e.g., HTTP-only cookies, secure storage).

---

### **Comparison Table**
| Feature           | Access Token | Refresh Token |
|------------------|-------------|--------------|
| **Purpose**      | Access APIs  | Get a new access token |
| **Lifetime**     | Short-lived  | Long-lived |
| **Usage**        | Sent with every API request | Used only to refresh access token |
| **Storage**      | Memory, secure storage | HTTP-only cookies, secure storage |
| **Security Risk** | If stolen, can be used for API access until expiration | If stolen, attacker can generate new access tokens |

---

### **Which One to Use?**
- **Use access tokens** for API authorization.
- **Use refresh tokens** to maintain user sessions without requiring frequent logins.

### **Best Practices**
✅ Store **access tokens in memory** (not local storage) to reduce XSS risks.  
✅ Store **refresh tokens in HTTP-only cookies** to prevent client-side access.  
✅ Implement **token rotation** (issue a new refresh token along with a new access token).  
✅ Set an **expiration** and **revoke refresh tokens** on logout or inactivity.  
✅ Use **short expiration times** for access tokens to limit security risks.  

