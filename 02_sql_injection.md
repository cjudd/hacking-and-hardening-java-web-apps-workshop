# SQL Injection

The ZAP scan itentified a severe vulnerability of SQL Injection. Injection risks has always been and remains the number 1 risk in the [OWAS 10 Ten](https://www.owasp.org/index.php/Top_10-2017_Top_10) list. 
In this lab, you will learn how to use [sqlmap](http://sqlmap.org/) to test and validate SQL injection vulnerabilities.

NOTE: Many developers think SQL Injection vulnerabilities are a thing of the past. Unfortunately they are not. In the 2016 US presidential election for example, not one but [two state's election databases were exfiltrated](http://thehackernews.com/2016/08/election-system-hack.html?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed:+TheHackersNews+(The+Hackers+News+-+Security+Blog)&_m=3n.009a.1311.gs0ao085y3.rkc&m=1). Evidance points to the attackers actually using sqlmap to perform the attack.

## Using sqlmap

Which request did the scan identify as having the SQL injection vulnerability? Which field in that request was vulnerable?

HINT: http://localhost:8080/results?searchTerm=%27

1. Open a new terminal.

2. Invoke sqlmap providing the url of the vulnerable request. If it is a GET request, specify the vulnerable parameter with an *. Accept all the default anwsers to the questions asked until "do you want to store hashes to a temporary file for eventual futher processing with other tools?", choose y. When prompted for "what dictionary do you want to use?", choose 1.

```
sqlmap -u http://localhost:8080/results?searchTerm=* --dump-all
```

## Observations

* SQL Injection is incredibly easy to exploit. Attackers don't even need to know there are boolean-based blind, error-based, etc attacks.
* It doesn't matter how strong your network or perimeter security is, if your application is vulnerable to a SQL injection, an attacker can get your entire database.
* Passwords can easily be reversed engineered using rainbow tables if passwords don't properly use strong hashes, unique salts and a work factor.
* If the database credentials are open too much, the attacker maybe able to access other databases on the same server.
* Data is written to CSV files making it easy for attackers to import them into Excel.
* Injection attacks are not just SQL but any type of interpreter including search engines, LDAP, operating system

## Solutions

* Parameterized Queries
* Encoding - [OWASP Enterprise Security API](https://github.com/ESAPI/esapi-java-legacy) unfortunatly considered deprecated