\# 🌐 Understanding VPC CIDR and Building My First Custom VPC



Went deeper into AWS networking fundamentals: \*\*CIDR\*\* (Classless Inter-Domain Routing) and how it powers \*\*Amazon VPC\*\* (Virtual Private Cloud).



\---



\## 📌 What is CIDR?



CIDR is a modern way to represent IP address ranges, replacing the older Class A/B/C addressing system. It's written as:



```

Base Address / Prefix Length

```



Example: `10.10.0.0/16`



The prefix tells you how many bits are reserved for the \*\*network\*\* and how many are available for \*\*hosts\*\*.



```

Total addresses = 2^(32 − prefix length)    (IPv4)

```



| CIDR | Calculation | Total IPs |

|---|---|---|

| `/16` | 2^16 | 65,536 |

| `/24` | 2^8 | 256 |



The \*\*higher\*\* the prefix number, the \*\*smaller\*\* the network.



\---



\## 📌 CIDR rules in AWS



\- AWS supports VPC prefixes from \*\*/16 to /28\*\*

\- CIDR ranges should follow \*\*RFC 1918\*\* private addressing:



&#x20; | Range | Block |

&#x20; |---|---|

&#x20; | `10.0.0.0/8` | Class A private range |

&#x20; | `172.16.0.0/12` | Class B private range |

&#x20; | `192.168.0.0/16` | Class C private range |



\- \*\*IPv6\*\* uses a fixed \*\*/56\*\* prefix, and the range is \*\*auto-allocated by AWS\*\*. You don't choose it

\- Unlike private IPv4 addresses, \*\*IPv6 addresses are globally unique and public\*\*



\---



\## 🛠️ Hands-on: Creating my first custom VPC



Instead of relying on AWS's \*\*default VPC\*\* (auto-created in every region), I built one from scratch.



\### 1️⃣ Opened the VPC service



!\[VPC dashboard](screenshots/01-vpc-service-dashboard.jpg)



\### 2️⃣ Selected "VPC only" creation mode



!\[VPC only](screenshots/02-create-vpc-only.jpg)



\### 3️⃣ Named it and assigned the CIDR block



| Setting | Value |

|---|---|

| Name | `Demo VPC` |

| IPv4 CIDR | `10.10.0.0/16` |



!\[Name and CIDR](screenshots/03-vpc-name-and-cidr.jpg)



\### 4️⃣ Skipped IPv6 and set tenancy



| Setting | Value |

|---|---|

| IPv6 | Skipped (optional) |

| Tenancy | \*\*Default\*\* (shared hardware) |



Default tenancy is the standard, cost-efficient choice, unless you need dedicated hardware for compliance or licensing reasons.



!\[IPv6 and tenancy](screenshots/04-ipv6-and-tenancy.jpg)



\### 5️⃣ Created the VPC



!\[VPC created](screenshots/05-vpc-created.jpg)



!\[VPC details](screenshots/06-vpc-details.jpg)



!\[VPC list](screenshots/07-vpc-list.jpg)



\---



\## ⏭️ What's next



This VPC is the foundation for the next exercises: \*\*subnets, route tables, internet gateways\*\*, and more.



\## 💡 Key takeaway



Understanding CIDR isn't just theory. It directly impacts how you design \*\*scalable, secure network architecture\*\* in the cloud. Getting it right at the VPC level saves major headaches later.



`#AWS` `#CloudComputing` `#Networking` `#VPC` `#CIDR` `#AWSCertified` `#CloudSecurity` `#LearningInPublic` `#SolutionsArchitect`

