## Title

 Reflected Cross-Site Scripting (XSS) via search Parameter on Help Center Page

## Vulnerability Type

Reflected XSS

## Summary 
In http://kzlabs.com/punishment/17.php ptu parameter is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
http://kzlabs.com/punishment/17.php?ptu=

## Steps to Reproduce 

1. Navigate to the following URL : ```http://kzlabs.com/punishment/17.php?ptu=%3Cimg%20src=x%20onerror=%22alert(1)%22%3E```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

```<img src=x onerror="alert(1)">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 

<img width="1920" height="1080" alt="Screenshot From 2026-05-25 21-35-10" src="https://github.com/user-attachments/assets/5add55af-dff2-4587-93f2-bb7d03941e6f" />


 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
<img width="1920" height="1080" alt="Screenshot From 2026-05-25 21-35-17" src="https://github.com/user-attachments/assets/f7db6871-207a-4055-be9c-1d3f5cb1750b" />




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


