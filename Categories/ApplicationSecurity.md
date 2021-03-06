# Application / Web Application Security

### Describe the last program or script that you wrote. What problem did it solve? 

### How would you implement a secure login field on a high traffic website where performance is a consideration? 

The answer you’re looking for here is that TLS is a must for the entire site at this point, and that there are very few situations where you shouldn’t insist on encryption. 

### What are the various ways to handle account brute forcing? 

account lockouts, IP restrictions, fail2ban, commercial versions thereof, etc. 

### What is XSS, stored XSS, reflected XSS and DOM-based XSS?

**XSS:** injects malicious code into a vulnerable web application. XSS differs from other web attack vectors (e.g., SQL injections), in that it does not directly target the application itself. Instead, the users of the web application are the ones at risk. 

**Stored XSS:** also known as persistent XSS, is the more damaging of the two. It occurs when a malicious script is injected directly into a vulnerable web application. Stored Cross-site scripting vulnerabilities happens when the payload is saved, for example in a database and then is executed when a user opens the page. Stored cross-site scripting is very dangerous for a number of reasons: 

**Reflected XSS:** Reflected XSS involves the reflecting of a malicious script off of a web application, onto a user’s browser. The script is embedded into a link, and is only activated once that link is clicked on. A reflected XSS vulnerability happens when the user input from a URL or POST data is reflected on the page without being stored. This means that an attacker has to send a crafted link or post form to the victim to insert the payload, and the victim should click the link. This kind of payload is also generally being caught by built in browser XSS filters, like in Chrome, Internet Explorer or Edge. 

**DOM-based XSS:** an advanced type of XSS attack which is made possible when the web application’s client side scripts write user provided data to the Document Object Model (DOM). The data is subsequently read from the DOM by the web application and outputted to the browser. If the data is incorrectly handled, an attacker can inject a payload, which will be stored as part of the DOM and executed when the data is read back from the DOM. 



`<img scr=””>` will often load content from other websites, making a cross-origin HTTP request. 

### How would you hunt for XSS?

#### Follow up: Give me an example of XSS and what you can do with it.

### Prevention on XSS 

Input Validation and Output Sanitization, with focus on the latter. 

XSS can be prevented by the use of the proper available sanitizers. Web developers have to have an eye on the gateways through which they receive information and these are the gateways which must be made as a barrier for malicious files. 

There are software or applications available for doing this, like the XSS Me for Firefox and DOM snitch for Google Chrome. Also, the default web application firewall formula, popularly 

In addition, a strong CSP provides an additional layer of protection against XSS.

### What is CSP (Content Security Policy) ?

### Cross-Site Request Forgery CSRF

#### What is CSRF?

#### How does one defend against CSRF? 

Nonce required by the server for each page or each request is an accepted, albeit not foolproof, method. 

When CSRF attacks, you can opt for two available methods. 

Firstly, with every request try to include a random token. In this way a unique string of tokens will be generated which is a good safeguard. 

Secondly, for each field of form, try using different names. This will somewhat help you in becoming anonymous due to the entry of so many different names and thus will behave as a safeguard from CSRF attacks. 

In addition, consider Same-Site Cookie for preventing CSRF attacks.

### What is SSRF Server Side Request Forgery?

### What is SQL Injection? Give me an example.

#### Follow up:
1. SQL Injection prevention
2. What is blind SQL Injection?

### HTTP Related

#### What’s the difference between HTTP and HTML? 

One is the networking/application protocol and the other is the markup language 

#### How does HTTP handle state? 

It doesn’t. Not natively. Good answers are things like “cookies”, but the best answer is that cookies are a hack to make up for the fact that HTTP doesn’t do it itself. 

#### HTTP Public Key Pinning

(HPKP)

Deprecated by Google Chrome

#### Cookies 

httponly - cannot be accessed by javascript.

#### SQLi 

(Wo)man in the browser (flash / java applets) (malware).

Validation / sanitisation of webforms.

#### POST 

Form data. 

#### GET 

Queries. 

Visible from URL.

### What is Exfiltration? Data Exfiltration 

Infiltration is the method by which you enter or smuggle elements into a location. Exfiltration is just the opposite: getting sensitive information or objects out of a location without being discovered. In an environment with high security, this can be extremely difficult but not impossible. Again we turn to our friends in the fake delivery uniforms wandering around the building, and see that yes there are ways to get in and out without a lot of issues. 

Data exfiltration or Data extrusion is the unauthorized transfer of data from a computer. The transfer of data can be manual by someone with physical access to the computer or automated, carried out through malware over a network. Because data routinely moves in and out of networked enterprises, data exfiltration can closely resemble normal network traffic, making detection of exfiltration attempts challenging for IT security groups. 

### What is SOP (Same-origin policy)?

Only accept requests from the same origin domain. 

### What is CORS (Cross-origin resource sharing)?

Cross-Origin Resource Sharing. Can specify allowed origins in HTTP headers. Sends a preflight request with options set asking if the server approves, and if the server approves, then the actual request is sent (eg. should client send auth cookies).

### What is SRI (Sub-Resource Integrity)?

### Buffer Overflow

#### How does a buffer overflow work? 

#### How can one defend against buffer overflows? 

### Directory traversal 

Find directories on the server you’re not meant to be able to see.

There are tools that do this.

How to prevent?

### APIs 

Think about what information they return. 

And what can be sent.

### Beefhook

Get info about Chrome extensions.

### User agents

Is this a legitimate browser? Or a botnet?

### Browser extension take-overs

Miners, cred stealers, adware.

### Local file inclusion

### Remote file inclusion (not as common these days)

### Web vuln scanners. 

### SQLmap.

### Malicious redirects.