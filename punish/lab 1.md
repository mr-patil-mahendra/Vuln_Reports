## Title

 Reflected Cross-Site Scripting (XSS) via fname Parameter 

## Vulnerability Type

Reflected XSS

## Summary : 
IN https://kzlabs.com/punishment/1.php?fname first name  box is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint


## Steps to Reproduce : 

1. Navigate to the following URL : ```https://kzlabs.com/punishment/1.php?fname=<script>alert(1)<%2Fscript>&lname=```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

```<script>alert(1)</script>```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
  
<img width="1920" height="1080" alt="Screenshot From 2026-05-25 16-13-00" src="https://github.com/user-attachments/assets/38bd5f58-ce62-43f8-9291-fb798e0dcfea" />


 

 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 
 
<img width="1920" height="1080" alt="Screenshot From 2026-05-25 16-13-31" src="https://github.com/user-attachments/assets/63af2781-0ad1-4266-8f8d-7b7d64ff41a8" />


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


