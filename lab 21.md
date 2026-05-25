## Title

Stored XSS via Subject and Description Create Support Ticlet System 

## Vulnerability Type

Stored XSS

## Summary : 

The application is vulnerable to Stored Cross-Site Scripting (XSS) through the  Create Support Ticlet System field. User-supplied HTML is stored without sanitization and rendered using innerHTML, allowing an attacker to inject malicious JavaScript that executes when users view the affected article page.

## Vulnerable Endpoint
http://kzlabs.com/21.php

Vulnerable Parameter:  Create Support Ticlet System

## Steps to Reproduce : 

1. Log in to the application at `https://kzlabs.com/21.php` with a valid account.
2. Navigate to the My Article tab.
3. Click on + Write article .
4. In the Body (html) field, enter the following payload: `Video and Audio Payloads <video onload="alert(2)" controls>`
5. Fill in the remaining required fields (Title, Tag, etc.) and submit the form.
6. Once the report is saved, you are redirected back to the article  listing page.
7. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
8. Every authenticated user who loads this page will trigger the same alert.

## Payload Used

```Video and Audio Payloads <video onload="alert(2)" controls>```

## Proof of Concept Request
  ```Screenshot 1``` — The Reports listing page showing the raw script payload stored as-is in row #7 under "Created By" as `<script>alert(1)</script>`, meaning the app saved it exactly as typed with no filtering at all.

<img width="1920" height="1080" alt="Screenshot From 2026-05-25 23-32-14" src="https://github.com/user-attachments/assets/9a0d4c8e-8785-4602-9cc8-562b978ecf62" />





 ```Screenshot 2 : ``` Used an img tag payload `'"><img src=x onerror=a>lert(1)` this time and the alert still triggered on page load, which confirms it's not just script tags that work here. Any HTML payload gets executed.
 <img width="1920" height="1080" alt="Screenshot From 2026-05-25 23-33-17" src="https://github.com/user-attachments/assets/afd47a00-2fd6-4b23-97eb-00971a94507a" />



 



## Impact
 
 An attacker can perform the following actions using this vulnerability:
 
- Steal session cookies of every user who visits the page
- Admins are affected too since they visit the same page
- Can inject fake login forms to harvest credentials
- One submission hits every authenticated user
  
## Recommendations for fix:

 Validate and sanitize the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

1. Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
2. Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
4. If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
5. Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
