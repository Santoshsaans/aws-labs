\# 🍪 AWS: Sticky Sessions on an Application Load Balancer



Used the same ALB setup from the previous lab and added one more feature: \*\*sticky sessions\*\*.



\---



\## 😩 The problem



By default, the ALB uses \*\*round-robin\*\*, so every refresh can go to a different server. In my lab, the page kept switching between Virginia and Europe.



That's a problem for apps that keep your session (a login or a shopping cart) on \*\*one\*\* server. If the next request goes to another server, that server doesn't know you.



\## ✅ The solution: Stickiness



The ALB \*\*remembers which server you were sent to\*\* and keeps sending you back to it. It does this with a \*\*cookie\*\*.



\---



\## What I did, step by step



\### Step 1: Started from my existing setup



ALB, target group, and two EC2 instances (Virginia and Europe) from the previous lab. No new resources were needed.



!\[Existing setup](screenshots/01-existing-setup.jpg)



\### Step 2: Opened the target group attributes



```

EC2 → Target Groups → my target group → Attributes tab → Edit

```



Stickiness was \*\*off\*\* by default.



!\[Attributes before](screenshots/02-target-group-attributes.jpg)



\### Step 3: Turned on stickiness



| Setting | Value |

|---|---|

| Type | Load balancer generated cookie (duration-based) |

| Duration | 5 minutes |



!\[Enable stickiness](screenshots/03-enable-stickiness.jpg)



\### Step 4: Saved the changes



!\[Stickiness saved](screenshots/04-stickiness-saved.jpg)



\### Step 5: Tested it



I opened the ALB DNS name in the browser and refreshed many times.



| | Result |

|---|---|

| 🔁 \*\*Before\*\* | Virginia → Europe → Virginia → Europe |

| 📌 \*\*After\*\* | Europe → Europe → Europe → Europe |



!\[Before: round robin](screenshots/05-before-round-robin.jpg)



!\[After: same server](screenshots/06-after-sticky-same-server.jpg)



The ALB set a cookie in my browser, and every request went to the same server.



!\[AWSALB cookie](screenshots/07-awsalb-cookie.jpg)



In an \*\*Incognito window\*\* (no cookie), the ALB could pick either server.



!\[Incognito test](screenshots/08-incognito-test.jpg)



\---



\## 🧠 What I learned



\- ✅ Stickiness is a \*\*target group\*\* setting, not a load balancer setting

\- ✅ There are \*\*2 types\*\*:

&#x20; - \*\*Duration-based:\*\* the ALB creates the cookie

&#x20; - \*\*Application-based:\*\* your app creates the cookie

\- ✅ The ALB uses a cookie (`AWSALB`) to remember the server. After the duration expires, you may be sent to a different one

\- ✅ Useful for apps that store session data on one server

\- ⚠️ \*\*Trade-off:\*\* traffic may become uneven, because "sticky" users stay on one server even when it's busy



\## 🔒 Note on HTTPS



I skipped the HTTPS part of the course for now, since it needs a \*\*domain name\*\* for an ACM certificate. The idea: the certificate goes on the ALB listener (`HTTPS:443`) and the ALB handles the encryption (\*\*TLS termination\*\*). I'll try it hands-on when I have a domain.



\---



\## 💡 Takeaway



Small settings on a load balancer can change how an app behaves. The same setup gave two different results just by changing one attribute. 🚀



\## ⏭️ Next



More load balancer types and \*\*Auto Scaling\*\*.



`#AWS` `#EC2` `#ApplicationLoadBalancer` `#StickySessions` `#LoadBalancer` `#CloudComputing` `#LearningInPublic` `#CyberSecurity` `#BTech`

