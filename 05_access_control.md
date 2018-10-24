# Access Control

Many sites use security through obscurity by hiding urls from the user if they shouldn't have access but don't do adequate of validating on the serverside the user has the appropriate permissions. 

## Access Admin Pages

1. Login as admin and notice the url for the admin page. Pretty cleaver and tricky?

2. Logout out.

3. Try navigating to [http://localhost:8080/admin](http://localhost:8080/admin).

4. Login as blogger1 and try going to [http://localhost:8080/admin](http://localhost:8080/admin).

What happened? Does the blogger1 user see the admin link?

HINT: non logged in user can not get to admin page but any logged in user can.

## Observations

* This is the most common issue I have seen in applications I work on.

## Solutions

* Use Spring Security Annotations
* Programmatically check permissions