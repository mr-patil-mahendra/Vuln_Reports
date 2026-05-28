## Title
 Reflected Cross-Site Scripting (XSS) via "s" Parameter on zeals.ai
 
## Vulnerability Type

Reflected XSS

## Summary : 
Zeals.ai has XSS at https://zeals.ai/jp/case/blog/?s=&search_industry=&search_product= . "s"  parameter is vulnerable to reflected XSS . website reflects the User input from p paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://zeals.ai/jp/case/blog/?s=&search_industry=&search_product=

Steps to Reproduce : 
 
1. Navigate to the following URL : ```https://zeals.ai/jp/case/blog/?s=Game1'"><Img Src=X OneRror=alert(1)>&search_industry=&search_product=```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.

## Payload Used

```Game1'"><Img Src=X OneRror=alert(1)>```

## Proof of Concept Request
   

 ```Screenshot 1 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 <img width="1920" height="1080" alt="Screenshot From 2026-05-28 23-48-01" src="https://github.com/user-attachments/assets/d08cc7c5-55af-4f97-90d0-a0fade72049d" />


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
