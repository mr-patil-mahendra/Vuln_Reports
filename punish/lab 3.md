## Title

 Reflected Cross-Site Scripting (XSS) via search Parameter on Help Center Page

## Vulnerability Type

Reflected XSS

## Summary : 
In https://kzlabs.com/punishment/3.php? first name  box is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://kzlabs.com/punishment/3.php?fname=

## Steps to Reproduce : 

1. Navigate to the following URL : ```https://kzlabs.com/punishment/3.php?fname=%3Csvg+onload%3Dalert%281%29%3E&lname=```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

```<svg onload="alert(1)">```

## Proof of Concept Request

  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
  

<img width="1920" height="1080" alt="Screenshot From 2026-05-25 16-40-29" src="https://github.com/user-attachments/assets/946d6ec3-f0cb-4088-a7d6-daa05dabba0e" />



 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 

<img width="1920" height="1080" alt="Screenshot From 2026-05-25 16-40-37" src="https://github.com/user-attachments/assets/fed2d6d9-4725-4eb3-8da0-d656cdc6d6e8" />




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
