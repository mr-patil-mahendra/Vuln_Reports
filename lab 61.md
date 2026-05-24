## Title

# Stored Cross-Site Scripting (XSS) via My Article Field in Quill

## Vulnerability Type

Stored XSS

## Summary : 
The "Report Name" input field in the Network Reports section does not sanitize or encode user-supplied input before storing it in the database and later rendering it back to users. This means any JavaScript payload entered as a report name gets saved and then executed in the browser of every authenticated user who visits the Reports page — not just the attacker.

## Vulnerable Endpoint
http://kzlabs.com/61.php

Vulnerable Parameter: Report Name field (input field inside the "New Network Report" form)

## Steps to Reproduce : 

1. Log in to the application at `https://kzlabs.com/61.php` with a valid account.
2. Navigate to the Reports tab.
3. Click on + New Network Report.
4. In the Report Name field, enter the following payload: `<img src=x onerror="alert(1)" onclick="confirm(1)" onmouseover="prompt(1)">`
5. Fill in the remaining required fields (Network, Date Range, etc.) and submit the form.
6. Once the report is saved, you are redirected back to the Network Reports listing page.
7. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
8. Every authenticated user who loads this page will trigger the same alert.

## Payload Used

```<img src=x onerror="alert(1)" onclick="confirm(1)" onmouseover="prompt(1)">```

## Proof of Concept Request
  ```Screenshot 1``` — The Reports listing page showing the raw script payload stored as-is in row #7 under "Created By" as `<script>alert(1)</script>`, meaning the app saved it exactly as typed with no filtering at all.

<img width="1920" height="1080" alt="Screenshot From 2026-05-24 15-11-27" src="https://github.com/user-attachments/assets/bd11fc9c-1e9b-4abf-8370-a40bd0674bb3" />




 ```Screenshot 2 : ``` Used an img tag payload `'"><img src=x onerror=a>lert(1)` this time and the alert still triggered on page load, which confirms it's not just script tags that work here. Any HTML payload gets executed.
 
<img width="1920" height="1080" alt="Screenshot From 2026-05-24 15-11-32" src="https://github.com/user-attachments/assets/13ababeb-de7f-46f6-813f-fea44b14cd25" />


 



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
