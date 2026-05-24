# Title

 Reflected Cross-Site Scripting (XSS) via search Parameter on Help Center Page

## Vulnerability Type

Reflected XSS

## Summary : 
Equifax Help Center http://kzlabs.com/55.php?search= Search box is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
https://labs.krazeplanet.com/56.php?p=

Steps to Reproduce : 

1. Log in to the application at  https://labs.krazeplanet.com/55.php  with Valid account.
2. Visit the help center of Equifax 
3. Navigate to the following URL : ```https://labs.krazeplanet.com/55.php?search=Game1</script><svg onload="alert(1)">```
4. Observe that an alert box displaying , indicating that the JavaScript code was executed.
{ Screenshot } 

## Payload Used

```Game1</script><svg onload="alert(1)">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
  
 <img width="1914" height="999" alt="Screenshot From 2026-05-24 13-18-24" src="https://github.com/user-attachments/assets/f5899bfb-ead2-460b-90fb-3dbcdcea363a" />
 

 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 
 <img width="1920" height="1080" alt="Screenshot From 2026-05-24 13-23-37" src="https://github.com/user-attachments/assets/9b69a210-b976-48c3-9605-25cfd3eb4864" />
 



## Impact
 
 An attacker can perform the following actions using this vulnerability:
 
  - Admins are affected too since they visit the same page
  - Steal Session Cookies of every user who visit the page
  - Data Exfiltration
  - Once submission hits every authenticated user.
  
## Recommendations for fix:

 Validate and sanitize the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

1. filter all of tags like these: <script>, <img>, <svg>
2. filter all of these methods: alert, confirm, prompt
3. If you're using PHP then use htmlspecialchars() function
4. use cloudflare they have soo many ruls, almost all of xss payload will be blocked automatically
