# Cross-site Request Forgery (CSRF)

Attacker forces a login victim's browser to send a forged request that looks valid.

## CSRF Tester

1. Run OWASP CSRFTester

```
cd ~/workspaces/CSRFTester-1.0
java -classpath .:lib/concurrent.jar:OWASP-CSRFTester-1.0.jar org.owasp.csrftester.CSRFTester
```

2. Change Iceweasel's proxy to point to localhost 8008.

3. Navigate to http://localhost:8080/post.

4. Start recording in OWASP CSRFTester.

5. Submit a post.

6. Stop recording.

7. Delete any extra rows besides the post submission.

8. Change the title and content parameters to say something else.

9. Generate HTML using your preferred report type (form, iframe, img, xhr, link).

10. Notice just rending the local page submits data to Wordy Ninja Blog.

## Logout

Most users don't take the time to logout of sites. Unfortunately if that site is vulnerable to a CSRF attack, it lengths the target time.

1. Visit [https://robinlinus.github.io/socialmedia-leak/](https://robinlinus.github.io/socialmedia-leak/) to determine if there are any social media sites you really don't need to be logged into right now.

## Observations

* Attackers using social media (email, twitter, facebook, ads, url shortners, etc) can trick somebody into just visiting a page to do the damage.

## Solutions

* CSRF tokens
* Force logouts