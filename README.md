# Day-66-100-Days-challenge-in-cybersecurity
# 🛡️ Day 66: File Inclusion Vulnerability (LFI & RFI)

Welcome to Day 66 of my cybersecurity learning journey! Today's focus is on **File Inclusion Vulnerabilities**, a critical flaw in web applications caused by improper handling of user input during dynamic file loading.

## 📖 Overview
At its core, a File Inclusion vulnerability happens because of implicit trust. If an application takes user input (like a URL parameter) and uses it directly to fetch a file without validation, an attacker can manipulate that input to view sensitive files or execute malicious code.

## 🔍 Types of File Inclusion

* **Local File Inclusion (LFI):** The attacker tricks the application into exposing or executing files already present locally on the server (e.g., configuration files, `/etc/passwd`).
* **Remote File Inclusion (RFI):** The attacker forces the web application to download and execute a file from a remote, attacker-controlled server. (Often relies on configurations like `allow_url_include` in PHP).

## 🎯 Attacker's Motivation
1.  **Information Disclosure:** Stealing sensitive data, source code, or database credentials.
2.  **Remote Code Execution (RCE):** Gaining full control over the victim's server via a web shell.
3.  **Denial of Service (DoS):** Overloading the system by forcing it to load massive or critical system files.

## ⚔️ Common Attack Methods
Attackers manipulate URL parameters using specific techniques to bypass basic filters:
* **Directory/Path Traversal (`../`):** Moving up the server's directory tree to escape the web root.
* **Null Byte Injection (`%00`):** Tricking older systems into ignoring required file extensions (e.g., appending `.php`).
* **PHP Wrappers (`php://filter`):** Using built-in protocols to encode files in Base64, allowing the attacker to read the raw source code without the server executing it.

## 🛡️ Practical Prevention Techniques
Defending against file inclusion requires a **Zero Trust** approach to user input:
1.  **Whitelisting (The Gold Standard):** Explicitly define a list of *only* the exact files that are allowed to be included. Reject everything else.
2.  **Avoid Direct File Referencing:** Use indirect references (like mapping IDs to files in the backend) instead of passing file names via URLs (e.g., `?page=1` instead of `?page=about.php`).
3.  **Secure Server Configuration:** Disable dangerous features if they aren't necessary (e.g., setting `allow_url_include = Off` in `php.ini`).

## 🧠 The Defender's Mindset
Security isn't just about breaking things; it's about engineering resilience. Thinking like a defender means anticipating how a feature (like dynamic file loading) can be abused and building strict guardrails *before* the code reaches production.
