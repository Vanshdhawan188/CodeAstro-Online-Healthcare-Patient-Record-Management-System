# 🚨 Stored XSS Vulnerability in Online Healthcare Patient Record Management (CodeAstro)

A critical **Stored Cross-Site Scripting (XSS)** vulnerability was discovered in the **Report** section of the Online Healthcare Patient Record Management system by **CodeAstro**.

Attackers can inject malicious JavaScript via the `Patient Name` field (POST parameter), which gets persistently stored in the database and executed whenever the report page is viewed.

---

## 🔍 Key Details

| Property             | Value                                                                 |
|----------------------|------------------------------------------------------------------------|
| **Affected Vendor**  | CodeAstro                                                              |
| **Vulnerable Section** | Report Generation of Patients                                         |
| **Attack Vector**    | `Patient Name` and `Impression By` POST parameters                     |
| **Vulnerability**    | Stored Cross-Site Scripting (XSS)                                      |
| **Version Affected** | 1.0                                                                    |
| **Official Website** | [CodeAstro PRMS](https://codeastro.com/patient-record-management-system-in-php-mysql-with-source-code/) |

---

## 🧪 Proof of Concept (PoC)

### Step-by-Step Exploitation

1. **Login to the Application**

   - Navigate to the login portal:
     ```
     http://localhost/PRMS-php/
     ```
   - Log in using valid credentials.
   - ![image](https://github.com/user-attachments/assets/dcd5289f-7fd8-423b-b5f5-cccea6456001)


2. **Inject XSS Payload in Patient Name Field**

   - Go to **Generate Record**.
   - Select any existing report → Click "New".
   - In the **"Patient Name"** and **"Name"** input fields, insert the following payload:
     ```html
     <script>alert(1)</script>
     ```
   - Click **Submit**.
![image](https://github.com/user-attachments/assets/245f1a08-d265-458d-94f4-25a3eb8d20d3)
![image](https://github.com/user-attachments/assets/283d2973-999d-4781-8b9a-091859a71c20)


3. **Trigger the Payload**

   - View the submitted report.
   - A JavaScript `alert(1)` will be triggered.
   - The payload also executes for any **employee or admin** viewing the report.
![image](https://github.com/user-attachments/assets/e57d495c-dcda-4c26-b608-b7c5adb3689c)
![image](https://github.com/user-attachments/assets/fe91b7d7-9bf3-4354-b1c3-a1d76a1e7031)


---

## 🛑 Potential Impact

- 🔐 **Session Hijacking** – Steal session cookies using `document.cookie`.
- 🎣 **Phishing** – Display fake forms to collect user credentials.
- 🖼️ **Defacement** – Modify website appearance or display fake content.
- 📤 **Data Exfiltration** – Steal sensitive data via background HTTP requests.
- 🦠 **Malware Propagation** – Redirect users to malicious external websites.
- 🔓 **Privilege Escalation** – Leverage stored scripts to gain unauthorized access.

---

## ✅ Mitigation Strategies

### 🔒 Input Sanitization

Sanitize user input server-side:

```php
$input = htmlspecialchars($_POST['patient_name'], ENT_QUOTES, 'UTF-8');
```

## 🧑‍💻 Authors

     Subhash Paudel

     Vansh Dhawan

📅 Reported On: 2025-06-18

🛡️ Severity: High
