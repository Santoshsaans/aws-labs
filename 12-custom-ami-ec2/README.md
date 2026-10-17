\# 🖼️ AWS Hands-On: Creating a Custom AMI and Launching an EC2 Instance



Learned how to create a \*\*reusable template\*\* from an existing EC2 instance, and launch a new server from it with everything already configured.



\---



\## 🎯 Goal



I already had an EC2 instance running with:



\- Linux OS

\- A web server

\- Website files

\- An image file stored on the EBS volume



Instead of configuring everything again on a new EC2 instance, I created a \*\*custom AMI\*\* from the existing instance.



!\[Original website](screenshots/01-original-ec2-website.jpg)



\---



\## What I did



\### 1️⃣ Started with an existing EC2 instance



The web server and website were already configured and running successfully.



\### 2️⃣ Created a custom AMI



```

EC2 → Instance → Actions → Image and templates → Create image

```



I enabled the \*\*reboot\*\* option, which helps maintain data consistency while the image is created.



The AMI first showed \*\*Pending\*\* and later changed to \*\*Available\*\*.



!\[Create image](screenshots/02-create-image.jpg)



!\[AMI pending](screenshots/03-ami-pending.jpg)



!\[AMI available](screenshots/04-ami-available.jpg)



!\[EBS snapshots](screenshots/05-ebs-snapshots.jpg)



\### 3️⃣ Launched a new EC2 from my custom AMI



```

Launch Instance → My AMIs → My custom AMI

```



Then configured the instance type, key pair, VPC, and a security group with HTTP access.



Importantly, I \*\*did not use User Data\*\* or manually install the web server this time.



!\[Launch from My AMIs](screenshots/06-launch-from-my-ami.jpg)



\### 4️⃣ Tested the new EC2



After the instance was ready, I opened its public IP address.



🎉 The website was \*\*already running\*\*!



I also tested the image file from the original instance, and it was available on the new EC2 as well.



!\[New EC2 website](screenshots/07-new-ec2-website.jpg)



!\[Image on new EC2](screenshots/08-image-on-new-ec2.jpg)



\---



\## 🧠 Key concept



An \*\*AMI acts like a blueprint/template\*\* for launching EC2 instances.



For an EBS-backed instance, creating an AMI creates \*\*snapshots of its EBS volumes\*\*. Those snapshots let new instances start with the captured disk data.



```

Existing EC2

&#x20;    ↓

Create Custom AMI

&#x20;    ↓

EBS Snapshots

&#x20;    ↓

Custom AMI

&#x20;    ↓

Launch New EC2

&#x20;    ↓

Same basic server setup 🚀

```



\## 🤔 Custom AMI vs User Data



| | User Data | Custom AMI |

|---|---|---|

| \*\*How it works\*\* | Script runs at first boot and installs things | Server is already fully configured before launch |

| \*\*Launch speed\*\* | Slower (installs on every launch) | Faster (everything is baked in) |

| \*\*Best for\*\* | Simple, quick setups | Many identical servers with the same software |



This is useful when we need to create \*\*multiple EC2 instances with the same software and configuration\*\* without setting everything up manually each time.



\---



\## 🧹 Cleanup



Terminated the extra instances, and deleted the AMI and its snapshot when finished, to avoid unnecessary costs.



\---



`#AWS` `#EC2` `#AMI` `#EBS` `#CloudComputing` `#CloudSecurity` `#CyberSecurity` `#AWSHandsOn` `#LearningAWS` `#100DaysOfCloud`

