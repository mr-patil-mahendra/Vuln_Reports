## Title

 Reflected Cross-Site Scripting (XSS) via search Parameter
## Vulnerability Type

Reflected XSS

## Summary : 
In http://kzlabs.com/13.php search parameter is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
http://kzlabs.com/16.php?search=

## Steps to Reproduce : 

1. Navigate to the following URL : ```http://kzlabs.com/16.php?search=%3C%2Fhr%3E%3Cobject+onerror%3D%22alert%281%29%22+data%3Dx%3E```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

``</h2>`<object onerror="alert(1)" data=x>```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
<img width="1920" height="1080" alt="Screenshot From 2026-05-26 05-22-02" src="https://github.com/user-attachments/assets/aa714e3e-8a44-4fbe-9300-565f4a2a9115" />


 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.

<img width="1920" height="1080" alt="Screenshot From 2026-05-26 05-22-09" src="https://github.com/user-attachments/assets/aa1543ce-0e9b-4baa-b26c-0aefeeb3ee23" />

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




