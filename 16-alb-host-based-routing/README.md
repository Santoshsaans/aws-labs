\# 🌐 AWS: Host-Based Routing on the ALB



Last part of my Application Load Balancer series. Earlier labs: an ALB with two EC2 servers (Virginia and Europe), then sticky sessions. This one covers \*\*host-based routing\*\*.



> ⚠️ \*\*Honest note:\*\* I did \*\*not\*\* do this lab hands-on. It needs a domain name (Route 53), and I don't own one yet. These are study notes based on working through the lab steps. I'll practice it for real once I have a domain.



\---



\## What it is



The ALB reads the \*\*Host header\*\* (the website name the user typed) and sends the request to a different target group:



| User visits | Goes to |

|---|---|

| `asia.example.com` | Target Group 1 (Asia) |

| `europe.example.com` | Target Group 2 (Europe) |



```

&#x20;                     Internet

&#x20;                        ↓

&#x20;             Application Load Balancer

&#x20;                        ↓

&#x20;       Check the Host header (rules by priority)

&#x20;         ↓                              ↓

asia.example.com                 europe.example.com

&#x20;         ↓                              ↓

&#x20;  Target Group: Asia            Target Group: Europe

```



\## Why my earlier setup couldn't do it



Both servers were in \*\*one\*\* target group. Listener rules forward to target groups, so you need \*\*one target group per destination\*\*.



\---



\## Steps



1\. \*\*Create 2 new target groups\*\* (Asia and Europe)

&#x20;  - HTTP, port 80, health check `/index.html`

&#x20;  - One instance in each

2\. \*\*Keep the old target group\*\* as the default rule

3\. \*\*Add listener rules\*\*



&#x20;  | Priority | Condition | Action |

&#x20;  |---|---|---|

&#x20;  | 1 | Host = `asia.<domain>` | Forward to Asia target group |

&#x20;  | 2 | Host = `europe.<domain>` | Forward to Europe target group |

&#x20;  | Default | Nothing matched | Forward to the old target group |



&#x20;  The ALB checks rules \*\*by priority\*\*. If nothing matches, the \*\*default rule\*\* runs.

4\. \*\*Route 53:\*\* create 2 \*\*alias records\*\* (`asia`, `europe`) pointing to the ALB's DNS name

5\. \*\*Test:\*\* `asia` always shows Asia and `europe` always shows Europe, with \*\*no round-robin\*\*

&#x20;  - DNS is cached, so wait a few minutes or try another network

6\. \*\*Clean up:\*\* EC2 instances, target groups, ALB, and Route 53 records



\---



\## 🧠 What I learned



\- ✅ One ALB can act like \*\*many websites\*\*

\- ✅ \*\*Host-based routing\*\* uses the Host header. \*\*Path-based routing\*\* uses the URL path (`/api`, `/images`)

\- ✅ \*\*Routing rules\*\* and \*\*DNS records\*\* are two separate jobs

\- ✅ It \*\*saves money\*\*: one ALB for many apps



\## ⏭️ Next



Practice this hands-on with a real domain, then move on to \*\*Auto Scaling\*\*.



`#AWS` `#ApplicationLoadBalancer` `#Route53` `#CloudComputing` `#LearningInPublic` `#CyberSecurity` `#BTech`

