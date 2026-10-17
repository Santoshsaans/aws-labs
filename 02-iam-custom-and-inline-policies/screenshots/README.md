# 🔐 IAM Deep Dive: One User, Two Policy Types, Zero Guesswork

Hands-on lab on controlling exactly what a user can and can't touch, using two different policy types on the same identity.

---

## What I did

### 1️⃣ Created a Customer Managed Policy called `custom-s3`

- Used the Visual Policy Editor to allow all S3 actions (`s3:*`) on all resources
- Reviewed the auto-generated JSON to understand exactly what the policy grants
- Saved it as a standalone, reusable policy in IAM

### 2️⃣ Attached the policy to my IAM user

- Went to Policies → selected `custom-s3` → attached it directly to the user
- Confirmed under the user's Permissions tab that it shows up as "Directly attached"

### 3️⃣ Added an Inline Policy scoped to EC2 read-only

- Allowed only `ec2:Describe*` actions
- The user can view EC2 instances but cannot launch, stop, or modify anything

### 4️⃣ Tested it from the user's own session

- ✅ S3 actions worked (could create/view buckets)
- ❌ EC2 write actions were correctly denied, proving the read-only restriction works

---

## Customer Managed vs Inline Policy

| | Customer Managed Policy | Inline Policy |
|---|---|---|
| **Where it lives** | Standalone object in IAM | Embedded inside one user/group/role |
| **Reusable?** | Yes, attach to many users, groups, or roles | No, tied to one identity |
| **Management** | Easy to track, version, and manage centrally | Managed only through its identity |
| **If identity is deleted** | Policy stays | Policy is deleted with it |
| **Best for** | Permissions you'll reuse | One-off, tightly scoped permissions |

**Key takeaway:** Customer managed policies = reusable building blocks. Inline policies = permissions glued permanently to one specific identity.

---

Learning IAM one hands-on lab at a time. The more I break things (safely, in a test account 😅), the more it clicks.

`#AWS` `#IAM` `#CloudSecurity` `#CyberSecurity` `#LearningInPublic` `#BugBounty`
