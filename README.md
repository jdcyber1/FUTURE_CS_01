# FUTURE_CS_01
Internship Report: 1.Web Application Security Testing

1. Introduction
During the internship, security testing was conducted on sample vulnerable web applications to identify and understand common web vulnerabilities such as SQL Injection, Cross-Site Scripting (XSS), and Authentication flaws.
 The objective was to practically apply ethical hacking and penetration testing techniques using industry-standard approaches.

2. Tools and Resources Used
Burp Suite Community Edition – HTTP Proxy and Request Capturing


SQLMap – Automated SQL Injection Exploitation


Manually collected XSS payloads (from LinkedIn and other sources)


Browser – Manual XSS Testing


PortSwigger Labs – Authentication flaw testing


Notepad++ – Request file analysis



3. Methodology
3.1 SQL Injection Testing
Visited the target website: http://testphp.vulnweb.com/search.php?test=query.


Captured HTTP requests using Burp Suite and saved the captured request into a .txt file (request.txt).


Used SQLMap with the -r option (request file) instead of directly attacking the live site.


SQLMap Commands used:

sqlmap -r request.txt --dbs
sqlmap -r request.txt -D acuart --tables
sqlmap -r request.txt -D acuart -T users --dump

Successfully retrieved databases, tables, and extracted user data from the vulnerable application.
3.2 Cross-Site Scripting (XSS) Testing
Accessed the practice website: https://xss-game.appspot.com/.


Did not use any automated tool.


Manually collected random XSS payloads from LinkedIn and online resources.


Tested various payloads manually by injecting them into input fields and URLs.


Example Payloads Used:
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg onload=alert('XSS')>

Successfully triggered JavaScript alerts and completed various XSS challenges.




3.3 Authentication Flaw Testing
Target: PortSwigger Lab Username Enumeration via Different Responses


Method used: Burp Suite Intruder - Sniper Attack


Steps Followed:
Captured the login request using Burp Proxy after submitting random invalid credentials.


Sent the request to Intruder and selected the username parameter as the payload position (§invalid-username§).


Attack 1: Username Enumeration


Selected Simple list payload type and added a list of candidate usernames.


Started a Sniper Attack.


Observed the Length column: One response was longer and contained the message "Incorrect password" instead of "Invalid username."


Identified the valid username based on this difference.


Attack 2: Password Brute Force
Cleared positions, selected the password parameter for payload.


Set the username to the discovered valid username.


Added a list of common passwords.


Started a second Sniper Attack.


Observed Status column:


All responses were 200 OK except one 302 Found (redirect).


The password causing the 302 response was identified as the correct password.







Final Step:


Used the discovered username and password to log in successfully.


Gained access to the user account page and solved the lab.





