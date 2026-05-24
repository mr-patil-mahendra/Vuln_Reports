## Title

 Reflected Cross-Site Scripting (XSS) Open Redirect via returnTo Parameter in Account Confirmation End

## Vulnerability Type

Reflected XSS

## Summary : 
The returnTo parameter is vulnerable and Open Redirect due to improper input validation. An attacker can inject a javascript: URI or external URL, leading to JavaScript execution or redirection to a malicious website when a user clicks the Continue button.

## Vulnerable Endpoint
https://labs.krazeplanet.com/57.php?returnTo=

Steps to Reproduce : 


1. Navigate to the following URL : ```http://kzlabs.com/57.php?returnTo=javascript:alert(document.cookie)```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.


## Payload Used

```javascript:alert(document.cookie)```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
  
 <img width="1920" height="1080" alt="Screenshot From 2026-05-24 14-04-09" src="https://github.com/user-attachments/assets/7fcc45d6-dd2e-4b7f-a137-bff358d3ee00" />


 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 <img width="1920" height="1080" alt="Screenshot From 2026-05-24 14-04-16" src="https://github.com/user-attachments/assets/fb768b05-f7b7-4131-8546-3d54ada88947" />

 



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

