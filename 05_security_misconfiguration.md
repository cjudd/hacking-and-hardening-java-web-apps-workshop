# Security Misconfiguration

Servers and environments must be configured securely properly to insure good security. Defaults are often insecure.

## HTTPS

All web traffic must be encrypted during transit meaning it must use TLS over HTTP.

1. Visit [SSL Labs](https://www.ssllabs.com/ssltest/) and test your site or your banks HTTPS.

The site will provide a grade as well important details such as the certificate details and chain in addition to protocols and Cipher suites.

## Headers

Headers can be an important part of security indepth.

1. Visit [Security Headers](https://securityheaders.com) and test your site.

## Cookies

Cookies need to be secure to prevent them from being captured by man in the middle attacks or XSS vulnerabilities from stealing them.

1. Login to your site.

2. Use browser's inspect feature and cookies.

NOTE: Chrome Application tab > Cookies > domain.

Make sure your sensitive cookies such as JSESSIONID is marked as HTTP Only and Secure.

## Observations

* Before making any changes suggested above make sure you understand whether make the changes could break yoursite.
