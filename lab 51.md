## Title

 Self Cross-Site Scripting (XSS)  

## Vulnerability Type

Self XSS

## Summary  
In https://kzlabs.com/51.php  is vulnerable to self XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://kzlabs.com/51.php

## Steps to Reproduce  

1. Navigate to the following URL : ```http://kzlabs.com/51.php```
2. Add Payload `<script>alert(1)</sccript>`
3. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

```<script>alert(1)</sccript>```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 

<img width="1920" height="1080" alt="Screenshot From 2026-05-26 00-22-18" src="https://github.com/user-attachments/assets/abb112f4-6cf4-4d95-8670-c190c28599ae" />




 

 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 

 <img width="1920" height="1080" alt="Screenshot From 2026-05-26 00-22-22" src="https://github.com/user-attachments/assets/13a794ef-190c-4229-94c6-f80c623b77b0" />






## Impact
 
 An attacker can perform the following actions using this vulnerability:
  - It allows attackers to hijack user session
  - It potentially leads to full account takeover
  - It allows to perform  unauthorized actions within the vulnerable application
  - It allows attacker to exfiltrate sensitive data
  
## Recommendations for fix

 Validate and sanitize the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

1. Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
2. Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
4. If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
5. Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
