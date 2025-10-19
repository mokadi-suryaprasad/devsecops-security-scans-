# 🧩 CodeQL — Static Code Analysis (SAST)

## 🔍 What is CodeQL?

**CodeQL** is a **Static Application Security Testing (SAST)** tool created by **GitHub**.  
It helps you **find security vulnerabilities** and **coding errors** in your codebase automatically.

Think of CodeQL as a **database for your code** — it converts your code into a structured format that can be queried like a database.  
You can then write **queries** (or use pre-built ones) to detect issues such as:

- SQL Injection  
- Cross-Site Scripting (XSS)  
- Hardcoded secrets  
- Insecure function usage  
- Unsafe API calls  

---

## ⚙️ How CodeQL Works

1. **Code Scanning Setup**
   - When you push code to GitHub or open a pull request, the **CodeQL workflow** runs automatically.

2. **Code Database Creation**
   - CodeQL analyzes your source code and builds a **CodeQL database** (like a map of your code).

3. **Query Execution**
   - It runs a set of **security queries** against the database.
   - These queries look for common patterns of insecure or bad code.

4. **Results Reporting**
   - The scan results are shown under **GitHub → Security → Code scanning alerts**.
   - You can review and fix the issues directly from GitHub.

---

## 🧰 Languages Supported

CodeQL supports many programming languages, including:
- Java
- JavaScript / TypeScript
- Python
- C / C++
- C#
- Go
- Ruby

---

## 🚀 Benefits of CodeQL

| Feature | Description |
|----------|-------------|
| 🛡️ Security | Detects common vulnerabilities before code is deployed. |
| ⚡ Automation | Runs automatically on every push or pull request using GitHub Actions. |
| 🔎 Custom Rules | You can write your own queries to detect organization-specific risks. |
| 🔁 Integration | Works directly in GitHub with no extra tools required. |

---

## 🧪 Example: What CodeQL Detects

- SQL Injection in a web app.
- Insecure file handling (like reading user files unsafely).
- Hardcoded credentials or API keys.
- Use of deprecated or vulnerable libraries.
- Unsafe data handling between user input and database.

---

## 🧩 Sample GitHub Workflow

```yaml
name: "CodeQL Analysis"

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  schedule:
    - cron: '0 0 * * 0'

jobs:
  analyze:
    name: Analyze code with CodeQL
    runs-on: ubuntu-latest

    permissions:
      actions: read
      contents: read
      security-events: write

    strategy:
      matrix:
        language: [ 'python', 'javascript' ]

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Initialize CodeQL
        uses: github/codeql-action/init@v3
        with:
          languages: ${{ matrix.language }}

      - name: Perform CodeQL Analysis
        uses: github/codeql-action/analyze@v3
