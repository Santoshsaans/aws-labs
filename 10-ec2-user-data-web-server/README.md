\# 🌐 AWS EC2 Assignment: Deploying a Web Server Using EC2 User Data



Deployed a simple web server using \*\*EC2 User Data\*\* instead of configuring the server by hand.



\---



\## 🎯 Goal



1\. Launch an EC2 instance

2\. Automatically install an HTTP server

3\. Start the service

4\. Access the website through the EC2 public IP







| File | What it is |

|---|---|

| `user-data.sh` | The startup script passed to EC2 as User Data |

| `screenshots/` | Screenshots of each step |



\---



\## What I did



\### 🔹 Step 1: Launch EC2



| Setting | Value |

|---|---|

| AMI | Amazon Linux 2023 |

| Instance type | `t3.micro` |

| VPC | Default VPC |

| Public IP | Enabled |



The AMI provides the base operating system for the instance.



!\[Launch settings](screenshots/01-launch-ec2-settings.jpg)



\### 🔹 Step 2: Configure the Security Group



Since the website uses HTTP, I allowed:



| Type | Protocol | Port | Source |

|---|---|---|---|

| HTTP | TCP | 80 | `0.0.0.0/0` |

| SSH | TCP | 22 | kept for troubleshooting |



\*\*Lesson:\*\* installing a web server is not enough. The security group must also allow the required network traffic.



!\[Security group](screenshots/02-security-group-http-80.jpg)



\### 🔹 Step 3: Configure User Data



Under \*\*Advanced details → User data\*\*, I pasted a startup script (see `user-data.sh`).



```

Launch EC2

&#x20;   ↓

User Data executes

&#x20;   ↓

Install HTTP server

&#x20;   ↓

Start HTTP service

&#x20;   ↓

Website becomes available

```



No need to SSH into the server and install everything manually.



!\[User data script](screenshots/03-user-data-script.jpg)



\### 🔹 Step 4: Test the website



Once the instance was running, I copied the \*\*Public IPv4 address\*\* and opened:



```

http://<public-ip>

```



The website loaded successfully 🎉



HTTP uses port \*\*80\*\* and HTTPS uses port \*\*443\*\*, so I had to use `http://` explicitly.



!\[Instance running](screenshots/04-instance-running.jpg)



!\[Website loaded](screenshots/05-website-loaded.jpg)



\---



\## 🤔 Why User Data instead of configuring manually?



| Approach | Steps |

|---|---|

| \*\*Manual\*\* | Launch EC2 → SSH → Install software → Configure → Start service |

| \*\*User Data\*\* | Launch EC2 → Script runs automatically → Server ready |



User Data is useful when you want to \*\*automate the initial configuration\*\* of an EC2 instance.



\## 🤔 Why not a Custom AMI?



A Custom AMI makes sense when you've already configured a server and want to launch many instances with the \*\*same preconfigured environment\*\*. For this assignment I only needed a simple automated setup, so User Data was the better fit.



\---



\## 🧠 Key takeaway



| Component | Role |

|---|---|

| \*\*AMI\*\* | Provides the base OS/template |

| \*\*EC2\*\* | Provides the virtual server |

| \*\*User Data\*\* | Automates the initial setup |

| \*\*Security Group\*\* | Controls network traffic |

| \*\*Port 80\*\* | HTTP |

| \*\*Public IP\*\* | Allows internet access |



The complete flow:



```

AMI → EC2 → User Data → HTTP Server → Security Group → Public IP → 🌐 Website

```



This exercise helped me understand how EC2, AMIs, User Data, networking, and security groups work together in AWS.



`#AWS` `#EC2` `#CloudComputing` `#CloudSecurity` `#DevOps` `#AWSLearning` `#SAA`

