## IAAA Failures(1/3)

### Task 02: What is IAAA?

**What does IAAA stand for?**

`Identity, Authentication, Authorisation, Accountability`

### A01: Broken Access Control

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
     
## Application Design Flaws(2/3)

### AS02: Security Misconfigurations

Challenge Link(Instance): `http://10.49.154.138:5002`

<img width="1578" height="418" alt="image" src="https://github.com/user-attachments/assets/7cfa14fd-a796-45bc-8198-5b2b6265096c" />

**Writeup:**

Directory bruteforcing `/api` endpoints reveals few other directories. In `/api/user/admin` the flag can be retrieved.

<img width="858" height="438" alt="image" src="https://github.com/user-attachments/assets/6b3d0035-9390-4001-b44f-59b30dab9519" />


<img width="702" height="289" alt="image" src="https://github.com/user-attachments/assets/6a38d8a8-5b96-4ad8-8f7a-555f1d30e6a2" />


Flag: `THM{V3RB0S3_3RR0R_L34K}`

### AS03: Software Supply Chain Failures

Here they have given one python file and the challenge link.

Challenge Link(Instance): `http://10.49.154.138:5003`

<img width="1763" height="774" alt="image" src="https://github.com/user-attachments/assets/21ce970e-b56c-422c-9bf2-f5744b7e4893" />

We have two endpoints to hit here,  one is `/api/health` and `/api/process`.

`/api/health` - Doesn't seem interesting

Let’s hit `/api/process`. Make sure to include the `Content-Type: application/json` header, since it’s a RESTful API that works only with JSON. Also, it’s a `POST` request, so it requires a parameter which is `data`.

<img width="1496" height="547" alt="image" src="https://github.com/user-attachments/assets/0f50d58e-b9fc-48c9-8ce4-41eb06e811c2" />

So we need to find the value for the data parameter, Lets anaylse the python code for any leaks.

<img width="688" height="443" alt="image" src="https://github.com/user-attachments/assets/fafeffbb-13d7-45da-8448-29aa2aff07a7" />


```
if data == 'debug': # Value Leaked Here
            return jsonify(debug_info())
```

So our value is `debug`, which reveals the flag.

<img width="1514" height="615" alt="image" src="https://github.com/user-attachments/assets/45f3eb46-cf5e-4bd6-b6ed-bc66e325c146" />


Flag: `THM{SUPPLY_CH41N_VULN3R4B1L1TY}`
