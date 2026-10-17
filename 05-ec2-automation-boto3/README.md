\# 🚀 Automating AWS EC2 with Python (Boto3)



Hands-on lab where I created and terminated an EC2 instance using Python, instead of clicking through the AWS Management Console.



\---



\## Tools used



\- Python

\- AWS SDK for Python (\*\*Boto3\*\*)

\- AWS IAM credentials

\- AWS EC2

\- AWS CLI / SDK authentication

\- GitHub



\## Scripts in this folder



| File | What it does |

|---|---|

| `launch\_ec2.py` | Creates an EC2 instance |

| `terminate\_ec2.py` | Terminates the instance |



\---



\## What I did



\### 1️⃣ Wrote a script to launch an EC2 instance



I used Boto3 to call the AWS EC2 API from Python. Credentials are \*\*not\*\* hardcoded in the script. Boto3 reads them from the AWS credentials configuration (set up earlier with `aws configure`).



!\[launch\_ec2.py](screenshots/01-launch-ec2-script.jpg)



\### 2️⃣ Hit an error with `t2.micro`



The launch failed when I used `t2.micro`.



!\[t2.micro error](screenshots/02-t2micro-error.jpg)



\### 3️⃣ Debugged it and fixed it



1\. \*\*Error:\*\* the instance launch failed

2\. \*\*Hypothesis:\*\* I thought it was a region problem

3\. \*\*Test:\*\* I tried another region, and it still failed

4\. \*\*Investigate:\*\* I read the actual error message properly

5\. \*\*Root cause:\*\* `t2.micro` was not Free Tier eligible on my newer AWS account

6\. \*\*Fix:\*\* changed the instance type from `t2.micro` to `t3.micro` ✅

7\. \*\*Verify:\*\* the instance launched successfully



!\[t3.micro success](screenshots/03-launch-t3micro-success.jpg)



!\[Instance running in console](screenshots/04-ec2-running-console.jpg)



\### 4️⃣ Terminated the instance with a script



`terminate\_ec2.py` shuts the instance down, so I don't leave resources running and paying for them.



!\[terminate\_ec2.py](screenshots/05-terminate-ec2-script.jpg)



!\[Instance terminated in console](screenshots/06-ec2-terminated-console.jpg)



\---



\## Key lessons



\- \*\*Never hardcode access keys\*\* in scripts. Let Boto3 read them from the AWS credentials config.

\- \*\*Read the real error message\*\* before guessing. My region theory was wrong, and the message pointed to the real cause.

\- Debugging flow: \*\*Error → Hypothesis → Test → Investigate → Root cause → Fix → Verify\*\*

\- Always \*\*terminate\*\* test instances when you're done.



\---



\## Key takeaway



Cloud engineering isn't just knowing commands or services. It's also troubleshooting systematically and understanding \*why\* something fails.



`#AWS` `#EC2` `#Python` `#Boto3` `#CloudSecurity` `#DevOps` `#InfrastructureAutomation` `#LearningInPublic`

