## OWASP Top 10 2025: IAAA Failures(1/3)

### Task 02: What is IAAA?

**What does IAAA stand for?**

`Identity, Authentication, Authorisation, Accountability`

### Task 03 A01: Broken Access Control

1)  **If you don't get access to more roles but can view the data of another users, what type of privilege escalation is this?**
 
     Answer: `Horizontal`

2) **What is the note you found when viewing the user's account who had more than $ 1 million?**

     Flag: `THM{Found.the.Millionare!}`

**Writeup:** 

The site is vulnerable to IDOR vulnerability by changing the id from 5 to 7 gives access to other's profile were the flag is hidden.

<img width="916" height="312" alt="image" src="https://github.com/user-attachments/assets/45ba51cd-ac62-402e-96f8-b535c350b651" />


### A07: Authentication Failures

1) **What is the flag on the admin user's dashboard?**

**Writeup:**
Here we can create duplicate account using the same username `admin` in different cases eg. `aDMIN`

<img width="427" height="424" alt="image" src="https://github.com/user-attachments/assets/711d7901-7a99-4821-bab3-b389650ed091" />



Now login with the same username which is Admin account authentication failure.


<img width="914" height="430" alt="image" src="https://github.com/user-attachments/assets/015520e6-82ae-461f-bd73-51c977db02f6" />



**Flag:** `THM{Account.confusion.FTW!}`
   
### A09: Logging & Alerting Failures

1) **It looks like an attacker tried to perform a brute-force attack, what is the IP of the attacker?**
      
Answer: `203.0.113.45`

**Why?**

<img width="878" height="421" alt="image" src="https://github.com/user-attachments/assets/b50fd6b2-3f0e-45ed-9b66-21afd455ecfc" />

We can see the timing between each request is very less which is in miliseconds, So we can confirm that this is an automated bruteforce trial.

2) **Looks like they were able to gain access to an account! What is the username associated with that account?**

   **Answer:** `admin`


3) **What action did the attacker try to do with the account? List the endpoint the accessed.**

     **Answer:** `/supersecretadminstuff`
     
