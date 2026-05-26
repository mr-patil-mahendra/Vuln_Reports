## Title

  Stored XSS via User Profile Management

## Vulnerability Type

Stored XSS

## Summary  
In http://kzlabs.com/13.php update profile  is vulnerable to Stored XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
http://kzlabs.com/18.php

## Steps to Reproduce  

1. Log in to the application at `https://kzlabs.com/.php` with a valid account.
2. Navigate to the Post a Comment tab.
3. In the Comment field, enter the following payload: `</dir> <script>alert(1)</script>`
4. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
5. Every authenticated user who loads this page will trigger the same alert.
   


## Payload Used

```</dir> <script>alert(1)</script> ```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
<img width="1920" height="1080" alt="Screenshot From 2026-05-26 05-34-40" src="https://github.com/user-attachments/assets/111f9c4a-c9d2-4295-a43c-ecc6c94ae2f8" />

 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
<img width="1920" height="1080" alt="Screenshot From 2026-05-26 05-34-52" src="https://github.com/user-attachments/assets/b7eae8ca-c901-4c72-a199-df412687cdff" />

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




