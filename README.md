# Vulnerability Assessment: OWASP Juice Shop

## 1. Executive Summary
**Project Type:** Web Application Security Assessment
**Target:** OWASP Juice Shop (Local Docker Instance)
**Tools Used:** Burp Suite Community (Proxy, Intruder, Repeater, Sequencer), Manual Analysis
**Objective:** To identify and exploit OWASP Top 10 vulnerabilities in a modern web application and demonstrate the impact of weak security configurations.

---

## 2. Technical Findings

### Finding 01: Broken Authentication (SQL Injection)
**Severity:** Critical 🔴
**Vulnerability Type:** SQL Injection (SQLi)
**Description:**
The application's login portal fails to properly sanitize user input. By injecting a logical bypass payload into the email field, I was able to alter the backend SQL query and force the database to return a "true" result.

**Proof of Concept:**
* **Vector:** Login Page (`/login`)
* **Payload:** `' OR 1=1 --`
* **Impact:** Successful login as the Administrator (`admin@juice-sh.op`) without a valid password.

**Evidence:**
![SQL Injection Login](SQL-Evidence)

---

### Finding 02: Reflected Cross-Site Scripting (XSS)
**Severity:** High 🟠
**Vulnerability Type:** Reflected XSS
**Description:**
The search function reflects user input directly to the browser (DOM) without proper output encoding. This allows an attacker to inject malicious JavaScript that executes immediately when a victim views the page.

**Proof of Concept:**
* **Vector:** Search Bar
* **Payload:** `<iframe src="javascript:alert(document.cookie)">`
* **Impact:** Execution of arbitrary code, capable of hijacking user sessions.

**Evidence:**
![XSS Alert Box]([LINK TO YOUR XSS SCREENSHOT HERE])

---

### Finding 03: Broken Authentication (Weak Session IDs)
**Severity:** Critical 🔴
**Vulnerability Type:** Insufficient Session ID Entropy
**Description:**
Using Burp Suite Sequencer, I analyzed the randomness of the application's session tokens. The analysis returned a result of "Extremely Poor," indicating that tokens are generated using a predictable pattern.

**Proof of Concept:**
* **Tool:** Burp Sequencer
* **Sample Size:** ~200 Tokens
* **Result:** 0 bits of effective entropy.
* **Impact:** An attacker could mathematically predict valid session tokens and hijack any user's account without interaction.

**Evidence:**
![Sequencer Graph]([LINK TO YOUR SEQUENCER SCREENSHOT HERE])

---

## 3. Reflection
This project demonstrated the critical importance of **Input Validation** and **Secure Randomness**. By combining manual testing with statistical analysis tools like Burp Sequencer, I validated that security flaws often exist both in the visible interface and the invisible logic of the application.
