## Title

 Reflected Cross-Site Scripting (XSS) via search Parameter on Help Center Page

## Vulnerability Type

Reflected XSS

## Summary : 
In http://kzlabs.com/punishment/22.php color parameter is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
http://kzlabs.com/punishment/22.php?color=

## Steps to Reproduce : 

1. Navigate to the following URL : ```http://kzlabs.com/punishment/22.php?color=%3CImg%20src=x%20onerror=%22eval(%27\x61\x6c\x65\x72\x74(1)%27)%22%3E```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

```<Img src=x onerror="eval('\x61\x6c\x65\x72\x74(1)')">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
  
 <img width="1920" height="1080" alt="Screenshot From 2026-05-25 22-12-03" src="https://github.com/user-attachments/assets/2089a493-c4f1-4634-ae7b-61ef44d93f10" />


 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 
<img width="1920" height="1080" alt="Screenshot From 2026-05-25 22-12-18" src="https://github.com/user-attachments/assets/db88496f-4b62-4486-afa1-9e816452d9c2" />



## Impact
 
 An attacker can perform the following actions using this vulnerability:
  - It allows attackers to hijack user session
  - It potentially leads to full account takeover
  - It allows to perform  unauthorized actions within the vulnerable application
  - It allows attacker to exfiltrate sensitive data
  
## Recommendations for fix:

 Validate and sanitize the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

1. Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
2. Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
4. If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
5. Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server


