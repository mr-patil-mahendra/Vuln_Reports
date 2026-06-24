## Title

 Reflected Cross-Site Scripting (XSS) via Search parameter

## Vulnerability Type

Reflected XSS

## Summary  
In https://kzlabs.com/1601.php?search=  search paramter is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://kzlabs.com/1601.php?search=

## Steps to Reproduce  

1. Navigate to the following URL : ```https://kzlabs.in/1601.php?search=Game1%3C%2Fscript%3E%3Csvg+onload%3D%22alert%281%29%22%3E```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

```Game1</script><svg onload="alert(1)">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5ffca714-7739-43c4-b985-95b04e136790" />


 
 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7eab845b-41a4-426f-a5cb-744392b0021a" />



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

