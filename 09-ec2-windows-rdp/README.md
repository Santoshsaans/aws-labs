\# 🖥️ Hands-on with AWS EC2: Windows Server and RDP



Launched my first Windows Server instance on AWS, and controlled it remotely. This lab also taught me the difference between \*\*RDP\*\* and \*\*SSH\*\*.



\---



\## What I did, step by step



\### 1️⃣ Opened the EC2 Dashboard



Went to the Mumbai (`ap-south-1`) region and clicked \*\*Launch instances\*\*.



\### 2️⃣ Named the instance and chose a Windows AMI



Selected the \*\*Windows Server 2022 Base\*\* AMI instead of the usual Linux image.



!\[Windows AMI](screenshots/01-launch-windows-ami.jpg)



\### 3️⃣ Chose the instance type and key pair



\- Instance type: free-tier eligible `t2.micro`

\- Selected my key pair (`.pem` file). This key is what unlocks the admin password later.



!\[Instance type and key pair](screenshots/02-instance-type-keypair.jpg)



\### 4️⃣ Configured the security group



Allowed \*\*RDP on port 3389\*\*, restricted to \*\*My IP\*\* only.



This is critical: exposing RDP to the whole internet (`0.0.0.0/0`) is a common attack vector.



!\[Security group RDP](screenshots/03-security-group-rdp-my-ip.jpg)



\### 5️⃣ Launched the instance



Left storage at the default 8 GiB and clicked \*\*Launch instance\*\*.



!\[Instance running](screenshots/04-instance-running.jpg)



\### 6️⃣ Got the Windows password



Once running: \*\*Actions → Security → Get Windows Password\*\*, uploaded my `.pem` key, and let AWS decrypt the Administrator password.



!\[Get Windows password](screenshots/05-get-windows-password.jpg)



\### 7️⃣ Connected with Remote Desktop



Opened \*\*Remote Desktop Connection\*\* on my laptop, entered the instance's public IPv4 address, and logged in with:



\- Username: `Administrator`

\- Password: the decrypted one



!\[RDP connection](screenshots/06-rdp-connection.jpg)



\### 8️⃣ Got a full Windows Server desktop 🎉



A full Windows Server desktop, running in an AWS data center, controlled remotely from my machine.



!\[Windows desktop](screenshots/07-windows-desktop.jpg)



\### 9️⃣ Terminated the instance



Terminated it afterward to avoid unnecessary running costs.



!\[Instance terminated](screenshots/08-instance-terminated.jpg)



\---



\## 🔑 RDP vs SSH



| | RDP (Windows) | SSH (Linux) |

|---|---|---|

| \*\*Full form\*\* | Remote Desktop Protocol | Secure Shell |

| \*\*Interface\*\* | Full graphical desktop (GUI) | Command line only (terminal) |

| \*\*Default port\*\* | 3389 | 22 |

| \*\*Authentication\*\* | Username + password (decrypted using your key pair) | Private key (`.pem`) directly, no password needed |

| \*\*Use case\*\* | Managing Windows servers visually | Managing Linux servers via commands |

| \*\*Bandwidth\*\* | Heavier (streams the whole desktop) | Lightweight (just text) |



\*\*Biggest mindset shift:\*\* SSH logs you into a Linux server's terminal using your key pair directly. RDP gives you the entire Windows desktop, but the password has to be decrypted using that same key pair first, because AWS never sends the raw password.



\---



\## ⚠️ Security notes



\- Restrict RDP (port 3389) to \*\*My IP\*\*, never `0.0.0.0/0`

\- Never share your `.pem` key or the decrypted password

\- Terminate instances you're not using



\---



\## Key takeaway



A small exercise, but it made cloud infrastructure feel a lot less abstract.



`#AWS` `#CloudComputing` `#EC2` `#Windows` `#RDP` `#SSH` `#CyberSecurity` `#LearningInPublic` `#TechStudent`

