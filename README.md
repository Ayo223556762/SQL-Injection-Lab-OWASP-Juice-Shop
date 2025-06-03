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

2. Found SQLi Vulnerability
Searched for a product in the Juice Shop search bar using '

Captured the backend request:

sql
GET /rest/products/search?q=
Used Firefox Dev Tools → “Copy as cURL” → converted into raw HTTP request (juice-request.txt)
