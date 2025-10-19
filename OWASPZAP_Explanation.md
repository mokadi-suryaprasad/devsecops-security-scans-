# 🔒 OWASP ZAP — Dynamic Application Security Testing (DAST)

## 🌍 What is OWASP ZAP?

**OWASP ZAP (Zed Attack Proxy)** is a **security testing tool** used to find **vulnerabilities in running web applications**.  
It is developed by the **OWASP (Open Web Application Security Project)** community — a well-known organization for web security standards.

ZAP helps developers and DevOps engineers to check **how secure their application is after it is deployed**.  
It acts like a **real hacker**, sending requests to your app to test for weak points.

---

## 🧠 Why is OWASP ZAP Important?

Even if your code looks safe, your **running application** might still have hidden issues like:
- Weak authentication or login systems  
- Unencrypted communication  
- Leaking sensitive data  
- Insecure cookies  
- Input fields that accept dangerous data (SQL Injection, XSS)

OWASP ZAP helps to **find these real-time issues automatically**, before attackers do.

---

## ⚙️ How OWASP ZAP Works (Step-by-Step)

1. **Run the Application**
   - Your web app should be live or running locally (like `http://localhost:8080` or a testing URL).

2. **Start the ZAP Scan**
   - ZAP sends many HTTP and HTTPS requests to your app.
   - It checks how your app responds to different kinds of input.

3. **Simulate Attacks**
   - ZAP tries **safe attacks** like SQL injection, XSS, CSRF, etc.
   - It doesn’t harm your app, but tests how strong your defenses are.

4. **Collect and Analyze Results**
   - ZAP records the responses and identifies possible security problems.

5. **Generate a Security Report**
   - It produces a detailed **HTML or XML report** showing:
     - Type of issue  
     - URL affected  
     - Severity (Low, Medium, High, Critical)  
     - Fix suggestion  

---

## 🧰 Key Features of OWASP ZAP

| Feature | Description |
|----------|-------------|
| 🔍 **Automatic Scanning** | Scans the application for vulnerabilities without writing any code. |
| 🧠 **Smart Spidering** | Crawls all web pages and forms to test them for security flaws. |
| ⚙️ **Active & Passive Scans** | Passive scans observe traffic, while active scans send attack-like requests. |
| 📊 **Detailed Reports** | Generates visual reports (HTML/XML) for review. |
| 🔄 **CI/CD Integration** | Can be automated using GitHub Actions, Jenkins, or GitLab CI. |
| 🧩 **Free & Open Source** | 100% free tool maintained by OWASP community. |

---

## 🧪 Example Vulnerabilities Detected by ZAP

1. **Cross-Site Scripting (XSS)**  
   - Injecting malicious scripts into web pages.  
   - Example: `<script>alert('Hacked!')</script>`

2. **SQL Injection**  
   - Using SQL queries to access database data.  
   - Example: `' OR '1'='1' --`

3. **Insecure Cookies or HTTP Headers**  
   - Missing “Secure” or “HttpOnly” flags in cookies.  

4. **Sensitive Data Exposure**  
   - Returning passwords or personal data in API responses.  

5. **Broken Authentication**  
   - Weak login pages or unprotected sessions.

---

## 🧩 Example GitHub Workflow — OWASP ZAP Integration

This GitHub Action automatically scans your web application for vulnerabilities after deployment.

```yaml
name: "OWASP ZAP Scan"

on:
  workflow_dispatch:  # Manual trigger
  schedule:
    - cron: '0 0 * * 1'  # Run every Monday

jobs:
  zap_scan:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Run OWASP ZAP Baseline Scan
        uses: zaproxy/action-baseline@v0.12.0
        with:
          target: "http://your-app-url.com"
          rules_file_name: ".zap/rules.tsv"
          cmd_options: "-a"

      - name: Upload ZAP Report
        uses: actions/upload-artifact@v4
        with:
          name: zap-report
          path: zap-report.html
