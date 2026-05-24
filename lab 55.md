# Title

 Reflected Cross-Site Scripting (XSS) via search Parameter on Help Center Page

## Vulnerability Type

Reflected XSS

## Summary : 
Equifax Help Center http://kzlabs.com/55.php?search= Search box is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://labs.krazeplanet.com/56.php?p=

Steps to Reproduce : 

1. Log in to the application at  https://labs.krazeplanet.com/55.php  with Valid account.
2. Visit the help center of Equifax 
3. Navigate to the following URL : ```https://labs.krazeplanet.com/55.php?search=Game1</script><svg onload="alert(1)">```
4. Observe that an alert box displaying , indicating that the JavaScript code was executed.
{ Screenshot } 

## Payload Used

```Game1</script><svg onload="alert(1)">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
  
 <img width="1914" height="999" alt="Screenshot From 2026-05-24 13-18-24" src="https://github.com/user-attachments/assets/f5899bfb-ead2-460b-90fb-3dbcdcea363a" />
 

 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 
 <img width="1920" height="1080" alt="Screenshot From 2026-05-24 13-23-37" src="https://github.com/user-attachments/assets/9b69a210-b976-48c3-9605-25cfd3eb4864" />
 



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


