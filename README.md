# Cross-Site Scripting (XSS) Vulnerability in Insurance Management System

## Overview
A **Cross-Site Scripting (XSS)** vulnerability was discovered in **Version 1** of the **Insurance Management System** available at [SourceCodester](https://www.sourcecodester.com/php/16995/insurance-management-system-php-mysql.html). This vulnerability allows an attacker to inject arbitrary JavaScript code into certain input fields, leading to the execution of the script when viewed by users or administrators. This can cause broken page layouts and unintended behavior on the platform.

## Vulnerability Details
- **Vulnerability Type**: Stored Cross-Site Scripting (XSS)
- **Affected Product**: Insurance Management System, Version 1
- **CVE ID**: (TBD after MITRE assignment)
- **Vendor**: SourceCodester
- **Impact**: 
  - **End User**: Triggers JavaScript alert and breaks page layout.
  - **Administrator**: Causes page layout to break and shows "1" where content should be.

## Steps to Reproduce

1. **Create a User**: Register a new user on the platform or use an existing user account.
2. **Inject the XSS Payload**:
   - Navigate to the **Support Ticket** section where the "Subject" field is available.
   - In the **"Subject"** field, inject the following XSS payload:
     ```html
     "><script>document.body.innerHTML=<img src=x onerror=alert(1)></script>
     ```
   - Fill in the remaining fields (e.g., description) and submit the form.
3. **Observe the Vulnerability**:
   - **End User**: When a regular user accesses their account and views their ticket history, the injected script will execute, causing the page to break and an alert box with the number "1" to display.
   - **Administrator**: When an administrator views the dashboard or pending support tickets, the page layout may break, and "1" will be displayed where content should be.

## Impact Analysis
- **Confidentiality**: Low. No sensitive information is exposed, but page content is manipulated.
- **Integrity**: Low. While the page layout is altered and alert messages appear, actual data is not modified.
- **Availability**: Medium. The page layout may break, causing disruptions in usability and user experience.

## Affected Component(s)
- **User Input Fields**: Specifically the **"Subject"** field in the support ticket section.
- **Affected Areas**: 
  - User ticket history views.
  - Administrator dashboard and pending ticket views.

## Screenshots of the Vulnerability

### End User - Broken Layout Example
![End User - Broken Layout](https://github.com/CodeByMoriarty/Insurance-Management-System-Stored-Xss/blob/main/admin.png)

### Administrator - Sidebar Broken
![Administrator - Sidebar Broken](https://github.com/CodeByMoriarty/Insurance-Management-System-Stored-Xss/blob/main/admin.png)

## Recommendations for Mitigation
1. **Input Validation**: Sanitize input in all user-submitted fields, especially the "Subject" field, to prevent malicious scripts from being included.
2. **Output Escaping**: Ensure all user-generated content is properly escaped when displayed in HTML contexts to prevent script execution.
3. **Content Security Policy (CSP)**: Implement a strict CSP to disallow inline JavaScript, reducing the attack surface for XSS vulnerabilities.

## Suggested Patch
1. **Sanitize Input**: Use functions like `htmlspecialchars()` in PHP to escape special characters in user inputs.
2. **Escaping Output**: Properly escape and encode user inputs when displaying them in HTML.
3. **Content Security Policy**: Enforce a CSP header to block inline JavaScript.

## References
- [CVE-XXXX-XXXXX](https://www.cve.org) (TBD after MITRE CVE assignment)
- [Proof of Concept (PoC) Repository](https://github.com/CodeByMoriarty/Insurance-Management-System-Stored-Xss)
- [SourceCodester - Insurance Management System](https://www.sourcecodester.com/php/16995/insurance-management-system-php-mysql.html)

## Contact Information
- **Discovered by**: CodeByMoriarty (AndrewL)
- **Email**: [your-email@example.com]

