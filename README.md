# 🔐 HTTPS vs HTTP — Cryptographic Failures Demo

## 📚 Table of Contents
1. [Description](#-description)  
2. [Project Purpose and Requirements](#-project-purpose-and-requirements)  
3. [Tests by Operating System](#-tests-by-operating-system)  
4. [Test 2: Password Hashing with bcrypt](#-test-2-password-hashing-with-bcrypt)  
5. [Conclusions](#-conclusions)

---

## 🧩 Description
This project analyzes the difference between HTTP and HTTPS from a cryptographic security perspective.  
Through practical tests, it demonstrates how HTTPS protects data confidentiality and integrity via TLS encryption, while HTTP transmits information in plain text.  
Additionally, it includes a demonstration of bcrypt for secure password storage, highlighting best practices in both local and browser environments.

---

## 🧭 Project Purpose and Requirements
This repository aims to visualize common cryptographic failures and good security practices in data transmission and password management.

**Requirements**
- Basic knowledge of terminal or command line.
- Internet connection to perform network tests.
- Optional: Git installed for version control.

---

## ⚙️ Tests by Operating System

### 🐧 Linux (Debian/Ubuntu)

#### Install tools
```bash
sudo apt update
sudo apt install curl openssl -y
```

#### Create docs directory
```bash
mkdir -p docs
```

#### Test 1: HTTP request (unencrypted)
```bash
curl -v http://httpbin.org/get -o docs/http-linux.txt
```
The output file `http-linux.txt` will contain readable JSON data — transmitted without encryption.

#### Test 2: HTTPS request (encrypted)
```bash
curl -v https://httpbin.org/get -o docs/https-linux.txt
```
The output file `https-linux.txt` will contain the same JSON data, but transmitted securely through TLS, preventing interception or tampering.

#### Optional: Compare both outputs
```bash
diff docs/http-linux.txt docs/https-linux.txt
```

---

### 🍎 macOS (Homebrew)

#### Install tools
```bash
brew install curl openssl
```

#### Create docs directory
```bash
mkdir -p docs
```

#### Test 1: HTTP request (unencrypted)
```bash
curl -v http://httpbin.org/get -o docs/http-macos.txt
```
The file `http-macos.txt` will display readable JSON data, indicating unencrypted transmission.

#### Test 2: HTTPS request (encrypted)
```bash
curl -v https://httpbin.org/get -o docs/https-macos.txt
```
The file `https-macos.txt` will show the same content securely transmitted via TLS.

#### Optional: Compare both outputs
```bash
diff docs/http-macos.txt docs/https-macos.txt
```

---

### 🪟 Windows (PowerShell with Chocolatey)

#### Install tools
```bash
choco install curl openssl
```

> If you don’t have **Chocolatey**, you can manually download:  
> - [Download curl](https://curl.se/windows/)  
> - [Download OpenSSL](https://slproweb.com/products/Win32OpenSSL.html)

#### Create docs directory
```bash
mkdir docs
```

#### Test 1: HTTP request (unencrypted)
```bash
curl -v http://httpbin.org/get -o docs/http-windows.txt
```
The file `http-windows.txt` will contain visible JSON data — proof of unencrypted communication.

#### Test 2: HTTPS request (encrypted)
```bash
curl -v https://httpbin.org/get -o docs/https-windows.txt
```
The file `https-windows.txt` will show encrypted negotiation logs, ensuring secure data exchange.

#### Optional: Compare both outputs
```bash
fc docs\http-windows.txt docs\https-windows.txt
```

---

## 🔐 Test 2: Password Hashing with bcrypt (Python)

### Install required library
```bash
pip install bcrypt
```

### Create the Python script `bcrypt_demo.py`
```python
import bcrypt

# User-provided password
password = input("Enter your password: ").encode('utf-8')

# Generate salt and hash
salt = bcrypt.gensalt()
hashed = bcrypt.hashpw(password, salt)

print(f"\n🔐 Hashed password:\n{hashed.decode()}")

# Verify password
check = input("\nRe-enter your password to verify: ").encode('utf-8')
if bcrypt.checkpw(check, hashed):
    print("✅ Password match — hash verified.")
else:
    print("❌ Password mismatch — verification failed.")
```

### Run the test
```bash
python bcrypt_demo.py
```

**Result**
- Prompts for a password.  
- Generates a secure salted hash using bcrypt.  
- Allows verification by re-entering the password.  

**Key takeaway:**  
The generated hash is non-reversible — even if an attacker steals it, they cannot recover the original password.

---

## 🧠 Conclusions
- **HTTP** exposes data in transit — vulnerable to sniffing and manipulation.  
- **HTTPS** encrypts communication — ensuring confidentiality and integrity.  
- **bcrypt** reinforces local security by hashing credentials before storage.  

Together, these examples highlight the essential difference between secure transmission and secure storage.
