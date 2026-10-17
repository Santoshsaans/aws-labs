\# ☁️ Hands-on with AWS EC2: Launch and Connect



My first real cloud deployment: launching an EC2 instance and connecting to it in two different ways.



\---



\## What I did



\### 1️⃣ Launched an EC2 instance



Spun up a virtual server on AWS from scratch. I chose:



\- the \*\*AMI\*\* (Amazon Machine Image)

\- the \*\*instance type\*\*

\- the basic settings



!\[Launch instance settings](screenshots/01-launch-instance-settings.jpg)



\### 2️⃣ Created an SSH key pair



Generated a key pair (public + private key) during launch. AWS keeps the public key on the instance, and I download the private key as a `.pem` file. This key lets me log in securely without a password.



!\[Create key pair](screenshots/02-create-key-pair.jpg)



!\[Instance running](screenshots/03-instance-running.jpg)



\### 3️⃣ Connected via SSH



Used the private key (`.pem` file) from my terminal to SSH into the instance. This is the standard way engineers access remote servers.



```bash

ssh -i "my-key.pem" ec2-user@<public-ip>

```



!\[SSH connected](screenshots/04-ssh-connected-terminal.jpg)



\### 4️⃣ Connected via the AWS Console (EC2 Instance Connect)



Logged in straight from the browser using AWS's built-in connection. No terminal or key file needed on my side.



!\[EC2 Instance Connect](screenshots/05-ec2-instance-connect.jpg)



\---



\## What I learned



| Lesson | Why it matters |

|---|---|

| 🔑 \*\*SSH keys > passwords\*\* | Public-key authentication is far more secure, because the private key never leaves your machine |

| 🌐 \*\*Multiple ways to access the same server\*\* | Terminal SSH gives more control and is closer to real-world usage. The browser console is great for quick access or troubleshooting |

| ☁️ \*\*Instances are just virtual computers\*\* | Once connected, an EC2 instance behaves like a remote Linux machine you can configure and install software on |

| 🛡️ \*\*Security basics from day one\*\* | Key management, security groups, and access control are the foundation in the cloud, not afterthoughts |



\---



\## ⚠️ Security notes



\- Never share or upload your `.pem` private key file

\- Keep the key private on your own machine (and don't commit it to GitHub)

\- Terminate instances you're not using



\---



\## Key takeaway



A small step, but a solid one in my journey from AWS Cloud Practitioner → Solutions Architect → Cloud Security.



`#AWS` `#CloudComputing` `#EC2` `#CyberSecurity` `#LearningInPublic` `#CloudSecurity` `#Networking`

