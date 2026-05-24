## Title

 Reflected Cross-Site Scripting (XSS) via Username Path Injection in Mobile Messaging Endpoint

## Vulnerability Type

Reflected XSS

## Summary : 
The application is vulnerable to Reflected XSS through the username segment in the URL path. User input is reflected unsanitized inside a double-quoted href attribute, allowing an attacker to inject malicious JavaScript that executes automatically when a victim visits a crafted URL.

## Vulnerable Endpoint
http://kzlabs.com/58.php/account/SaturnV/messages

Steps to Reproduce : 

1. Navigate to the following URL : ```http://kzlabs.com/58.php/account/%3Cimg%20src=x%20onerror=%22alert(1)%22%20onclick=%22confirm(1)%22%20onmouseover=%22prompt(1)%22%3E/messages```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.

## Payload Used

```<img src=x onerror="alert(1)" onclick="confirm(1)" onmouseover="prompt(1)">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
  <img width="1920" height="1080" alt="Screenshot From 2026-05-24 14-23-10" src="https://github.com/user-attachments/assets/22d6b34e-7dc4-4596-a1fd-7dc6a9ddcadd" />




 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 <img width="1920" height="1080" alt="Screenshot From 2026-05-24 14-23-14" src="https://github.com/user-attachments/assets/d96ff92f-268a-4a7a-94da-5e7e2eec82da" />

 



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
