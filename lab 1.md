## Title

 Reflected Cross-Site Scripting (XSS) via fname and lname Parameter 

## Vulnerability Type

Reflected XSS

## Summary  
In https://kzlabs.com/1.php?fname=&lname=  fname and lname paramter is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://kzlabs.com/1.php?fname=&lname=

## Steps to Reproduce  

1. Navigate to the following URL : ```http://kzlabs.com/1.php?fname=%22%3E%3Cscript%3Ealert%28%22Game+OVer+%22+%29+%3C%2Fscript%3E&lname=```
2. Observe that a JavaScript alert box pops up displaying `Game Over` — confirming that the script executed.
   


## Payload Used

```"><script>alert("Game OVer" ) </script>```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 


<img width="1920" height="1080" alt="Screenshot From 2026-05-25 22-28-29" src="https://github.com/user-attachments/assets/4f3a0cfc-5f0d-484e-b5ea-7f98a3298d5f" />

 

 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 


<img width="1920" height="1080" alt="Screenshot From 2026-05-25 22-28-13" src="https://github.com/user-attachments/assets/e61b7041-d42b-4727-b9ef-eab200722138" />



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
