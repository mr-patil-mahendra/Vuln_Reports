## Title

 Reflected Cross-Site Scripting (XSS) via "p"  Parameter on Pubg-Community Feed

## Vulnerability Type

Reflected XSS

## Summary  
Pubg-Community Feed  http://kzlabs.com/56.php?p= Search box is vulnerable to reflected XSS . website reflects the User input from p paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://labs.krazeplanet.com/56.php?p=

Steps to Reproduce  
 
1. Navigate to the following URL : ```http://kzlabs.com/56.php?p=Game1%27%3E%3Cimg+src%3Da+onerror%3Dalert%28document.cookie%29%3E```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.

## Payload Used

```Game1'><img src=a onerror=alert(document.cookie)>```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
<br> <br>
<img width="1920" height="1080" alt="Screenshot From 2026-05-24 13-53-56" src="https://github.com/user-attachments/assets/a4dfe522-1f25-4e87-8eab-bb1c5733a619" />

  
 

 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 
 <img width="1920" height="1080" alt="Screenshot From 2026-05-24 13-54-03" src="https://github.com/user-attachments/assets/7d07baf0-1c60-4c99-adc7-0f3aa57e5f62" />




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

