\# ⚖️ Built My First Application Load Balancer on AWS



Set up one \*\*Application Load Balancer (ALB)\*\* with two backend EC2 web servers, using the launch templates from the previous lab.



\---



\## Architecture



```

&#x20;           Internet

&#x20;              ↓

&#x20;  Application Load Balancer (HTTP :80)

&#x20;       ↓                    ↓

&#x20;  EC2 (Virginia)      EC2 (Europe)

&#x20;    in AZ 1              in AZ 2

```



\---



\## What I did, step by step



\### Step 1: Launched 2 EC2 instances from launch templates



I used the \*\*Virginia\*\* and \*\*Europe\*\* templates. All settings were filled in automatically, and I only added a \*\*Name tag\*\* to each one. Each server runs Apache and shows its own page, so I can tell which one is responding.



!\[Two instances running](screenshots/01-two-instances-running.jpg)



\### Step 2: Created a Target Group



| Setting | Value |

|---|---|

| Target type | Instances |

| Protocol / port | HTTP, 80 |

| Health check path | `/index.html` |

| Targets | Both EC2 instances |



!\[Create target group](screenshots/02-create-target-group.jpg)



!\[Targets registered](screenshots/03-targets-registered.jpg)



\### Step 3: Created the Application Load Balancer



| Setting | Value |

|---|---|

| Scheme | Internet-facing |

| Availability Zones | The two AZs where my instances were running |



!\[Create ALB](screenshots/04-create-alb.jpg)



\### Step 4: Created a separate Security Group for the ALB



I didn't use the default one. I created a new security group that allows \*\*HTTP (port 80) from anywhere\*\*.



!\[ALB security group](screenshots/05-alb-security-group.jpg)



\### Step 5: Added an HTTP listener on port 80



The listener \*\*forwards all traffic\*\* to my target group.



!\[Listener](screenshots/06-listener-forward.jpg)



!\[Targets healthy](screenshots/07-targets-healthy.jpg)



\### Step 6: Tested it! 🎉



I copied the ALB's \*\*public DNS name\*\*, opened it in the browser with `http://`, and refreshed a few times.



🔁 Result: \*\*Virginia → Europe → Virginia → Europe\*\*



The traffic was shared between both servers. This is the \*\*round-robin\*\* algorithm at work.



!\[ALB shows Virginia](screenshots/08-alb-virginia.jpg)



!\[ALB shows Europe](screenshots/09-alb-europe.jpg)



\---



\## 🧠 What I learned



\- ✅ An ALB \*\*spreads traffic across multiple servers\*\*, so no single server gets overloaded

\- ✅ \*\*Health checks\*\* keep watching your instances. The target group sends a request to `/index.html`, and a `200 OK` response means the instance is healthy

\- ✅ \*\*Unhealthy instances stop getting traffic\*\* automatically

\- ✅ \*\*Best practice:\*\* the web server security group should accept traffic \*\*only from the ALB's security group\*\*, not from the whole internet

\- ✅ In real projects, the ALB goes in a \*\*public subnet\*\* and the EC2 instances in \*\*private subnets\*\*. I'll learn this when I reach VPC and networking.



\## 💡 Takeaway



This is how real websites stay available even if one server goes down. 🚀



\## ⏭️ Next



More load balancer exercises and \*\*Auto Scaling\*\*.



`#AWS` `#EC2` `#LoadBalancer` `#ApplicationLoadBalancer` `#CloudComputing` `#LearningInPublic` `#DevOps` `#CyberSecurity` `#BTech`



