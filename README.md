# Insurance-Management-System-Stored-Xss

A Cross-Site Scripting (XSS) vulnerability was discovered in Version 1 of the Insurance Management System available at SourceCodester. This vulnerability allows an attacker to inject arbitrary JavaScript code into certain input fields, leading to the execution of the script when viewed by users or administrators. This results in broken page layouts and unintended behavior on the platform.
Vulnerability Details:
1.	Affected Product: Insurance Management System, Version 1 (SourceCodester)
2.	Vulnerability Type: Stored Cross-Site Scripting (XSS).
3.	Exploitability: The attacker can inject JavaScript through the "Subject" field when creating or modifying records.
4.	Impact:
o	End User Impact: When a regular user accesses their account or views certain records, the injected JavaScript causes an alert to be triggered (showing "1") and can break the page layout.
o	Administrator Impact: When an administrator views the dashboard or any records containing the injected content, the page elements (such as the sidebar or pending tickets) may break, and "1" may be displayed where content should be.
Steps to Reproduce:
1.	Create a User: Register a new user on the platform or use an existing user account.
2.	Inject the XSS Payload:
o	Navigate to a section where the "Subject" field is available (such as creating or modifying a record).
o	In the "Subject" field, inject the following XSS payload:
"><script>document.body.innerHTML=<img src=x onerror=alert(1)></script>
o	Fill in the remaining fields and submit the form.
3.	Observe the Vulnerability:
o	End User: When the user accesses their account and views their records, the injected script will execute, causing a broken page and displaying an alert ("1").
o	Administrator: When an administrator accesses the dashboard or pending records, the page will break, displaying "1" or malfunctioning elements (such as the sidebar).
Impact:
•	Confidentiality: Low. No sensitive information is exposed, but the attacker can manipulate the page content.
•	Integrity: Low. The attacker alters the page layout and triggers alerts, but does not modify actual data.
•	Availability: Medium. The vulnerability causes page elements to break or behave unexpectedly, potentially affecting usability.
Vulnerable Component:
•	Component: The user input fields, particularly the "Subject" field, are not properly sanitized.
•	Affected Areas:
o	User account views.
o	Administrator dashboard and pending records display.
Mitigation/Recommendations:
•	Input Validation: Implement proper input sanitization to prevent the inclusion of malicious scripts in user-submitted fields, such as the "Subject" field.
•	Output Escaping: Ensure all user-generated content is properly escaped when displayed in HTML contexts to prevent code execution.
•	Content Security Policy (CSP): Enforce a strict Content Security Policy to restrict inline JavaScript execution, reducing the risk of XSS attacks.
Suggested Patch:
•	Sanitization: Apply sanitization techniques (such as removing or encoding script tags) to all user input fields.
•	Escaping Output: Ensure that any user-generated content is correctly escaped when displayed in HTML (using functions like htmlspecialchars() in PHP or equivalent methods in other languages).
•	CSP Implementation: Configure a CSP that disallows inline JavaScript, helping mitigate XSS vulnerabilities.

