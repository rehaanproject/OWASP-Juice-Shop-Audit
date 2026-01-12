# OWASP Juice Shop: Manual Security Assessment 🛡️

## Project Overview
This repository documents a manual security assessment of **OWASP Juice Shop**, a modern web application designed with intentional security flaws. The goal was to identify, exploit, and document **OWASP Top 10** vulnerabilities using **Burp Suite** and manual testing techniques.

## Key Findings 🕵️‍♂️
* **SQL Injection (SQLi):** Bypassed authentication to gain administrative access by manipulating backend SQL queries.
* **Reflected Cross-Site Scripting (XSS):** Executed arbitrary JavaScript in the victim's browser via the search function.
* **Broken Authentication:** Discovered weak session ID entropy using **Burp Sequencer**, proving that session tokens were predictable and vulnerable to hijacking.

## Tools Used 🛠️
* **Burp Suite Community Edition:**
    * **Proxy:** For intercepting and analyzing traffic.
    * **Repeater:** For manual request manipulation.
    * **Intruder:** For brute-forcing administrative passwords.
    * **Sequencer:** For statistical analysis of session tokens.
    * **Decoder:** For analyzing encoded data formats.
