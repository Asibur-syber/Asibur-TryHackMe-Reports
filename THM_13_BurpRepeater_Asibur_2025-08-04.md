# 🛡 Web Application Penetration Test Report  
**Client:** TryHackMe – Burp Suite Repeater Lab (Educational)  
**Project:** Burp Suite Repeater – HTTP Header Manipulation Test  
**Date:** August 4, 2025  
**Version:** 1.0  
**Prepared by:** Asibur Rahaman  
**Title:** Ethical Hacker & Cybersecurity Specialist  
**Contact:** asib51639@gmail.com | [GitHub](https://github.com/Asibur-syber) | [LinkedIn](https://linkedin.com/feed)  

---

## 📌 Executive Summary
This penetration test identified a **Medium Risk vulnerability** within the tested application:  
the ability to bypass access control by adding a specific HTTP header using **Burp Suite Repeater**.  

While this lab environment was educational, in a real-world scenario such a weakness could allow  
attackers to access restricted data, bypass authentication, and compromise sensitive assets.  

**Overall Risk Level:** 🟨 Medium (CVSS v3.1 Base Score: 6.5)  
**Business Impact:** Unauthorized data exposure, compliance violations, and reputational damage.

---

## 📜 Scope & Limitations
- **Scope:**  
  - IP: `10.201.6.12`  
  - Application: Web-based HTTP service  
- **Limitations:**  
  - Testing performed in a safe, non-production TryHackMe environment.  
  - No brute force, fuzzing, or destructive testing.

---

## 📊 Findings Table

| ID  | Vulnerability                          | CVSS Score | Risk Level | Evidence       | Fix Time |
|-----|----------------------------------------|------------|-----------|----------------|----------|
| 01  | Header-based access control bypass     | 6.5        | 🟨 Medium | Screenshot #5  | 1-2 Days |

---

## 🔍 Vulnerability Analysis

**Description:**  
The application relies on client-side validation and fails to enforce proper server-side access control.  
By adding a custom header `FlagAuthorised: True`, an attacker can access restricted content.  

**Proof of Concept Steps:**  
1. Intercept HTTP request using **Burp Suite Proxy**.  
2. Send request to **Repeater**.  
3. Add header: `FlagAuthorised: True`.  
4. Forward the request and review the server’s response.  
5. Sensitive data (flag) is disclosed in the HTTP response body.

---

## 💡 Business Impact
If present in a production environment, this vulnerability could:
- Allow unauthorized access to sensitive data.
- Bypass authentication checks entirely.
- Lead to regulatory non-compliance (GDPR, HIPAA, PCI-DSS).

---

## 🛠 Tools & Techniques Used
- **Burp Suite Proxy** – Intercepting HTTP traffic.  
- **Burp Suite Repeater** – Modifying and resending requests.  
- **Burp Inspector** – Editing HTTP headers.  
- **Firefox Browser** – Accessing the target lab environment.

---

## 🖼 Proof & Screenshots

**Screenshot 1 – Target Website Opened in Browser**  
![Screenshot 1](https://i.imgur.com/rHzDLar.jpeg)

**Screenshot 2 – HTTP Request Captured in Proxy**  
![Screenshot 2](https://i.imgur.com/Lf37GO4.jpeg)

**Screenshot 3 – Request Sent to Repeater (Unmodified)**  
![Screenshot 3](https://i.imgur.com/2ruMhe7.jpeg)

**Screenshot 4 – Header Added in Inspector**  
![Screenshot 4](https://i.imgur.com/6sWlTR8.jpeg)

**Screenshot 5 – Flag Shown in Response**  
![Screenshot 5](https://i.imgur.com/tP244C7.jpeg)

---

## 🩹 Remediation Recommendations
1. Implement **server-side validation** for all authentication and authorization checks.  
2. Reject unauthorized headers from client-side requests.  
3. Use **role-based access control (RBAC)** to enforce permissions.  
4. Conduct regular **security code reviews** and penetration tests.

---

## ⚠ Visual Risk Matrix

| Likelihood ↓ \ Impact → | Low  | Medium | High  |
|--------------------------|------|--------|-------|
| Low                      | 🟩   | 🟨     | 🟧    |
| Medium                   | 🟨   | 🟧     | 🟥    |
| High                     | 🟧   | 🟥     | 🟥    |

**Overall Risk:** 🟨 Medium

---

## 📚 References
- [Burp Suite Official Documentation](https://portswigger.net)  
- [OWASP Access Control Cheat Sheet](https://owasp.org)  
- [CVSS v3.1 Calculator](https://www.first.org/cvss/calculator/3.1)  

---

## 📑 Fiverr Delivery Note (Cover Letter)

Hello **TryHackMe – Burp Suite Repeater Lab (Educational)**,

Thank you for choosing my penetration testing service.  
Please find attached the **Web Application Penetration Test Report** for your project.  
The report includes:

- Detailed vulnerability analysis  
- CVSS risk scoring  
- Screenshots as proof of exploitation  
- Actionable remediation steps  

**Next Steps:**  
I recommend implementing the provided fixes immediately to ensure your application remains secure.  
If you need assistance with remediation or re-testing, I would be happy to help.

Thank you,  
**Asibur Rahaman**  
Ethical Hacker & Cybersecurity Specialist
