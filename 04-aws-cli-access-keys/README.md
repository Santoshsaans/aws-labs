\# ☁️ AWS CLI: Accessing AWS from the Command Line



Hands-on lab on using the AWS CLI instead of the Management Console, and on why access keys must be protected.



\---



\## 3 ways to interact with AWS



| Method | How you use it |

|---|---|

| \*\*AWS Management Console\*\* | Web interface. Click buttons 🖱️ |

| \*\*AWS CLI\*\* | Command line. Run commands ⌨️ |

| \*\*AWS SDK\*\* | Access AWS from your code 👨‍💻 |



All three talk to AWS, but the way you interact is different.



\---



\## What I did



\### 1️⃣ Created an access key for my IAM user



\- Went to IAM → Users → Security credentials → Create access key

\- Access keys are credentials tied to an IAM user, used for programmatic access (CLI or SDK)

\- An IAM user can have a maximum of \*\*two\*\* active access keys at a time



!\[Create access key](screenshots/01-create-access-key.jpg)



\### 2️⃣ Installed the AWS CLI



\- Installed the CLI for my operating system (Windows)

\- Verified the install with `aws --version`



!\[AWS CLI version](screenshots/02-aws-version.jpg)



\### 3️⃣ Configured the CLI



```bash

aws configure

```



It asks for four things:



\- 🔑 Access Key ID

\- 🔐 Secret Access Key

\- 🌎 Default Region (I used `ap-south-1`, Mumbai)

\- 📄 Output Format (I used `json`, because it is structured and easy for programs to process)



!\[aws configure](screenshots/03-aws-configure.jpg)



\### 4️⃣ Ran my first command



```bash

aws s3 ls

```



This lists the S3 buckets in my AWS account, straight from the terminal.



!\[aws s3 ls](screenshots/04-aws-s3-ls.jpg)



\### 5️⃣ Overrode the default region



The default region is used when a command doesn't specify one. You can override it with `--region`:



```bash

aws s3 ls --region us-east-1

```



!\[Region override](screenshots/05-region-override.jpg)



\### 6️⃣ Deleted the access key



After the lab I deactivated and deleted the key, so it can't be misused.



!\[Delete access key](screenshots/06-delete-access-key.jpg)



\---



\## ⚠️ Security lessons



\- \*\*Never share\*\* your Access Key ID and Secret Access Key

\- Anyone with valid credentials and enough permissions can access your AWS resources

\- The secret access key is shown \*\*only once\*\*. If you lose it, you can't get it back: create a new key and deactivate/delete the old one

\- Never commit keys to GitHub or paste them in screenshots

\- Delete keys you no longer use



\---



\## Key takeaway



Console = click buttons. CLI = run commands. SDK = use code. Understanding access keys and how to protect them is a core part of AWS IAM and cloud security.



`#AWS` `#AWSCLI` `#IAM` `#CloudSecurity` `#CyberSecurity` `#LearningInPublic` `#SolutionsArchitect`

