## Title

 Reflected Cross-Site Scripting (XSS) via Path Parameter Injection in Comments Endpoint

## Vulnerability Type

Reflected XSS

## Summary  
The application is vulnerable to Reflected XSS through the POST_ID path parameter. User input is reflected unsanitized inside an unquoted HTML attribute, allowing an attacker to inject a new event handler attribute and execute malicious JavaScript when a victim hovers over the affected element.

## Vulnerable Endpoint
```http://kzlabs.com/59.php/svc/shreddit/api/comments/askreddit/t3_u9po1l/t1_i5sxroa```

Steps to Reproduce 

1. Navigate to the following URL : ```http://kzlabs.com/59.php/svc/shreddit/api/comments/askreddit/%3Cimg%20src=x%20onerror=%22alert(1)%22%20onclick=%22confirm(1)%22%20onmouseover=%22prompt(1)%22%3E/t1_i5u8kpl)```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.

## Payload Used

```<img src=x onerror="alert(1)" onclick="confirm(1)" onmouseover="prompt(1)">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
<img width="1920" height="1080" alt="Screenshot From 2026-05-24 14-37-29" src="https://github.com/user-attachments/assets/971514c8-1b1f-4ed8-b892-faf58c6d79e8" />




 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.

 <img width="1920" height="1080" alt="Screenshot From 2026-05-24 14-37-33" src="https://github.com/user-attachments/assets/cb7e3eb3-ff59-4d9b-a734-e14f08e479a6" />




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
