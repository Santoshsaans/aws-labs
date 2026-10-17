\# 🏗️ AWS VPC Deep Dive: Building a Public \& Private Subnet Architecture



Hands-on with core AWS networking components: \*\*Internet Gateway, Subnets, and Route Tables\*\*. I built a proper public/private subnet setup inside my `Demo VPC`.



\---



\## 📌 The core concepts



\### 1. Subnets



A VPC is one large address range. Subnets divide it into \*\*smaller networks\*\*, and each subnet lives inside a \*\*single Availability Zone\*\*.



Best practice: the VPC gets a `/16` CIDR and subnets get `/24` (256 addresses each), though this is flexible.



\### 2. Local router and route tables



Every VPC has a built-in \*\*local router\*\* that moves traffic between subnets inside the VPC. Something still has to tell traffic where to go. That's the job of the \*\*route table\*\*.



Every VPC starts with a \*\*Main route table\*\* (default). Every subnet follows it unless you attach a custom one.



\### 3. Internet Gateway (IGW)



By default, a VPC has \*\*zero internet connectivity\*\*. Attaching an Internet Gateway makes internet access possible, but it doesn't automatically give every subnet access.



\### 4. Public vs private subnet: decided entirely by the route table



| Subnet type | Route table |

|---|---|

| \*\*Public\*\* | Has an entry `0.0.0.0/0 → Internet Gateway` |

| \*\*Private\*\* | No such entry, so there's no path out |



\---



\## 🛠️ What I built, step by step



\### 1️⃣ Created an Internet Gateway and attached it to the VPC



`demo-igw`, attached to my existing `Demo VPC`.



!\[Create IGW](screenshots/01-create-igw.jpg)



!\[Attach IGW](screenshots/02-attach-igw-to-vpc.jpg)



\### 2️⃣ Created two subnets in different Availability Zones



| Subnet | AZ | CIDR |

|---|---|---|

| `demo-public-subnet` | `ap-south-1a` | `10.10.0.0/24` |

| `demo-private-subnet` | another AZ | `10.10.1.0/24` |



!\[Public subnet](screenshots/03-create-public-subnet.jpg)



!\[Private subnet](screenshots/04-create-private-subnet.jpg)



\### 3️⃣ Created a custom route table for the public subnet



`demo-public`:



\- Added a route: `0.0.0.0/0 → Internet Gateway`

\- Associated it with `demo-public-subnet` (subnet associations)



!\[Public route](screenshots/05-public-route-table-igw-route.jpg)



!\[Public association](screenshots/06-public-subnet-association.jpg)



\### 4️⃣ Created a separate route table for the private subnet



`demo-private`:



\- Left with only the default \*\*local\*\* route (no internet route)

\- Associated it with `demo-private-subnet`



!\[Private route table](screenshots/07-private-route-table-local-only.jpg)



!\[Private association](screenshots/08-private-subnet-association.jpg)



\### 5️⃣ Verified the setup



I checked each subnet's associated route table:



| Subnet | Routes |

|---|---|

| Public | \*\*2 routes\*\* (local + internet) |

| Private | \*\*1 route\*\* (local only) |



!\[Public subnet routes](screenshots/09-verify-public-subnet-routes.jpg)



!\[Private subnet routes](screenshots/10-verify-private-subnet-routes.jpg)



\---



\## 🗺️ Architecture



```

&#x20;                   Internet

&#x20;                      ↓

&#x20;             Internet Gateway (demo-igw)

&#x20;                      ↓

┌──────────────── Demo VPC 10.10.0.0/16 ────────────────┐

│                                                        │

│  Public subnet 10.10.0.0/24     Private subnet 10.10.1.0/24

│  (route: 0.0.0.0/0 → IGW)       (route: local only)    │

└────────────────────────────────────────────────────────┘

```



\---



\## 💡 Key takeaway



Both subnets started \*\*identical in structure\*\*. The only thing that made one "public" and one "private" was \*\*which route table was attached to it\*\*.



This is exactly the kind of subtle configuration detail that matters in real-world cloud security: \*\*a misattached route table can accidentally expose a database subnet to the internet.\*\*



`#AWS` `#CloudComputing` `#VPC` `#Networking` `#AWSCertified` `#CloudSecurity` `#SolutionsArchitect` `#LearningInPublic`

