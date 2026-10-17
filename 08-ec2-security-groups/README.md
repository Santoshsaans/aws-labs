\# 🛡️ AWS EC2 Security Groups: My Key Learning



Hands-on lab exploring Security Groups, which act as a \*\*virtual firewall\*\* for EC2 instances.



\---



\## Inbound vs Outbound traffic



| Direction | Meaning | Example |

|---|---|---|

| 📥 \*\*Inbound\*\* | Traffic coming \*\*into\*\* the EC2 instance | SSH on port 22, HTTP on port 80 |

| 📤 \*\*Outbound\*\* | Traffic the instance \*\*initiates\*\* toward another service or the internet | Downloading updates |



!\[Security groups list](screenshots/01-security-groups-list.jpg)



!\[Inbound rules](screenshots/02-inbound-rules.jpg)



!\[Outbound rules](screenshots/03-outbound-rules.jpg)



\---



\## 🔄 Security Groups are stateful



If an inbound request is allowed, its \*\*return traffic is automatically allowed\*\*. I don't need a separate rule for the response.



\---



\## Key features



\- ✅ \*\*Allow rules only\*\*: there are no explicit deny rules

\- Control traffic using \*\*protocols, ports and IP ranges\*\*

\- Support \*\*IPv4 and IPv6\*\*

\- \*\*Changes apply automatically\*\*

\- One security group can be used by \*\*multiple EC2 instances\*\*

\- \*\*Multiple security groups\*\* can be attached to one EC2 instance



!\[Multiple security groups on an instance](screenshots/06-multiple-sgs-on-instance.jpg)



\---



\## 📡 ICMP and ping



Ping uses \*\*ICMP\*\*, not TCP or UDP. To ping an EC2 instance, the required ICMP traffic must be allowed in the security group.



I added an inbound rule for ICMP:



!\[Add ICMP rule](screenshots/04-add-icmp-rule.jpg)



Then tested with ping:



```bash

ping <public-ip>

```



!\[Ping test](screenshots/05-ping-test.jpg)



\---



\## 🌐 Common ports



| Service | Port |

|---|---|

| SSH | 22 |

| FTP | 21 |

| HTTP | 80 |

| HTTPS | 443 |

| RDP | 3389 |



\---



\## 📌 Security Group vs NACL



| | Security Group | NACL |

|---|---|---|

| \*\*Level\*\* | Instance level | Subnet level |

| \*\*State\*\* | Stateful | Stateless |

| \*\*Rules\*\* | Allow only | Allow + Deny |



\---



\## 📚 Summary



A security group controls \*\*who can communicate with an EC2 instance\*\* and \*\*what traffic is allowed\*\*. Understanding inbound/outbound traffic, stateful connections, ports and ICMP is essential for AWS networking and cloud security.



\## 💡 Key takeaway



Security groups are one of the first and most important security controls when securing EC2 instances.



`#AWS` `#EC2` `#CloudSecurity` `#CyberSecurity` `#AWSLearning` `#Networking` `#SecurityGroup` `#NACL` `#CloudComputing`

