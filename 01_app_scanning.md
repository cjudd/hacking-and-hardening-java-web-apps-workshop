# Application Scanning

In this lab, you will learn how to use the open source app scanning tool [ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project) from [OWASP](https://www.owasp.org) to identify vulnerabilities in your application.

NOTE: There are other app scanning tools available in the market including [Burp Suite](https://portswigger.net/burp) which is also included in Kali Linux.

## Launch and Configure ZAP

1. Start ZAP using Applications > 03 - Web Application Analysis > owasp-zap.

It is likely you will get the error "Cannot listen on port localhost:8080". This is because ZAP is written in Java and like all good Java applications they must listen on port 8080 but the web application has already bind to that port. Therefore, you must change the ZAP port.

2. Cancel all the prompts.

3. To change the listening port go to Tools > Options > Local Proxy and change the port to 8085.

## Run Basic Scan/Attack

WARNING: Do not use ZAP on a production application especially one you don't have written permisison to test. It can be illegal and depending on how you run it, it can pollute your database.

1. On the Quick Start tab, enter http://localhost:8080 into the URL to attack field and press the Attack button.

This will spider your application looking for links and run a very basic scan on the application. Once complete, it will show you alerts organized by severity in the Alerts tab. Expanding a category of vulneratiblities will reveal the vulnerable url. Selecting that url will expose the raw request and response data as well as information about the vulnerability including a descript, CVE number, possible solutions and references to more information.

## Run an Advanced Scan

Unfortunately using the Quick Start mechanism is not a very thorough scan. For example, it won't be able to login to the application so any vulnerabilites behind authentication won't be identified. A better way is for it to proxy a user testing all end points and then performing a scan based on the history.

1. Configure your browser to use the ZAP proxy. In Iceweasel go to Preferences > Advanced > Network > Settings. Select Manual proxy configurations and enter localhost and 8085 or what ever you configured ZAP's proxy port to earlier in the HTTP Proxy fields. Also clear out the No Proxy for field.

2. Navigate the entire application including logging in as admin, signing up, creating a new post, and selecting the Administration link.

You should see under http://localhost:8080 in the Sites tree new requests show up that the Quick Start couldn't find.

3. To perform a more advanced scan/attack, right click on http://localhost:8080 in tree choosing Attack > Active Scan and pressing Start Scan.

After this scan, you should see more and more severe alerts identified.

## Configuring Login (optional)

The previous advanced scan used the session cookies from the proxying. Unfortunately, at some point those cookies will expire and the tests will fail. ZAP can be configured to use different usernames and passwords to login.

1. Find the login request, POST:login(password,username). Right click and choose Flag as Context > Default Context : Form-based Auth Login Request.

2. Change the Password Parameter to be password.

3. Next identify regular expressions ZAP can use to determine if a user is logged in or not.

Regex pattern identified in Logged in response messages = Logout
Regex pattern identified in Logged Out response message = Login

4. In the tree, choose Users. Add users you would like to simulate and enable them.

5. This time when you active scan (Attack > Active Scan), you can select a context and a specific user.

## Insane Scan (optional)

By default the scan is set at a medium level. If you want to make it more intensive, you can increase that.

1. Start the scan as you normally would, Attack > Active Scan. Check the Show Advanced Options. On the Input Vector tab, you can test additional targets such as url paths, headers and cookies. On the Policy tab, you can increase the thresholds to High and Insane.

## Observations

* Scanning can produce false positives so take them with a grain of salt and validate.