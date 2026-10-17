\# 🔐 AWS Hands-On: EC2 IAM Role + S3 Access



How an EC2 instance can securely access an S3 bucket \*\*without storing AWS access keys\*\*, using an IAM Role.



\---



\## 🎯 Goal



1\. Launch/use an EC2 instance

2\. Try accessing S3 \*\*without\*\* an IAM Role

3\. Attach an IAM Role to EC2

4\. Access S3 using the role

5\. Download an object from S3

6\. Serve that object through the EC2 web server



\---



\## What I did



\### 🧪 Step 1: Test S3 access without an IAM Role



Connected to my EC2 instance with \*\*EC2 Instance Connect\*\* and ran:



```bash

aws s3 ls s3://<bucket-name>

```



It \*\*failed\*\*, because the instance had no AWS credentials available.



Instead of configuring an IAM user's access keys, I used the recommended approach: \*\*IAM Roles\*\*.



!\[Access denied without role](screenshots/01-s3-ls-denied-no-role.jpg)



\### 🔑 Step 2: Attach an IAM Role



Went to:



```

EC2 → Instance → Actions → Security → Modify IAM role

```



Attached my previously created role: \*\*Custom EC2 Role for S3\*\*. The role has the required Amazon S3 permissions.



!\[Modify IAM role](screenshots/02-modify-iam-role.jpg)



!\[Role attached](screenshots/03-role-attached.jpg)



\### ✅ Step 3: Access S3 using the IAM Role



Ran the same command again:



```bash

aws s3 ls s3://<bucket-name>

```



This time it \*\*worked\*\* 🎯. The instance accessed the bucket without any manually configured access keys.



!\[S3 ls success](screenshots/04-s3-ls-success.jpg)



\### 📥 Step 4: Download an S3 object



Downloaded an image from the bucket:



```bash

aws s3 cp s3://<bucket-name>/myvision.png .

```



The file was copied to the EC2 instance.



!\[S3 download](screenshots/05-s3-cp-download.jpg)



\### 🌐 Step 5: Serve the image through the web server



Copied the image into the web server directory:



```bash

sudo cp myvision.png /var/www/html/

```



Then opened the EC2 website and visited the image path. The image rendered successfully, now served by the EC2 web server after being downloaded from S3.



!\[Copy to web root](screenshots/06-cp-to-web-root.jpg)



!\[Image in browser](screenshots/07-image-in-browser.jpg)



\---



\## 💡 Key takeaway



```

EC2 + IAM Role → Temporary credentials → Secure access to AWS services

```



Instead of putting long-term IAM user access keys inside the EC2 instance, I attach an \*\*IAM Role\*\* and let AWS provide \*\*temporary credentials\*\* automatically.



| Approach | Risk |

|---|---|

| ❌ Access keys stored on the instance | Keys can leak, never expire, must be rotated manually |

| ✅ IAM Role attached to the instance | Temporary credentials, rotated automatically, nothing to leak |



This is much cleaner and safer for real-world cloud environments.



`#AWS` `#IAM` `#EC2` `#S3` `#CloudSecurity` `#CyberSecurity` `#CloudComputing` `#AWSHandsOn` `#LearningAWS`

