# ZAP Scanning Report

ZAP by [Checkmarx](https://checkmarx.com/).


## Summary of Alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 7 |
| Medium | 5 |
| Low | 7 |
| Informational | 5 |




## Insights

| Level | Reason | Site | Description | Statistic |
| --- | --- | --- | --- | --- |
| Low | Warning |  | ZAP warnings logged - see the zap.log file for details | 8    |
| Info | Informational | http://localhost:5000 | Percentage of responses with status code 2xx | 43 % |
| Info | Informational | http://localhost:5000 | Percentage of responses with status code 3xx | 5 % |
| Info | Exceeded Low | http://localhost:5000 | Percentage of responses with status code 4xx | 21 % |
| Info | Exceeded Low | http://localhost:5000 | Percentage of responses with status code 5xx | 35 % |
| Info | Informational | http://localhost:5000 | Percentage of endpoints with content type image/png | 5 % |
| Info | Informational | http://localhost:5000 | Percentage of endpoints with content type text/css | 5 % |
| Info | Informational | http://localhost:5000 | Percentage of endpoints with content type text/html | 90 % |
| Info | Informational | http://localhost:5000 | Percentage of endpoints with method GET | 95 % |
| Info | Informational | http://localhost:5000 | Percentage of endpoints with method POST | 5 % |
| Info | Informational | http://localhost:5000 | Count of total endpoints | 20    |







## Alerts

| Name | Risk Level | Number of Instances |
| --- | --- | --- |
| Cross Site Scripting (DOM Based) | High | 3 |
| Cross Site Scripting (Reflected) | High | 3 |
| Path Traversal | High | 2 |
| Remote OS Command Injection | High | 1 |
| Remote OS Command Injection (Time Based) | High | 1 |
| Server Side Template Injection | High | 1 |
| Source Code Disclosure - File Inclusion | High | 3 |
| Buffer Overflow | Medium | 4 |
| Content Security Policy (CSP) Header Not Set | Medium | Systemic |
| Integer Overflow Error | Medium | 4 |
| Missing Anti-clickjacking Header | Medium | Systemic |
| Source Code Disclosure - SQL | Medium | 4 |
| Application Error Disclosure | Low | 4 |
| Cross-Origin-Embedder-Policy Header Missing or Invalid | Low | 3 |
| Cross-Origin-Opener-Policy Header Missing or Invalid | Low | 3 |
| Cross-Origin-Resource-Policy Header Missing or Invalid | Low | 3 |
| Permissions Policy Header Not Set | Low | Systemic |
| Server Leaks Version Information via "Server" HTTP Response Header Field | Low | Systemic |
| X-Content-Type-Options Header Missing | Low | Systemic |
| Information Disclosure - Sensitive Information in URL | Informational | 2 |
| Information Disclosure - Suspicious Comments | Informational | 1 |
| Modern Web Application | Informational | 4 |
| Storable and Cacheable Content | Informational | Systemic |
| User Agent Fuzzer | Informational | Systemic |




## Alert Detail



### [ Cross Site Scripting (DOM Based) ](https://www.zaproxy.org/docs/alerts/40026/)



##### High (High)

### Description

Cross-site Scripting (XSS) is an attack technique that involves echoing attacker-supplied code into a user's browser instance. A browser instance can be a standard web browser client, or a browser object embedded in a software product such as the browser within WinAmp, an RSS reader, or an email client. The code itself is usually written in HTML/JavaScript, but may also extend to VBScript, ActiveX, Java, Flash, or any other browser-supported technology.
When an attacker gets a user's browser to execute his/her code, the code will run within the security context (or zone) of the hosting web site. With this level of privilege, the code has the ability to read, modify and transmit any sensitive data accessible by the browser. A Cross-site Scripted user could have his/her account hijacked (cookie theft), their browser redirected to another location, or possibly shown fraudulent content delivered by the web site they are visiting. Cross-site Scripting attacks essentially compromise the trust relationship between a user and the web site. Applications utilizing browser object instances which load content from the file system may execute code under the local machine zone allowing for system compromise.

There are three types of Cross-site Scripting attacks: non-persistent, persistent and DOM-based.
Non-persistent attacks and DOM-based attacks require a user to either visit a specially crafted link laced with malicious code, or visit a malicious web page containing a web form, which when posted to the vulnerable site, will mount the attack. Using a malicious form will oftentimes take place when the vulnerable resource only accepts HTTP POST requests. In such a case, the form can be submitted automatically, without the victim's knowledge (e.g. by using JavaScript). Upon clicking on the malicious link or submitting the malicious form, the XSS payload will get echoed back and will get interpreted by the user's browser and execute. Another technique to send almost arbitrary requests (GET and POST) is by using an embedded client, such as Adobe Flash.
Persistent attacks occur when the malicious code is submitted to a web site where it's stored for a period of time. Examples of an attacker's favorite targets often include message board posts, web mail messages, and web chat software. The unsuspecting user is not required to interact with any additional site/link (e.g. an attacker site or a malicious link sent via email), just simply view the web page containing the code.

* URL: http://localhost:5000/hash%3Fdata=%253Cscript%253Ealert(5397&29%253C/script%253E
  * Node Name: `http://localhost:5000/hash (data)`
  * Method: `GET`
  * Parameter: `data`
  * Attack: `<script>alert(5397)</script>`
  * Evidence: ``
  * Other Info: `The following steps were done to trigger the DOM XSS:
With <PAYLOAD_1> as: %3Cscript%3Ealert(5397)%3C/script%3E
Access: http://localhost:5000/hash?data=<PAYLOAD_1>
`
* URL: http://localhost:5000/traverse%3Ffile=%253Cscript%253Ealert(5397&29%253C/script%253E
  * Node Name: `http://localhost:5000/traverse (file)`
  * Method: `GET`
  * Parameter: `file`
  * Attack: `<script>alert(5397)</script>`
  * Evidence: ``
  * Other Info: `The following steps were done to trigger the DOM XSS:
With <PAYLOAD_1> as: %3Cscript%3Ealert(5397)%3C/script%3E
Access: http://localhost:5000/traverse?file=<PAYLOAD_1>
`
* URL: http://localhost:5000/xss%3Fname=%253Cscript%253Ealert(5397&29%253C/script%253E
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `name`
  * Attack: `<script>alert(5397)</script>`
  * Evidence: ``
  * Other Info: `The following steps were done to trigger the DOM XSS:
With <PAYLOAD_1> as: %3Cscript%3Ealert(5397)%3C/script%3E
Access: http://localhost:5000/xss?name=<PAYLOAD_1>
`


Instances: 3

### Solution

Phase: Architecture and Design
Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid.
Examples of libraries and frameworks that make it easier to generate properly encoded output include Microsoft's Anti-XSS library, the OWASP ESAPI Encoding module, and Apache Wicket.

Phases: Implementation; Architecture and Design
Understand the context in which your data will be used and the encoding that will be expected. This is especially important when transmitting data between different components, or when generating outputs that can contain multiple encodings at the same time, such as web pages or multi-part mail messages. Study all expected communication protocols and data representations to determine the required encoding strategies.
For any data that will be output to another web page, especially any data that was received from external inputs, use the appropriate encoding on all non-alphanumeric characters.
Consult the XSS Prevention Cheat Sheet for more details on the types of encoding and escaping that are needed.

Phase: Architecture and Design
For any security checks that are performed on the client side, ensure that these checks are duplicated on the server side, in order to avoid CWE-602. Attackers can bypass the client-side checks by modifying values after the checks have been performed, or by changing the client to remove the client-side checks entirely. Then, these modified values would be submitted to the server.

If available, use structured mechanisms that automatically enforce the separation between data and code. These mechanisms may be able to provide the relevant quoting, encoding, and validation automatically, instead of relying on the developer to provide this capability at every point where output is generated.

Phase: Implementation
For every web page that is generated, use and specify a character encoding such as ISO-8859-1 or UTF-8. When an encoding is not specified, the web browser may choose a different encoding by guessing which encoding is actually being used by the web page. This can cause the web browser to treat certain sequences as special, opening up the client to subtle XSS attacks. See CWE-116 for more mitigations related to encoding/escaping.

To help mitigate XSS attacks against the user's session cookie, set the session cookie to be HttpOnly. In browsers that support the HttpOnly feature (such as more recent versions of Internet Explorer and Firefox), this attribute can prevent the user's session cookie from being accessible to malicious client-side scripts that use document.cookie. This is not a complete solution, since HttpOnly is not supported by all browsers. More importantly, XMLHTTPRequest and other powerful browser technologies provide read access to HTTP headers, including the Set-Cookie header in which the HttpOnly flag is set.

Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use an allow list of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a deny list). However, deny lists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.

When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."

Ensure that you perform input validation at well-defined interfaces within the application. This will help protect the application even if a component is reused or moved elsewhere.
	

### Reference


* [ https://community.owasp.org/attacks/xss/ ](https://community.owasp.org/attacks/xss/)
* [ https://cwe.mitre.org/data/definitions/79.html ](https://cwe.mitre.org/data/definitions/79.html)


#### CWE Id: [ 79 ](https://cwe.mitre.org/data/definitions/79.html)


#### WASC Id: 8

#### Source ID: 1

### [ Cross Site Scripting (Reflected) ](https://www.zaproxy.org/docs/alerts/40012/)



##### High (Medium)

### Description

Cross-site Scripting (XSS) is an attack technique that involves echoing attacker-supplied code into a user's browser instance. A browser instance can be a standard web browser client, or a browser object embedded in a software product such as the browser within WinAmp, an RSS reader, or an email client. The code itself is usually written in HTML/JavaScript, but may also extend to VBScript, ActiveX, Java, Flash, or any other browser-supported technology.
When an attacker gets a user's browser to execute his/her code, the code will run within the security context (or zone) of the hosting web site. With this level of privilege, the code has the ability to read, modify and transmit any sensitive data accessible by the browser. A Cross-site Scripted user could have his/her account hijacked (cookie theft), their browser redirected to another location, or possibly shown fraudulent content delivered by the web site they are visiting. Cross-site Scripting attacks essentially compromise the trust relationship between a user and the web site. Applications utilizing browser object instances which load content from the file system may execute code under the local machine zone allowing for system compromise.

There are three types of Cross-site Scripting attacks: non-persistent, persistent and DOM-based.
Non-persistent attacks and DOM-based attacks require a user to either visit a specially crafted link laced with malicious code, or visit a malicious web page containing a web form, which when posted to the vulnerable site, will mount the attack. Using a malicious form will oftentimes take place when the vulnerable resource only accepts HTTP POST requests. In such a case, the form can be submitted automatically, without the victim's knowledge (e.g. by using JavaScript). Upon clicking on the malicious link or submitting the malicious form, the XSS payload will get echoed back and will get interpreted by the user's browser and execute. Another technique to send almost arbitrary requests (GET and POST) is by using an embedded client, such as Adobe Flash.
Persistent attacks occur when the malicious code is submitted to a web site where it's stored for a period of time. Examples of an attacker's favorite targets often include message board posts, web mail messages, and web chat software. The unsuspecting user is not required to interact with any additional site/link (e.g. an attacker site or a malicious link sent via email), just simply view the web page containing the code.

* URL: http://localhost:5000/hash%3Fdata=%253CscrIpt%253Ealert%25281%2529%253B%253C%252FscRipt%253E
  * Node Name: `http://localhost:5000/hash (data)`
  * Method: `GET`
  * Parameter: `data`
  * Attack: `<scrIpt>alert(1);</scRipt>`
  * Evidence: `<scrIpt>alert(1);</scRipt>`
  * Other Info: ``
* URL: http://localhost:5000/traverse%3Ffile=%253CscrIpt%253Ealert%25281%2529%253B%253C%252FscRipt%253E
  * Node Name: `http://localhost:5000/traverse (file)`
  * Method: `GET`
  * Parameter: `file`
  * Attack: `<scrIpt>alert(1);</scRipt>`
  * Evidence: `<scrIpt>alert(1);</scRipt>`
  * Other Info: ``
* URL: http://localhost:5000/xss%3Fname=%253C%252Fh1%253E%253CscrIpt%253Ealert%25281%2529%253B%253C%252FscRipt%253E%253Ch1%253E
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `name`
  * Attack: `</h1><scrIpt>alert(1);</scRipt><h1>`
  * Evidence: `</h1><scrIpt>alert(1);</scRipt><h1>`
  * Other Info: ``


Instances: 3

### Solution

Phase: Architecture and Design
Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid.
Examples of libraries and frameworks that make it easier to generate properly encoded output include Microsoft's Anti-XSS library, the OWASP ESAPI Encoding module, and Apache Wicket.

Phases: Implementation; Architecture and Design
Understand the context in which your data will be used and the encoding that will be expected. This is especially important when transmitting data between different components, or when generating outputs that can contain multiple encodings at the same time, such as web pages or multi-part mail messages. Study all expected communication protocols and data representations to determine the required encoding strategies.
For any data that will be output to another web page, especially any data that was received from external inputs, use the appropriate encoding on all non-alphanumeric characters.
Consult the XSS Prevention Cheat Sheet for more details on the types of encoding and escaping that are needed.

Phase: Architecture and Design
For any security checks that are performed on the client side, ensure that these checks are duplicated on the server side, in order to avoid CWE-602. Attackers can bypass the client-side checks by modifying values after the checks have been performed, or by changing the client to remove the client-side checks entirely. Then, these modified values would be submitted to the server.

If available, use structured mechanisms that automatically enforce the separation between data and code. These mechanisms may be able to provide the relevant quoting, encoding, and validation automatically, instead of relying on the developer to provide this capability at every point where output is generated.

Phase: Implementation
For every web page that is generated, use and specify a character encoding such as ISO-8859-1 or UTF-8. When an encoding is not specified, the web browser may choose a different encoding by guessing which encoding is actually being used by the web page. This can cause the web browser to treat certain sequences as special, opening up the client to subtle XSS attacks. See CWE-116 for more mitigations related to encoding/escaping.

To help mitigate XSS attacks against the user's session cookie, set the session cookie to be HttpOnly. In browsers that support the HttpOnly feature (such as more recent versions of Internet Explorer and Firefox), this attribute can prevent the user's session cookie from being accessible to malicious client-side scripts that use document.cookie. This is not a complete solution, since HttpOnly is not supported by all browsers. More importantly, XMLHTTPRequest and other powerful browser technologies provide read access to HTTP headers, including the Set-Cookie header in which the HttpOnly flag is set.

Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use an allow list of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a deny list). However, deny lists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.

When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."

Ensure that you perform input validation at well-defined interfaces within the application. This will help protect the application even if a component is reused or moved elsewhere.
	

### Reference


* [ https://community.owasp.org/attacks/xss/ ](https://community.owasp.org/attacks/xss/)
* [ https://cwe.mitre.org/data/definitions/79.html ](https://cwe.mitre.org/data/definitions/79.html)


#### CWE Id: [ 79 ](https://cwe.mitre.org/data/definitions/79.html)


#### WASC Id: 8

#### Source ID: 1

### [ Path Traversal ](https://www.zaproxy.org/docs/alerts/6/)



##### High (Medium)

### Description

The Path Traversal attack technique allows an attacker access to files, directories, and commands that potentially reside outside the web document root directory. An attacker may manipulate a URL in such a way that the web site will execute or reveal the contents of arbitrary files anywhere on the web server. Any device that exposes an HTTP-based interface is potentially vulnerable to Path Traversal.

Most web sites restrict user access to a specific portion of the file-system, typically called the "web document root" or "CGI root" directory. These directories contain the files intended for user access and the executable necessary to drive web application functionality. To access files or execute commands anywhere on the file-system, Path Traversal attacks will utilize the ability of special-characters sequences.

The most basic Path Traversal attack uses the "../" special-character sequence to alter the resource location requested in the URL. Although most popular web servers will prevent this technique from escaping the web document root, alternate encodings of the "../" sequence may help bypass the security filters. These method variations include valid and invalid Unicode-encoding ("..%u2216" or "..%c0%af") of the forward slash character, backslash characters ("..\") on Windows-based servers, URL encoded characters "%2e%2e%2f"), and double URL encoding ("..%255c") of the backslash character.

Even if the web server properly restricts Path Traversal attempts in the URL path, a web application itself may still be vulnerable due to improper handling of user-supplied input. This is a common problem of web applications that use template mechanisms or load static text from files. In variations of the attack, the original URL parameter value is substituted with the file name of one of the web application's dynamic scripts. Consequently, the results can reveal source code because the file is interpreted as text instead of an executable script. These techniques often employ additional special characters such as the dot (".") to reveal the listing of the current working directory, or "%00" NULL characters in order to bypass rudimentary file extension checks.

* URL: http://localhost:5000/traverse%3Ffile=%252Fetc%252Fpasswd
  * Node Name: `http://localhost:5000/traverse (file)`
  * Method: `GET`
  * Parameter: `file`
  * Attack: `/etc/passwd`
  * Evidence: `root:x:0:0`
  * Other Info: ``
* URL: http://localhost:5000/cmd%3Ffile=%252F
  * Node Name: `http://localhost:5000/cmd (file)`
  * Method: `GET`
  * Parameter: `file`
  * Attack: `/`
  * Evidence: `etc`
  * Other Info: `While the evidence field indicates etc, the rule actually checked that the response contains matches for all of the following: proc, etc, boot, tmp, home.`


Instances: 2

### Solution

Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use an allow list of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a deny list). However, deny lists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.

When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."

For filenames, use stringent allow lists that limit the character set to be used. If feasible, only allow a single "." character in the filename to avoid weaknesses, and exclude directory separators such as "/". Use an allow list of allowable file extensions.

Warning: if you attempt to cleanse your data, then do so that the end result is not in the form that can be dangerous. A sanitizing mechanism can remove characters such as '.' and ';' which may be required for some exploits. An attacker can try to fool the sanitizing mechanism into "cleaning" data into a dangerous form. Suppose the attacker injects a '.' inside a filename (e.g. "sensi.tiveFile") and the sanitizing mechanism removes the character resulting in the valid filename, "sensitiveFile". If the input data are now assumed to be safe, then the file may be compromised. 

Inputs should be decoded and canonicalized to the application's current internal representation before being validated. Make sure that your application does not decode the same input twice. Such errors could be used to bypass allow list schemes by introducing dangerous inputs after they have been checked.

Use a built-in path canonicalization function (such as realpath() in C) that produces the canonical version of the pathname, which effectively removes ".." sequences and symbolic links.

Run your code using the lowest privileges that are required to accomplish the necessary tasks. If possible, create isolated accounts with limited privileges that are only used for a single task. That way, a successful attack will not immediately give the attacker access to the rest of the software or its environment. For example, database applications rarely need to run as the database administrator, especially in day-to-day operations.

When the set of acceptable objects, such as filenames or URLs, is limited or known, create a mapping from a set of fixed input values (such as numeric IDs) to the actual filenames or URLs, and reject all other inputs.

Run your code in a "jail" or similar sandbox environment that enforces strict boundaries between the process and the operating system. This may effectively restrict which files can be accessed in a particular directory or which commands can be executed by your software.

OS-level examples include the Unix chroot jail, AppArmor, and SELinux. In general, managed code may provide some protection. For example, java.io.FilePermission in the Java SecurityManager allows you to specify restrictions on file operations.

This may not be a feasible solution, and it only limits the impact to the operating system; the rest of your application may still be subject to compromise.


### Reference


* [ https://community.owasp.org/attacks/Path_Traversal ](https://community.owasp.org/attacks/Path_Traversal)
* [ https://cwe.mitre.org/data/definitions/22.html ](https://cwe.mitre.org/data/definitions/22.html)


#### CWE Id: [ 22 ](https://cwe.mitre.org/data/definitions/22.html)


#### WASC Id: 33

#### Source ID: 1

### [ Remote OS Command Injection ](https://www.zaproxy.org/docs/alerts/90020/)



##### High (Medium)

### Description

Attack technique used for unauthorized execution of operating system commands. This attack is possible when an application accepts untrusted input to build operating system commands in an insecure manner involving improper data sanitization, and/or improper calling of external programs.

* URL: http://localhost:5000/cmd%3Ffile=whoami%2526cat+%252Fetc%252Fpasswd%2526
  * Node Name: `http://localhost:5000/cmd (file)`
  * Method: `GET`
  * Parameter: `file`
  * Attack: `whoami&cat /etc/passwd&`
  * Evidence: `root:x:0:0`
  * Other Info: `The scan rule was able to retrieve the content of a file or command by sending [whoami&cat /etc/passwd&] to the operating system running this application.`


Instances: 1

### Solution

If at all possible, use library calls rather than external processes to recreate the desired functionality.

Run your code in a "jail" or similar sandbox environment that enforces strict boundaries between the process and the operating system. This may effectively restrict which files can be accessed in a particular directory or which commands can be executed by your software.

OS-level examples include the Unix chroot jail, AppArmor, and SELinux. In general, managed code may provide some protection. For example, java.io.FilePermission in the Java SecurityManager allows you to specify restrictions on file operations.
This may not be a feasible solution, and it only limits the impact to the operating system; the rest of your application may still be subject to compromise.

For any data that will be used to generate a command to be executed, keep as much of that data out of external control as possible. For example, in web applications, this may require storing the command locally in the session's state instead of sending it out to the client in a hidden form field.

Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid.

For example, consider using the ESAPI Encoding control or a similar tool, library, or framework. These will help the programmer encode outputs in a manner less prone to error.

If you need to use dynamically-generated query strings or commands in spite of the risk, properly quote arguments and escape any special characters within those arguments. The most conservative approach is to escape or filter all characters that do not pass an extremely strict allow list (such as everything that is not alphanumeric or white space). If some special characters are still needed, such as white space, wrap each argument in quotes after the escaping/filtering step. Be careful of argument injection.

If the program to be executed allows arguments to be specified within an input file or from standard input, then consider using that mode to pass arguments instead of the command line.

If available, use structured mechanisms that automatically enforce the separation between data and code. These mechanisms may be able to provide the relevant quoting, encoding, and validation automatically, instead of relying on the developer to provide this capability at every point where output is generated.

Some languages offer multiple functions that can be used to invoke commands. Where possible, identify any function that invokes a command shell using a single string, and replace it with a function that requires individual arguments. These functions typically perform appropriate quoting and filtering of arguments. For example, in C, the system() function accepts a string that contains the entire command to be executed, whereas execl(), execve(), and others require an array of strings, one for each argument. In Windows, CreateProcess() only accepts one command at a time. In Perl, if system() is provided with an array of arguments, then it will quote each of the arguments.

Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use an allow list of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a deny list). However, deny lists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.

When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."

When constructing OS command strings, use stringent allow lists that limit the character set based on the expected value of the parameter in the request. This will indirectly limit the scope of an attack, but this technique is less important than proper output encoding and escaping.

Note that proper output encoding, escaping, and quoting is the most effective solution for preventing OS command injection, although input validation may provide some defense-in-depth. This is because it effectively limits what will appear in output. Input validation will not always prevent OS command injection, especially if you are required to support free-form text fields that could contain arbitrary characters. For example, when invoking a mail program, you might need to allow the subject field to contain otherwise-dangerous inputs like ";" and ">" characters, which would need to be escaped or otherwise handled. In this case, stripping the character might reduce the risk of OS command injection, but it would produce incorrect behavior because the subject field would not be recorded as the user intended. This might seem to be a minor inconvenience, but it could be more important when the program relies on well-structured subject lines in order to pass messages to other components.

Even if you make a mistake in your validation (such as forgetting one out of 100 input fields), appropriate encoding is still likely to protect you from injection-based attacks. As long as it is not done in isolation, input validation is still a useful technique, since it may significantly reduce your attack surface, allow you to detect some attacks, and provide other security benefits that proper encoding does not address.

### Reference


* [ https://cwe.mitre.org/data/definitions/78.html ](https://cwe.mitre.org/data/definitions/78.html)
* [ https://owasp.org/www-community/attacks/Command_Injection ](https://owasp.org/www-community/attacks/Command_Injection)


#### CWE Id: [ 78 ](https://cwe.mitre.org/data/definitions/78.html)


#### WASC Id: 31

#### Source ID: 1

### [ Remote OS Command Injection (Time Based) ](https://www.zaproxy.org/docs/alerts/90037/)



##### High (Medium)

### Description

Attack technique used for unauthorized execution of operating system commands. This attack is possible when an application accepts untrusted input to build operating system commands in an insecure manner involving improper data sanitization, and/or improper calling of external programs.

* URL: http://localhost:5000/cmd%3Ffile=whoami%2526sleep+1.0%2526
  * Node Name: `http://localhost:5000/cmd (file)`
  * Method: `GET`
  * Parameter: `file`
  * Attack: `whoami&sleep 15&`
  * Evidence: ``
  * Other Info: `The scan rule was able to control the timing of the application response by sending [whoami&sleep 15&] to the operating system running this application.`


Instances: 1

### Solution

If at all possible, use library calls rather than external processes to recreate the desired functionality.

Run your code in a "jail" or similar sandbox environment that enforces strict boundaries between the process and the operating system. This may effectively restrict which files can be accessed in a particular directory or which commands can be executed by your software.

OS-level examples include the Unix chroot jail, AppArmor, and SELinux. In general, managed code may provide some protection. For example, java.io.FilePermission in the Java SecurityManager allows you to specify restrictions on file operations.
This may not be a feasible solution, and it only limits the impact to the operating system; the rest of your application may still be subject to compromise.

For any data that will be used to generate a command to be executed, keep as much of that data out of external control as possible. For example, in web applications, this may require storing the command locally in the session's state instead of sending it out to the client in a hidden form field.

Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid.

For example, consider using the ESAPI Encoding control or a similar tool, library, or framework. These will help the programmer encode outputs in a manner less prone to error.

If you need to use dynamically-generated query strings or commands in spite of the risk, properly quote arguments and escape any special characters within those arguments. The most conservative approach is to escape or filter all characters that do not pass an extremely strict allow list (such as everything that is not alphanumeric or white space). If some special characters are still needed, such as white space, wrap each argument in quotes after the escaping/filtering step. Be careful of argument injection.

If the program to be executed allows arguments to be specified within an input file or from standard input, then consider using that mode to pass arguments instead of the command line.

If available, use structured mechanisms that automatically enforce the separation between data and code. These mechanisms may be able to provide the relevant quoting, encoding, and validation automatically, instead of relying on the developer to provide this capability at every point where output is generated.

Some languages offer multiple functions that can be used to invoke commands. Where possible, identify any function that invokes a command shell using a single string, and replace it with a function that requires individual arguments. These functions typically perform appropriate quoting and filtering of arguments. For example, in C, the system() function accepts a string that contains the entire command to be executed, whereas execl(), execve(), and others require an array of strings, one for each argument. In Windows, CreateProcess() only accepts one command at a time. In Perl, if system() is provided with an array of arguments, then it will quote each of the arguments.

Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use an allow list of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a deny list). However, deny lists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.

When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."

When constructing OS command strings, use stringent allow lists that limit the character set based on the expected value of the parameter in the request. This will indirectly limit the scope of an attack, but this technique is less important than proper output encoding and escaping.

Note that proper output encoding, escaping, and quoting is the most effective solution for preventing OS command injection, although input validation may provide some defense-in-depth. This is because it effectively limits what will appear in output. Input validation will not always prevent OS command injection, especially if you are required to support free-form text fields that could contain arbitrary characters. For example, when invoking a mail program, you might need to allow the subject field to contain otherwise-dangerous inputs like ";" and ">" characters, which would need to be escaped or otherwise handled. In this case, stripping the character might reduce the risk of OS command injection, but it would produce incorrect behavior because the subject field would not be recorded as the user intended. This might seem to be a minor inconvenience, but it could be more important when the program relies on well-structured subject lines in order to pass messages to other components.

Even if you make a mistake in your validation (such as forgetting one out of 100 input fields), appropriate encoding is still likely to protect you from injection-based attacks. As long as it is not done in isolation, input validation is still a useful technique, since it may significantly reduce your attack surface, allow you to detect some attacks, and provide other security benefits that proper encoding does not address.

### Reference


* [ https://cwe.mitre.org/data/definitions/78.html ](https://cwe.mitre.org/data/definitions/78.html)
* [ https://owasp.org/www-community/attacks/Command_Injection ](https://owasp.org/www-community/attacks/Command_Injection)


#### CWE Id: [ 78 ](https://cwe.mitre.org/data/definitions/78.html)


#### WASC Id: 31

#### Source ID: 1

### [ Server Side Template Injection ](https://www.zaproxy.org/docs/alerts/90035/)



##### High (High)

### Description

When the user input is inserted in the template instead of being used as argument in rendering is evaluated by the template engine. Depending on the template engine it can lead to remote code execution.

* URL: http://localhost:5000/xss%3Fname=zj%257B%257B4491*4372%257D%257Dzj
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `name`
  * Attack: `zj{{4491*4372}}zj`
  * Evidence: ``
  * Other Info: `Proof found at [http://localhost:5000/xss?name=Visitor]
content:
[<h1>Hello, zj19634652zj!</h1><p>Welcome to our site.</p>Server: Werkzeug/3.1.9 Python/3.9.25
Date: Fri, 27 Nov 2026 22:24:14 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 56
Connection: close
]`


Instances: 1

### Solution

Instead of inserting the user input in the template, use it as rendering argument.

### Reference


* [ https://portswigger.net/research/server-side-template-injection ](https://portswigger.net/research/server-side-template-injection)


#### CWE Id: [ 1336 ](https://cwe.mitre.org/data/definitions/1336.html)


#### WASC Id: 20

#### Source ID: 1

### [ Source Code Disclosure - File Inclusion ](https://www.zaproxy.org/docs/alerts/43/)



##### High (Medium)

### Description

The Path Traversal attack technique allows an attacker access to files, directories, and commands that potentially reside outside the web document root directory. An attacker may manipulate a URL in such a way that the web site will execute or reveal the contents of arbitrary files anywhere on the web server. Any device that exposes an HTTP-based interface is potentially vulnerable to Path Traversal.

Most web sites restrict user access to a specific portion of the file-system, typically called the "web document root" or "CGI root" directory. These directories contain the files intended for user access and the executable necessary to drive web application functionality. To access files or execute commands anywhere on the file-system, Path Traversal attacks will utilize the ability of special-characters sequences.

The most basic Path Traversal attack uses the "../" special-character sequence to alter the resource location requested in the URL. Although most popular web servers will prevent this technique from escaping the web document root, alternate encodings of the "../" sequence may help bypass the security filters. These method variations include valid and invalid Unicode-encoding ("..%u2216" or "..%c0%af") of the forward slash character, backslash characters ("..\") on Windows-based servers, URL encoded characters "%2e%2e%2f"), and double URL encoding ("..%255c") of the backslash character.

Even if the web server properly restricts Path Traversal attempts in the URL path, a web application itself may still be vulnerable due to improper handling of user-supplied input. This is a common problem of web applications that use template mechanisms or load static text from files. In variations of the attack, the original URL parameter value is substituted with the file name of one of the web application's dynamic scripts. Consequently, the results can reveal source code because the file is interpreted as text instead of an executable script. These techniques often employ additional special characters such as the dot (".") to reveal the listing of the current working directory, or "%00" NULL characters in order to bypass rudimentary file extension checks.

* URL: http://localhost:5000/hash%3Fdata=test
  * Node Name: `http://localhost:5000/hash (data)`
  * Method: `GET`
  * Parameter: `data`
  * Attack: `hash`
  * Evidence: ``
  * Other Info: `The output for the source code filename [hash] differs sufficiently from that of the random parameter [eoumityzestelmotuslnuvdqumqdrpqkvadzeh], at [27%], compared to a threshold of [75%]`
* URL: http://localhost:5000/traverse%3Ffile=README.md
  * Node Name: `http://localhost:5000/traverse (file)`
  * Method: `GET`
  * Parameter: `file`
  * Attack: `traverse`
  * Evidence: ``
  * Other Info: `The output for the source code filename [traverse] differs sufficiently from that of the random parameter [eoumityzestelmotuslnuvdqumqdrpqkvadzeh], at [75%], compared to a threshold of [75%]`
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `name`
  * Attack: `xss`
  * Evidence: ``
  * Other Info: `The output for the source code filename [xss] differs sufficiently from that of the random parameter [eoumityzestelmotuslnuvdqumqdrpqkvadzeh], at [66%], compared to a threshold of [75%]`


Instances: 3

### Solution

Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use an allow list of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a deny list). However, deny lists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.

When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."

For filenames, use stringent allow lists that limit the character set to be used. If feasible, only allow a single "." character in the filename to avoid weaknesses, and exclude directory separators such as "/". Use an allow list of allowable file extensions.

Warning: if you attempt to cleanse your data, then do so that the end result is not in the form that can be dangerous. A sanitizing mechanism can remove characters such as '.' and ';' which may be required for some exploits. An attacker can try to fool the sanitizing mechanism into "cleaning" data into a dangerous form. Suppose the attacker injects a '.' inside a filename (e.g. "sensi.tiveFile") and the sanitizing mechanism removes the character resulting in the valid filename, "sensitiveFile". If the input data are now assumed to be safe, then the file may be compromised. 

Inputs should be decoded and canonicalized to the application's current internal representation before being validated. Make sure that your application does not decode the same input twice. Such errors could be used to bypass allow list schemes by introducing dangerous inputs after they have been checked.

Use a built-in path canonicalization function (such as realpath() in C) that produces the canonical version of the pathname, which effectively removes ".." sequences and symbolic links.

Run your code using the lowest privileges that are required to accomplish the necessary tasks. If possible, create isolated accounts with limited privileges that are only used for a single task. That way, a successful attack will not immediately give the attacker access to the rest of the software or its environment. For example, database applications rarely need to run as the database administrator, especially in day-to-day operations.

When the set of acceptable objects, such as filenames or URLs, is limited or known, create a mapping from a set of fixed input values (such as numeric IDs) to the actual filenames or URLs, and reject all other inputs.

Run your code in a "jail" or similar sandbox environment that enforces strict boundaries between the process and the operating system. This may effectively restrict which files can be accessed in a particular directory or which commands can be executed by your software.

OS-level examples include the Unix chroot jail, AppArmor, and SELinux. In general, managed code may provide some protection. For example, java.io.FilePermission in the Java SecurityManager allows you to specify restrictions on file operations.

This may not be a feasible solution, and it only limits the impact to the operating system; the rest of your application may still be subject to compromise.


### Reference


* [ https://community.owasp.org/attacks/Path_Traversal ](https://community.owasp.org/attacks/Path_Traversal)
* [ https://cwe.mitre.org/data/definitions/22.html ](https://cwe.mitre.org/data/definitions/22.html)


#### CWE Id: [ 541 ](https://cwe.mitre.org/data/definitions/541.html)


#### WASC Id: 33

#### Source ID: 1

### [ Buffer Overflow ](https://www.zaproxy.org/docs/alerts/30001/)



##### Medium (Medium)

### Description

Buffer overflow errors are characterized by the overwriting of memory spaces of the background web process, which should have never been modified intentionally or unintentionally. Overwriting values of the IP (Instruction Pointer), BP (Base Pointer) and other registers causes exceptions, segmentation faults, and other process errors to occur. Usually these errors end execution of the application in an unexpected way.

* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=console.png
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f)`
  * Method: `GET`
  * Parameter: `__debugger__`
  * Attack: `lSobXvDHIkQcWGISifENPCvpOAuhHsQjIcGnbaYvydMxjINGctwYSldxUTqHoyrGYhdewHokAKeQIBBYBSyCWIlsSDagpsmbbaLuuNtXWPFRMEIBkxirWwdyoLiUZUpupsOZIAUtKpqQmEuqONXuVUHkgYfnbnJDadmsYSmlMhYZqTUeIQlZVRqcODUlGWaPQCURFkFBhFrOigSVEARLnQSaEsWUVngTjfmfcxXanMdkODxkPDkQdJJULClYjtswcSEEtlqFiwyjphMuxCoJvXNCyyTOgimMAPImZHyoqxYrpHBAHFxrPNSLUgeOMoTuBsXEiRbrLPZYxHkHvKrdoQQmvCgKwaYTlUfkBieYpsEaOAcFptdgZlXYNplkgOxCRkiEUkkdTQOtgtByPVByucfPSvcaOlutEZxyNnxqkGScoeINHlMHbnJYbdsVhPfZqBWlKxlQlbfQfpHxPoiQxKyPDIpckvghPQvWsqstGGUNNsuUUtTAaPhEmdXKYNoIhRXQXnFZkSvgspTCmhvhsefuCPfGZdmZOfxfwmlWMHAOCvLfCySlCPCOTBQlPTuTveJieRwyNxYdeLdOYUONbPMaOGNXGxOMfPrVkNxxGEQVUuNIxJTpLARKjkePcFccIXRWtJfYYcwiUejTqBdGaBvMpNexmrkPZFDQsEYNvkxBUceirGioKXgUrvhidUPJrkxtaIdRLZqIXLMHFsPAGRnsRyMHhNjydvNnaPVjWAlSRvMuuqAgnlaIqwMjUYAPNFXwuCHxaOOybuOdWHUiHEbgCqYcZhnwXIVfHkllhEIVCOoCntoMqMNZCoTFcMDweVbFJnWualxvIFEJiUBFoNTThoRDOxWVqVlYkHTenZIdlUnOnqOttVselVWoVOqaMGUhMlGDGFZDbgLXTygbZkqAYmICmWjopmveeMSIUAeDVUbPeUOcIFJugDtcakfjIVTsDdjSQknAZCFkPxDPDraqdceFyJFckIehqxKdjMXFXtvbfKrfotNUPmWnJcKZBjDdufjeZGuXcjTvDFQEttmLNgLLBejqApTJGyoftLcyukiIWuhwZDPbUDBuQKeSyQFrVrqWNwegYiZpFHfoEyRglcxEIIMTsqitcRjlQZZHjEpkbTrZVWOFRuPxLYLDtMYHtQYZPJvIsqHMNKTOFXIfiSEdCvipmiJfxOZUuJtnDacBNVHKJtdTLHqtINwdGElJiIFGnCxKLTnEjdMIEvvVKZSvPNIGhIxkxOLvRSeuqNPhKnqMumQLkrcVZoehcElXykLqFQRLkRWhoNGEmbWnkpdTYOKqddNmSRlpnHlQFJJtQVwjtLjjkmXMNaSRtWJQIZCiQeijOkeKdfZnWacoqOHaGPlmQGQwGemCXFsMPkEeiXSYRklJCBmYbajmxOtcjWqvrQvxPqygVWlepBEDdHMmerveAFtMOwkNVjIirfUffkJqtPpKyppkEYRcWXUkdjYQFcvBkTwEpUYcOJGcwPTOekYoKMgATtWstosQDTViYbvuBaassJytnJGeighnFHXFFCHkWbUqVBydIDwNIEpTuqOSvAAAUcLmJegoHLDNiVYNUWWEKcUZOqELKhQRPDMKoeYwcvnuJcdlyQZvkgOOAkQTtMgOfEoovpxwchmERZODHxgfOfdsvOBoinPCQOMqhXmdIEgsKKaPjVmeNQMcQKEsJospsdQDDTnEvefRWgZEdlGwpySAUYDdPaBfDNixVsuXKjACODHPCvNSdAuxkpFMrZcacRjQrejIqRAIRkcBtjnWrkXrLPTkxcJdXcbYwnGrtTOLXAnZOZGquoBhSUVEOBmvrMwQVycIDfvRPqmSMZxJLykonbyGmqZmofOJRfWxtrlpYOYJlmOTuIiyHETEFiihllvkRgeMVrAYcrQMHFRHDuhyrDXvVcZFNpNskjVRqkSstbZguGNXZCnmyFPoiBIPhfJEXdQNooselYPUpYJkaXxGJswikZZjTTbLocZtCeTWwlETcNXfiIYPWTjiXOWHNaohSZdeFEyjhFvkVFbrxWMKRREbmUiiNMjJldgSdflZycfyBZuriZnCxDQLXMVgZtFoSgABUVlCKXGo`
  * Evidence: `Connection: close`
  * Other Info: `Potential Buffer Overflow. The script closed the connection and threw a 500 Internal Server Error.`
* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=console.png
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f)`
  * Method: `GET`
  * Parameter: `cmd`
  * Attack: `vlrshRwiPEnQNPTuScSRZqunFGipTtCthQMniTBqmaLwtUiirKYjrmFblSOADpWuauvxEoAnaqSTCLrqJYtnYvTWjastJRKguofIeOWTSVLIrjVIjAYhhFcQmXromsemWPvpqtjmbqQSdKHsMADUfPsgMjwgyWNWjdaZLbuGBbBwpSRuhLkwFtsVhexrXkJlicfMBCpvFmCUuuXuAnenomiKefOoVvFOHHGyERiempeQdMAskxhElBLRQAEFgHarTuCrxBwMMrqerWTgmsIIBdYnXBIxNHPuRvnsArtIiIuqITRISTHplBYhIdbnegulyoaTVBMAINJKxstypsIqEujngWhitONKMjrxleRdDJEGUIhMLEpUemsnoTFPdeyUlbooqfnCbndtooFwbOorRoiCUGOdieIXioZiUThoRaqnrWpkaGkCTdLcnCmONLeSkPIWjAblGKcAijVIAUoXcMDFslLNuMKeNZMuEugLBaybXGCndxaINwhWjWicnXyyKNHJvAMJqqUcDGRPmBKNrsSIOhIZKQOFKBZvvZXBrImmYCchVwIYtlWNbFVIdVUwnnxHBhUVbBAaFeOUNSxfKOaIADmvSOhHLTbimQWyDDLuxaVxHDyjHQfDWZXkTSpBZmCuDfhrgQBEUqPRiqNmqsVsdSFHLsmXWfRvgMusyeomPKeTQmEOgXwnowVHRdwemEbvOAKjXChxIGboMEKCmjsJNkNVDUboaaldmGvQNYwWLxXPxxiHKLcnkypCusDlBGXMqqASYBxjGTotgTaHEYCuDXBkwGkEPBWNvXrjtIFBIaRMqIEPqMWklKMhGUGrtkSGaGaYPEsHgLTyuVnLyyNYKXCQkSULbWCXYbyqSjJxFxVuvxFiWaeimvMZbfYsQcRGodjAJDfGDntyiFyUpZMgjOcmIcyQblsQghHXeHrprGVoPjQHYjMjFRqdgptgdBTNfNBBxHZAPpDjrTbOMurlieQEcAvXYSevuXyqLxOsuBkKjqFnWnRLcLVLVHFXjByBRIwRgBuXttioRwnDuwDGGFoSreYUTyLxlqcPykAujxaQvtZxCCehxGprNJpqWBnarSyOgtyPgXkAJQYZbLQhGdqyHGLQESlFlygCyvcKrXcMRxfNjNDsDbXFfVmtmonkXaXwBQoWfNGkRGZNyMjuyZTWucvxsiOJkFhQZLNHtYvJWBrugIJemGjDorBeCVeKONPPoeDvOjvAtDCHwFoUJVBNGLUCFieenPwWvabceonrySoLFIJfyxdRTjBwONnlCDGaZfbEgaxXcncraaSpFDWhcOAByGeOjVaTVMPepDxZZCYQSqcTpvhnxJoQUKyhrdfwRpIAgJveDfFmZAHWQsXpNXANxNPMYmZAKPoeJLQYuGxEauvuclWwBGaiDeGekhHaUXvXJfEkCEkOAefbohFfPaZnUJWSYIvxcmpAiWYRiKhrbvCqdZBgrtnNOTrusXRKOnFXQqKKvfeEmaArggeItEFmhfDfCCVwIqklZQnvDCANnGgCeWtctJANTPpOyPLKWMxwpJGuMZQmAfFVVSECYrquPjjYYkaTqhRWFelRnOoDyjBRPOkMXJOsYQytfhVqtYKLWosXidrFuTrxGmVLaMlUpAaERHqWjSFCZQEQmGNhwqvYkXQCOcirOuHtDdNjVSHQQBnTytEhMCwHvqZgpIlPPYYlUYVjNiwYnibWQtpOxSaFYGHdFVhOWfyOwdINuecDgXyjsvBUxxLwHrEHSkygJjffTpHbQcSuuxfQDdVSyFEeCuxUaHElCkafygmVoknNaRRvcfFWTZZekBCvbEfxFMIifBhdpYxwCrmPbiiERwrtWlJCntcWaxZIsQaoCYeZomWcSAThoYxLKpcCFGXqsoIEGEkrOgtlcfkkVlBxOrbXGUAisKAGnZhPRaDSDugkCLwUuSVgJGlfWoIdGZFaKdKMXkKmhXisfYQboaGkdZMtLwagsGcgXTSRxKjEplRujBDWQstgpHxtAKtXfkunwFwhKpMKFJAxkpmmbwvqilPeBLHAxjDGINPwgAGtDjSvhVNCTVikQrmsVYxUcGxqSAaoHPcApSpEMEpmTefx`
  * Evidence: `Connection: close`
  * Other Info: `Potential Buffer Overflow. The script closed the connection and threw a 500 Internal Server Error.`
* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=console.png&s=K0w7DsbgSDM6qUh4LWRy
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f,s)`
  * Method: `GET`
  * Parameter: `__debugger__`
  * Attack: `gMBgfJyuiJlSbUaAyweDGNSAKNcEItGwvRnUiCtXplXdXsAwuRjQGjMRSVXqEqABESHDJXfeolQrtiRvGvfraogYWyMeEHJgUNVJqqdHtfuWxGTrCyKegcUCHBURuGZopLCHpxGYnBLlQMqgZKxXdITmPMHhquSXvJYQKdnxRtnVPeSVDxYyXZxtVIDWfUkShkOAAfbgGlyFKOGglZPZgMjBxmGHBBxKVGwpZULVXKjxHnhDEJTVClpIhkQINQSdDELrqGCFVfYvKFTAZjKxdCYutQCmocXGfKWZMwbQYELOsHkOWjkTnIXoeLDkWmtJoyiMmTVqHbEBwVjFTMtkhYxnNUrNVPjpHNLgAWlhIudiVRsSLrkXHkLhOtvHuIUFFdiMZUnGZfxgmYENOhdhMipUnoYKWbsvMvbVvrAScgCBhFcRFUcltuebKOOPREmiibbfIcOsPNeRMYcWKaFwuSfjVdiGswnRyDaOKZSEDhmPIYoVtrVuBsZUeQoICmOMhnJyMDPuhjrcIJMbCQOMIUyYPkmTmjSGamPJipTZjMSdTEyagvCfpodnjMGVSbDZggNiJLBcVugSJGENjCqldPdpSYVEwuyKsKOGCjVsxvTunGTqLLwyNhDnrtLHuaTVAQBZMbsFtshZDCtVaYPojmHQSPVrUFbUbaoOZheJDlyyZDKHwgXkWevIiHWxvAJPCoBEuOLhqfeXnFfSOIWKfATYtGBjpsuPsotLbRtmuqAMsGTppYsyBkPAcbjvjerdirwXSQBywlwGZxFUflpUUMXgveSJGYPyPFBridvtJusqJTqfefCgNjTsVTGIbvRsVdXuFuRjhPMstldBCXxfeoHZZanVNeAipkVIIoldHrERFMHoYMrPiAGSZGtthWAupaNcgNjZLtHubECtggZZBIYFeLHCfiBOVxUYVCKgyfFuOqbnfpGOybRuwkaJvbpVQsdAkFxJsgHIrGiqHrYevJehGrEciZLPKPGaCFmAYiDxisFDOKjpusJBYlVVYtUCElUyoHJEaPkrlsIVADLdgUjCjHtyoBZEwxgGJdgedZdEoWLoqRvNhcvMHCYNeKCkZkUBeGiKktLGGxUMiMLrDYrLkPxcCpmHcYsyNtvdYSoTyYEsEDZsWNDJvieEauggNnxLXIahoDstwHdjNjKUVxTBtTaTjhdBZsYpBaIKqOAxlVDDbJFwFbSUnAVBKxvgEaXUrwZTGGLcjDXyrqGDJJWKoZWVXtXudfpoPTjtHoBcKxtBvVyogJBtdtfXVbkdpkIlHBHOSlVgRRemRGuNZXmIMLukAlUBPUUtvhUPEAxvbowHGqQcClqRSeXIJJRgSxZrfGHcoYBJJbUAnbfuCYVhhkWVLPnUyhNmUCVbcvMwBoaXlbamYFtoUQuppnagfsrRTkXqAeGbQtMQZeXjdxqGFsBlAWkDClwsaeMnYZuLOuJRpJCxZjCCRcJrKJLmcKVeGtEfndrFJIQDsPVcIkIBehgHTdJFPQLlqAaJmxqtvbBggPKHQVylgsPHgSRbjslTANwevUywtmiEAMLYLBysDXKhIMgvmEjgIWbnTOhybUYWOARvDASLsYZaNINYOssLlqtRrPynxQQrRoPdWScSoolhttFCJEtPZbXojeFBGUCTOBYNVHvBFDyIUaplyMyNHanyTJOxYXdTaDdBKsLKVCAbVIiWCVFZbYDcPyVqVWtRiZsMNBbJjoUpOlVPsDuAYVYyZjfTSwuCigBbKmpHSIvRnRQhJywhOLwQtncJnHHFUlOMCoVbsCbqKQYbnrekrvHGXiQagGUAURMiOHdabUxEgpIdTONvrVpsayHHqQYOMBhtItkIbwFOupgfHCKHFbFnJPYyQCBaSaYpEvLLBjXpMtJXPcxqybQBhBSrmiNeDdvYhIHxXPuRkqbVDwycVTRennVNgOJoaiFaXDviHVZTDcVJTgEBsZILPgMeTCnLSVUhZdBAAaPXMGjUwNeFspNUeUPacwjwJVjVZGAKlcYyGYtsaxutNkMOxxxFMxbftQSnoMImNbXXTFEZIwDuNUJABVRHruDYoHugfjNJWUmOjHKrYZGRJSeaquYEuNxmjRcC`
  * Evidence: `Connection: close`
  * Other Info: `Potential Buffer Overflow. The script closed the connection and threw a 500 Internal Server Error.`
* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=console.png&s=K0w7DsbgSDM6qUh4LWRy
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f,s)`
  * Method: `GET`
  * Parameter: `cmd`
  * Attack: `JMsJdCivNgHJyvmEfvyJaXcYMHxbFMmgKoSProKWORcNtlRYqjZHOokNDsASuiBKcwBPOJsCoyeBfpcDuNaqtfLMGmRQpkagFfmKGIQLdQlMODRSxwPsePxPvCBZFIKyKnbfyWiQDjFYMayfakvdJpuxbQhtRGvIqmtrHOKeeKagUhqidGwbbjcmhLVbgmuLDKycqCYvJicbBdTnmKXLepaJThyQBcinfbcHjImHVLFmJcfsxGlfgNXldVdhTVriNoAoQpMNmjfQhOrVVvAiiByLbCLgMOgLoqAQqDxOqTtHuWdolIdvTsjqPTCnHJfiDQjDBMJKejwjvBeCvQqCZNjZoWjlEIYRrtMlNZaevJOsRIkfHWGoDZylbxeLckDKllLFEwibeSbqheURHPZFVFqWDQrFFXSXRcOLnErfYqchRIrCxNCZhrboVpaKNKrkxaDjbAkFSlbMckRVYTBfjHiBAcnpjWFqeKfCvFqhiXJdJSmWKUwBFvRKquRtbnBLplyRPfiyFaJUGrpmibrsUFNfaumsfkhisXhdhYWKCnxMPdCgrjGopoWOcwfUHMPQrKMhEIbRaRfcXsKqkEgUweHeKiysstxcdapYmXDoZJNdZjMXWEhPfYUSEekUCWoKKLLTCyESKloYCaLkCgGNyVbsAUnVsfoeneQhpTWWRdbeJnccfRXtFUuuOZgSGcunjqlAWtRdTckdfbWYfgadIScpunhbCXjOdGkZrYVfMCjQTMGjmkHBQTYeiYnweRbeWiOtLoYUwMfgJPTAWQwZPMMbhupVbMcudYFwxqZjCBOJkfRKULAVolOumDvVxnLacVxSiCHlLMZvisEukjZFcQymcYNgQxiyYMmewKtbymHrGQLTcgumBAYMAPFahLFBCjEqTfPWBPPWUgxnRVfuOskHPeEMXjbaNdFahlUbcAgUEDYUFGOEHPyxamntEuFaIINprohCHnvxAxIJmAgoRvHrbegbhAnhwJuBUgpRTjYmXedXkccqFwlMuxNawGwBvSXPRTaXeiMTWEsfDvkOlIwFORdMJXJOirkCKMBnknVkuclprtEXALeYTAWgZfcsPQEgYNFlUGlvrEduFxmtgLClGMOEjrqYpbelZGheJDGNWmrMWZPQIBPHLXpmjWXRxArANFurSZfihIAGAJeJhqTMtLYkiBHyEBMhqrMuvNnrdbdShcQMQwMKYBnEOvtaTDhvBxJipceHkJDIiCTReQcMpbJqOqPtYaGeOtrNAIFvlcTeBwFRqLQPdRgvejlnXUOcmvsNXSGoxClwZgHEJQCUDDGfGtASUJZuEbXZHfjTKvNrxSmXprShpgwLeQMSTpanEZTUJMnhCWSDXdtyvdfoQnCEkbxVdROFSvAbZxrHHxQjIvnFiVUCcxJOFNLyraUnwcqBkuNcZrenRgiOSiPAvHmTXCvaMipAxWyqRdGCGpumPfKNbhlxxFOALZsinRDuAxxBeVaibPldOYypsWfGgCdtQrmayieHJvGJwTGHkTwPHhMBHfKfEaxQaixtPtEJVAQdCUZnkQlGEcqZfgHqMwOOlvNdUOHqOiAtGqAdjekJLpwpwMvqYumJqUhiINGjtpDkSgiBILGEXcqAsgyLPBedUBLwPQmWCDVHlSqfYngIrdhPMTpnZEDxNUmWkvgbHvkofwmYBiNUFaoprLavCkTuTpuGjKaZQvoleXolcjyTSJscCpRSvsYGWDNRJNGBEjHMNthbvHhucLTuuQeMrxFUCGoWMpNwgPuYikitFDvtwdWlifFckiJJnFkNCsBDkOqNqpODLmErgGdigxBLrNoTSetxkpXAUcjjbnOxZYYdsUgxqvcVboRghjAWYmQICcvyvpWJavfpcgSBAjZCWpipmLFbKNgmuwwssTpKIpXeQkEDClXKpWtdOFDObtGeoJvUPBVGerIisLOjRunVCFuwOwJaNhDwucVLogegskDqlntbDeoZUbMgOaAecvUAutYwvhYZXoAYDNYtkJyGiyaaamQKfSCYtWnVXwXjsUewopiHkAidFfotUOmEaEeJgrIdlTDaDWSwjVfQDaCyDqQcWsVtrevXHrJlKYTxvLusvPWs`
  * Evidence: `Connection: close`
  * Other Info: `Potential Buffer Overflow. The script closed the connection and threw a 500 Internal Server Error.`


Instances: 4

### Solution

Rewrite the background program using proper return length checking. This will require a recompile of the background executable.

### Reference


* [ https://owasp.org/www-community/attacks/Buffer_overflow_attack ](https://owasp.org/www-community/attacks/Buffer_overflow_attack)


#### CWE Id: [ 120 ](https://cwe.mitre.org/data/definitions/120.html)


#### WASC Id: 7

#### Source ID: 1

### [ Content Security Policy (CSP) Header Not Set ](https://www.zaproxy.org/docs/alerts/10038/)



##### Medium (High)

### Description

Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks, including Cross Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement or distribution of malware. CSP provides a set of standard HTTP headers that allow website owners to declare approved sources of content that browsers should be allowed to load on that page — covered types are JavaScript, CSS, HTML frames, fonts, images and embeddable objects such as Java applets, ActiveX, audio and video files.

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/robots.txt
  * Node Name: `http://localhost:5000/robots.txt`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/sitemap.xml
  * Node Name: `http://localhost:5000/sitemap.xml`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``

Instances: Systemic


### Solution

Ensure that your web server, application server, load balancer, etc. is configured to set the Content-Security-Policy header.

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CSP ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CSP)
* [ https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html ](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)
* [ https://www.w3.org/TR/CSP/ ](https://www.w3.org/TR/CSP/)
* [ https://w3c.github.io/webappsec-csp/ ](https://w3c.github.io/webappsec-csp/)
* [ https://web.dev/articles/csp ](https://web.dev/articles/csp)
* [ https://caniuse.com/#feat=contentsecuritypolicy ](https://caniuse.com/#feat=contentsecuritypolicy)
* [ https://content-security-policy.com/ ](https://content-security-policy.com/)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3

### [ Integer Overflow Error ](https://www.zaproxy.org/docs/alerts/30003/)



##### Medium (Medium)

### Description

An integer overflow condition exists when an integer used in a compiled program extends beyond the range limits and has not been properly checked from the input stream.

* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=console.png
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f)`
  * Method: `GET`
  * Parameter: `__debugger__`
  * Attack: `79279488809473711481352376170462193585623502`
  * Evidence: `HTTP/1.1 500 INTERNAL SERVER ERROR`
  * Other Info: `Potential Integer Overflow. Status code changed on the input of a long string of random integers.`
* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=console.png
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f)`
  * Method: `GET`
  * Parameter: `cmd`
  * Attack: `10811767050146386994933727478608142849870206`
  * Evidence: `HTTP/1.1 500 INTERNAL SERVER ERROR`
  * Other Info: `Potential Integer Overflow. Status code changed on the input of a long string of random integers.`
* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=console.png&s=K0w7DsbgSDM6qUh4LWRy
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f,s)`
  * Method: `GET`
  * Parameter: `__debugger__`
  * Attack: `46160241471696755584218314401040026863824896`
  * Evidence: `HTTP/1.1 500 INTERNAL SERVER ERROR`
  * Other Info: `Potential Integer Overflow. Status code changed on the input of a long string of random integers.`
* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=console.png&s=K0w7DsbgSDM6qUh4LWRy
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f,s)`
  * Method: `GET`
  * Parameter: `cmd`
  * Attack: `01497986472527120692589945868463859657291691`
  * Evidence: `HTTP/1.1 500 INTERNAL SERVER ERROR`
  * Other Info: `Potential Integer Overflow. Status code changed on the input of a long string of random integers.`


Instances: 4

### Solution

In order to prevent overflows and divide by 0 (zero) errors in the application, please rewrite the backend program, checking if the values of integers being processed are within the application's allowed range. This will require a recompilation of the backend executable.

### Reference


* [ https://en.wikipedia.org/wiki/Integer_overflow ](https://en.wikipedia.org/wiki/Integer_overflow)
* [ https://cwe.mitre.org/data/definitions/190.html ](https://cwe.mitre.org/data/definitions/190.html)


#### CWE Id: [ 190 ](https://cwe.mitre.org/data/definitions/190.html)


#### WASC Id: 3

#### Source ID: 1

### [ Missing Anti-clickjacking Header ](https://www.zaproxy.org/docs/alerts/10020/)



##### Medium (Medium)

### Description

The response does not protect against 'ClickJacking' attacks. It should include either Content-Security-Policy with 'frame-ancestors' directive or X-Frame-Options.

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: `x-frame-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: `x-frame-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/debug
  * Node Name: `http://localhost:5000/debug`
  * Method: `GET`
  * Parameter: `x-frame-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/hash%3Fdata=test
  * Node Name: `http://localhost:5000/hash (data)`
  * Method: `GET`
  * Parameter: `x-frame-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `x-frame-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``

Instances: Systemic


### Solution

Modern Web browsers support the Content-Security-Policy and X-Frame-Options HTTP headers. Ensure one of them is set on all web pages returned by your site/app.
If you expect the page to be framed only by pages on your server (e.g. it's part of a FRAMESET) then you'll want to use SAMEORIGIN, otherwise if you never expect the page to be framed, you should use DENY. Alternatively consider implementing Content Security Policy's "frame-ancestors" directive.

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/X-Frame-Options ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/X-Frame-Options)


#### CWE Id: [ 1021 ](https://cwe.mitre.org/data/definitions/1021.html)


#### WASC Id: 15

#### Source ID: 3

### [ Source Code Disclosure - SQL ](https://www.zaproxy.org/docs/alerts/10099/)



##### Medium (Medium)

### Description

Application Source Code was disclosed by the web server. - SQL

* URL: http://localhost:5000/sqli
  * Node Name: `http://localhost:5000/sqli`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `SELECT * FROM users WHERE username `
  * Other Info: ``
* URL: http://localhost:5000/sqli%3Fbtn=Confirm+Pin&pin=ZAP
  * Node Name: `http://localhost:5000/sqli (btn,pin)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `SELECT * FROM users WHERE username `
  * Other Info: ``
* URL: http://localhost:5000/sqli%3Fbtn=Confirm+Pin&pin=ZAP&user=admin
  * Node Name: `http://localhost:5000/sqli (btn,pin,user)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `SELECT * FROM users WHERE username `
  * Other Info: ``
* URL: http://localhost:5000/sqli%3Fuser=admin
  * Node Name: `http://localhost:5000/sqli (user)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `SELECT * FROM users WHERE username `
  * Other Info: ``


Instances: 4

### Solution

Ensure that application Source Code is not available with alternative extensions, and ensure that source code is not present within other files or data deployed to the web server, or served by the web server.

### Reference


* [ https://nhimg.org/twitter-breach ](https://nhimg.org/twitter-breach)


#### CWE Id: [ 540 ](https://cwe.mitre.org/data/definitions/540.html)


#### WASC Id: 13

#### Source ID: 3

### [ Application Error Disclosure ](https://www.zaproxy.org/docs/alerts/90022/)



##### Low (Medium)

### Description

This page contains an error/warning message that may disclose sensitive information like the location of the file that produced the unhandled exception. This information can be used to launch further attacks against the web application. The alert could be a false positive if the error message is found inside a documentation page.

* URL: http://localhost:5000/sqli
  * Node Name: `http://localhost:5000/sqli`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `HTTP/1.1 500 INTERNAL SERVER ERROR`
  * Other Info: ``
* URL: http://localhost:5000/sqli%3Fbtn=Confirm+Pin&pin=ZAP
  * Node Name: `http://localhost:5000/sqli (btn,pin)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `HTTP/1.1 500 INTERNAL SERVER ERROR`
  * Other Info: ``
* URL: http://localhost:5000/sqli%3Fbtn=Confirm+Pin&pin=ZAP&user=admin
  * Node Name: `http://localhost:5000/sqli (btn,pin,user)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `HTTP/1.1 500 INTERNAL SERVER ERROR`
  * Other Info: ``
* URL: http://localhost:5000/sqli%3Fuser=admin
  * Node Name: `http://localhost:5000/sqli (user)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `HTTP/1.1 500 INTERNAL SERVER ERROR`
  * Other Info: ``


Instances: 4

### Solution

Review the source code of this page. Implement custom error pages. Consider implementing a mechanism to provide a unique error reference/identifier to the client (browser) while logging the details on the server side and not exposing them to the user.

### Reference



#### CWE Id: [ 550 ](https://cwe.mitre.org/data/definitions/550.html)


#### WASC Id: 13

#### Source ID: 3

### [ Cross-Origin-Embedder-Policy Header Missing or Invalid ](https://www.zaproxy.org/docs/alerts/90004/)



##### Low (Medium)

### Description

Cross-Origin-Embedder-Policy header is a response header that prevents a document from loading any cross-origin resources that don't explicitly grant the document permission (using CORP or CORS).

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: `Cross-Origin-Embedder-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: `Cross-Origin-Embedder-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `Cross-Origin-Embedder-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``


Instances: 3

### Solution

Ensure that the application/web server sets the Cross-Origin-Embedder-Policy header appropriately, and that it sets the Cross-Origin-Embedder-Policy header to 'require-corp' for documents.
If possible, ensure that the end user uses a standards-compliant and modern web browser that supports the Cross-Origin-Embedder-Policy header (https://caniuse.com/mdn-http_headers_cross-origin-embedder-policy).

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Cross-Origin-Embedder-Policy ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Cross-Origin-Embedder-Policy)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 14

#### Source ID: 3

### [ Cross-Origin-Opener-Policy Header Missing or Invalid ](https://www.zaproxy.org/docs/alerts/90004/)



##### Low (Medium)

### Description

Cross-Origin-Opener-Policy header is a response header that allows a site to control if others included documents share the same browsing context. Sharing the same browsing context with untrusted documents might lead to data leak.

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: `Cross-Origin-Opener-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: `Cross-Origin-Opener-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `Cross-Origin-Opener-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``


Instances: 3

### Solution

Ensure that the application/web server sets the Cross-Origin-Opener-Policy header appropriately, and that it sets the Cross-Origin-Opener-Policy header to 'same-origin' for documents.
'same-origin-allow-popups' is considered as less secured and should be avoided.
If possible, ensure that the end user uses a standards-compliant and modern web browser that supports the Cross-Origin-Opener-Policy header (https://caniuse.com/mdn-http_headers_cross-origin-opener-policy).

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Cross-Origin-Opener-Policy ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Cross-Origin-Opener-Policy)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 14

#### Source ID: 3

### [ Cross-Origin-Resource-Policy Header Missing or Invalid ](https://www.zaproxy.org/docs/alerts/90004/)



##### Low (Medium)

### Description

Cross-Origin-Resource-Policy header is an opt-in header designed to counter side-channels attacks like Spectre. Resource should be specifically set as shareable amongst different origins.

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: `Cross-Origin-Resource-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: `Cross-Origin-Resource-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `Cross-Origin-Resource-Policy`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``


Instances: 3

### Solution

Ensure that the application/web server sets the Cross-Origin-Resource-Policy header appropriately, and that it sets the Cross-Origin-Resource-Policy header to 'same-origin' for all web pages.
'same-site' is considered as less secured and should be avoided.
If resources must be shared, set the header to 'cross-origin'.
If possible, ensure that the end user uses a standards-compliant and modern web browser that supports the Cross-Origin-Resource-Policy header (https://caniuse.com/mdn-http_headers_cross-origin-resource-policy).

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Cross-Origin-Embedder-Policy ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Cross-Origin-Embedder-Policy)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 14

#### Source ID: 3

### [ Permissions Policy Header Not Set ](https://www.zaproxy.org/docs/alerts/10063/)



##### Low (Medium)

### Description

Permissions Policy Header is an added layer of security that helps to restrict from unauthorized access or usage of browser/client features by web resources. This policy ensures the user privacy by limiting or specifying the features of the browsers can be used by the web resources. Permissions Policy provides a set of standard HTTP headers that allow website owners to limit which features of browsers can be used by the page such as camera, microphone, location, full screen etc.

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/robots.txt
  * Node Name: `http://localhost:5000/robots.txt`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/sitemap.xml
  * Node Name: `http://localhost:5000/sitemap.xml`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``

Instances: Systemic


### Solution

Ensure that your web server, application server, load balancer, etc. is configured to set the Permissions-Policy header.

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Permissions-Policy ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Permissions-Policy)
* [ https://developer.chrome.com/blog/feature-policy/ ](https://developer.chrome.com/blog/feature-policy/)
* [ https://scotthelme.co.uk/a-new-security-header-feature-policy/ ](https://scotthelme.co.uk/a-new-security-header-feature-policy/)
* [ https://w3c.github.io/webappsec-feature-policy/ ](https://w3c.github.io/webappsec-feature-policy/)
* [ https://www.smashingmagazine.com/2018/12/feature-policy/ ](https://www.smashingmagazine.com/2018/12/feature-policy/)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3

### [ Server Leaks Version Information via "Server" HTTP Response Header Field ](https://www.zaproxy.org/docs/alerts/10036/)



##### Low (High)

### Description

The web/application server is leaking version information via the "Server" HTTP response header. Access to such information may facilitate attackers identifying other vulnerabilities your web/application server is subject to.

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Werkzeug/3.1.9 Python/3.9.25`
  * Other Info: ``
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Werkzeug/3.1.9 Python/3.9.25`
  * Other Info: ``
* URL: http://localhost:5000/robots.txt
  * Node Name: `http://localhost:5000/robots.txt`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Werkzeug/3.1.9 Python/3.9.25`
  * Other Info: ``
* URL: http://localhost:5000/sitemap.xml
  * Node Name: `http://localhost:5000/sitemap.xml`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Werkzeug/3.1.9 Python/3.9.25`
  * Other Info: ``
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `Werkzeug/3.1.9 Python/3.9.25`
  * Other Info: ``

Instances: Systemic


### Solution

Ensure that your web server, application server, load balancer, etc. is configured to suppress the "Server" header or provide generic details.

### Reference


* [ https://httpd.apache.org/docs/current/mod/core.html#servertokens ](https://httpd.apache.org/docs/current/mod/core.html#servertokens)
* [ https://learn.microsoft.com/en-us/previous-versions/msp-n-p/ff648552(v=pandp.10) ](https://learn.microsoft.com/en-us/previous-versions/msp-n-p/ff648552(v=pandp.10))
* [ https://www.troyhunt.com/shhh-dont-let-your-response-headers/ ](https://www.troyhunt.com/shhh-dont-let-your-response-headers/)


#### CWE Id: [ 497 ](https://cwe.mitre.org/data/definitions/497.html)


#### WASC Id: 13

#### Source ID: 3

### [ X-Content-Type-Options Header Missing ](https://www.zaproxy.org/docs/alerts/10021/)



##### Low (Medium)

### Description

The Anti-MIME-Sniffing header X-Content-Type-Options was not set to 'nosniff'. This allows older versions of Internet Explorer and Chrome to perform MIME-sniffing on the response body, potentially causing the response body to be interpreted and displayed as a content type other than the declared content type. Current (early 2014) and legacy versions of Firefox will use the declared content type (if one is set), rather than performing MIME-sniffing.

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold this scan rule will not alert on client or server error responses.`
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold this scan rule will not alert on client or server error responses.`
* URL: http://localhost:5000/debug
  * Node Name: `http://localhost:5000/debug`
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold this scan rule will not alert on client or server error responses.`
* URL: http://localhost:5000/hash%3Fdata=test
  * Node Name: `http://localhost:5000/hash (data)`
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold this scan rule will not alert on client or server error responses.`
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold this scan rule will not alert on client or server error responses.`

Instances: Systemic


### Solution

Ensure that the application/web server sets the Content-Type header appropriately, and that it sets the X-Content-Type-Options header to 'nosniff' for all web pages.
If possible, ensure that the end user uses a standards-compliant and modern web browser that does not perform MIME-sniffing at all, or that can be directed by the web application/web server to not perform MIME-sniffing.

### Reference


* [ https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/compatibility/gg622941(v=vs.85) ](https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/compatibility/gg622941(v=vs.85))
* [ https://owasp.org/www-community/Security_Headers ](https://owasp.org/www-community/Security_Headers)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3

### [ Information Disclosure - Sensitive Information in URL ](https://www.zaproxy.org/docs/alerts/10024/)



##### Informational (Medium)

### Description

The request appeared to contain sensitive information leaked in the URL. This can violate PCI and most organizational compliance policies. You can configure the list of strings for this check to add or remove values specific to your environment.

* URL: http://localhost:5000/sqli%3Fbtn=Confirm+Pin&pin=ZAP&user=admin
  * Node Name: `http://localhost:5000/sqli (btn,pin,user)`
  * Method: `GET`
  * Parameter: `user`
  * Attack: ``
  * Evidence: `user`
  * Other Info: `The URL contains potentially sensitive information. The following string was found via the pattern: user
user`
* URL: http://localhost:5000/sqli%3Fuser=admin
  * Node Name: `http://localhost:5000/sqli (user)`
  * Method: `GET`
  * Parameter: `user`
  * Attack: ``
  * Evidence: `user`
  * Other Info: `The URL contains potentially sensitive information. The following string was found via the pattern: user
user`


Instances: 2

### Solution

Do not pass sensitive information in URIs.

### Reference



#### CWE Id: [ 598 ](https://cwe.mitre.org/data/definitions/598.html)


#### WASC Id: 13

#### Source ID: 3

### [ Information Disclosure - Suspicious Comments ](https://www.zaproxy.org/docs/alerts/10027/)



##### Informational (Medium)

### Description

The response appears to contain suspicious comments which may help an attacker.

* URL: http://localhost:5000/sqli%3F__debugger__=yes&cmd=resource&f=debugger.js
  * Node Name: `http://localhost:5000/sqli (__debugger__,cmd,f)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `// Prevent page from refreshing.`
  * Other Info: `The following pattern was used: \bFROM\b and was detected in likely comment: "// Prevent page from refreshing.", see evidence field for the suspicious comment/snippet.`


Instances: 1

### Solution

Remove all comments that return information that may help an attacker and fix any underlying problems they refer to.

### Reference



#### CWE Id: [ 615 ](https://cwe.mitre.org/data/definitions/615.html)


#### WASC Id: 13

#### Source ID: 3

### [ Modern Web Application ](https://www.zaproxy.org/docs/alerts/10109/)



##### Informational (Medium)

### Description

The application appears to be a modern web application. If you need to explore it automatically then the Client Spider may well be more effective than the standard one.

* URL: http://localhost:5000/sqli
  * Node Name: `http://localhost:5000/sqli`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script src="?__debugger__=yes&amp;cmd=resource&amp;f=debugger.js"></script>`
  * Other Info: `No links have been found while there are scripts, which is an indication that this is a modern web application.`
* URL: http://localhost:5000/sqli%3Fbtn=Confirm+Pin&pin=ZAP
  * Node Name: `http://localhost:5000/sqli (btn,pin)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script src="?__debugger__=yes&amp;cmd=resource&amp;f=debugger.js"></script>`
  * Other Info: `No links have been found while there are scripts, which is an indication that this is a modern web application.`
* URL: http://localhost:5000/sqli%3Fbtn=Confirm+Pin&pin=ZAP&user=admin
  * Node Name: `http://localhost:5000/sqli (btn,pin,user)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script src="?__debugger__=yes&amp;cmd=resource&amp;f=debugger.js"></script>`
  * Other Info: `No links have been found while there are scripts, which is an indication that this is a modern web application.`
* URL: http://localhost:5000/sqli%3Fuser=admin
  * Node Name: `http://localhost:5000/sqli (user)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: `<script src="?__debugger__=yes&amp;cmd=resource&amp;f=debugger.js"></script>`
  * Other Info: `No links have been found while there are scripts, which is an indication that this is a modern web application.`


Instances: 4

### Solution

This is an informational alert and so no changes are required.

### Reference




#### Source ID: 3

### [ Storable and Cacheable Content ](https://www.zaproxy.org/docs/alerts/10049/)



##### Informational (Medium)

### Description

The response contents are storable by caching components such as proxy servers, and may be retrieved directly from the cache, rather than from the origin server by the caching servers, in response to similar requests from other users. If the response data is sensitive, personal or user-specific, this may result in sensitive information being leaked. In some cases, this may even result in a user gaining complete control of the session of another user, depending on the configuration of the caching components in use in their environment. This is primarily an issue where "shared" caching servers such as "proxy" caches are configured on the local network. This configuration is typically found in corporate or educational environments, for instance.

* URL: http://localhost:5000
  * Node Name: `http://localhost:5000`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: `In the absence of an explicitly specified caching lifetime directive in the response, a liberal lifetime heuristic of 1 year was assumed. This is permitted by rfc7234.`
* URL: http://localhost:5000/
  * Node Name: `http://localhost:5000/`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: `In the absence of an explicitly specified caching lifetime directive in the response, a liberal lifetime heuristic of 1 year was assumed. This is permitted by rfc7234.`
* URL: http://localhost:5000/robots.txt
  * Node Name: `http://localhost:5000/robots.txt`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: `In the absence of an explicitly specified caching lifetime directive in the response, a liberal lifetime heuristic of 1 year was assumed. This is permitted by rfc7234.`
* URL: http://localhost:5000/sitemap.xml
  * Node Name: `http://localhost:5000/sitemap.xml`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: `In the absence of an explicitly specified caching lifetime directive in the response, a liberal lifetime heuristic of 1 year was assumed. This is permitted by rfc7234.`
* URL: http://localhost:5000/xss%3Fname=Visitor
  * Node Name: `http://localhost:5000/xss (name)`
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: `In the absence of an explicitly specified caching lifetime directive in the response, a liberal lifetime heuristic of 1 year was assumed. This is permitted by rfc7234.`

Instances: Systemic


### Solution

Validate that the response does not contain sensitive, personal or user-specific information. If it does, consider the use of the following HTTP response headers, to limit, or prevent the content being stored and retrieved from the cache by another user:
Cache-Control: no-cache, no-store, must-revalidate, private
Pragma: no-cache
Expires: 0
This configuration directs both HTTP 1.0 and HTTP 1.1 compliant caching servers to not store the response, and to not retrieve the response (without validation) from the cache, in response to a similar request.

### Reference


* [ https://datatracker.ietf.org/doc/html/rfc7234 ](https://datatracker.ietf.org/doc/html/rfc7234)
* [ https://datatracker.ietf.org/doc/html/rfc7231 ](https://datatracker.ietf.org/doc/html/rfc7231)
* [ https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html ](https://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html)


#### CWE Id: [ 524 ](https://cwe.mitre.org/data/definitions/524.html)


#### WASC Id: 13

#### Source ID: 3

### [ User Agent Fuzzer ](https://www.zaproxy.org/docs/alerts/10104/)



##### Informational (Medium)

### Description

Check for differences in response based on fuzzed User Agent (eg. mobile sites, access as a Search Engine Crawler). Compares the response statuscode and the hashcode of the response body with the original response.

* URL: http://localhost:5000/debug
  * Node Name: `http://localhost:5000/debug`
  * Method: `GET`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)`
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/debug
  * Node Name: `http://localhost:5000/debug`
  * Method: `GET`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0)`
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/debug
  * Node Name: `http://localhost:5000/debug`
  * Method: `GET`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1)`
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/debug
  * Node Name: `http://localhost:5000/debug`
  * Method: `GET`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/5.0 (Windows NT 10.0; Trident/7.0; rv:11.0) like Gecko`
  * Evidence: ``
  * Other Info: ``
* URL: http://localhost:5000/debug
  * Node Name: `http://localhost:5000/debug`
  * Method: `GET`
  * Parameter: `Header User-Agent`
  * Attack: `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3739.0 Safari/537.36 Edg/75.0.109.0`
  * Evidence: ``
  * Other Info: ``

Instances: Systemic


### Solution



### Reference


* [ https://owasp.org/www-project-web-security-testing-guide/ ](https://owasp.org/www-project-web-security-testing-guide/)



#### Source ID: 1


