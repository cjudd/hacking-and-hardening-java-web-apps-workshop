# Cross-site Scripting (XSS)

The ZAP scan itentified severe cross site scripting (XSS) vulnerabilities of both the reflective and stored variety allowing an attacker to send untrusted JavaScript to be intepreted by the browser.

## Reflective attack

A reflective attack is in the request itself (frequently the URL) and the vulnerability is injected into the page verbatim.

Which request was identified as being vulnerable to a reflective attack? How would an attacker trick the user into executing the malicious request? How could the attacker use the vulnerability?

HINT: http://localhost:8080/results?searchTerm=<malicious payload>

NOTE: Chrome and Safari provide additional production against some times of reflective attacks.


1. In the Iceweasel, navigate to [http://localhost:8080/results?searchTerm='<script>alert(document.cookie)</script>](http://localhost:8080/results?searchTerm=%27%3Cscript%3Ealert%28document.cookie%29%3C/script%3E)

This request will force an invalid SQL grammer exception because of the single quote(') and reflect the payload back to the user's browser causing the JavaScript to be executed. This payload simply displays the users cookies in an alert but it could have just as easily sent it to an attacker so they could impersonate the user on that site.

## Store attack

A stored attack occurs when the attacker stores data in a data store (database, file, etc) and is triggered by a user visiting the page.

Which request was identified as being vulnerable to a reflective attack?  How would an attacker trick the user into executing the malicious request? How could the attacker use the vulnerability?

HINT: http://localhost:8080/post

1. As an admin or blogger, enter a post containing the following:

```
<script>$(“body").css("color","red");</script>
```

This request is a relatively harmless defacing of the site. But it could have easily done something more malicious such as stealing session cookies again.

## Observations

* XSS attacks can be used to hijack user sessions, deface websites or redirect users to malicious sites.
* Reflective XSS attacks are often performed via social media: email, twitter, facebook, url shortners.

## Solutions

* Escape/Encode - [OWASP Java Endoder Project](https://github.com/OWASP/owasp-java-encoder)
* Sanitize - [OWASP Java HTML Sanitizer](https://github.com/owasp/java-html-sanitizer) and [jsoup Java HTML Sanitizer](http://jsoup.org/cookbook/cleaning-html/whitelist-sanitizer)