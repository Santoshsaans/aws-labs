🔐 Hands-on with AWS IAM Groups — What I Learned About Least Privilege
Today I completed a practical AWS assignment on IAM groups, and it taught me something most beginners (me included, before this) get wrong: "Full Access" doesn't mean access to everything.

Here's what I did 👇
1. Created an IAM Group Made a group called DevOps and attached 5 AWS-managed policies: CloudWatchFullAccess, AmazonSSMFullAccess, AmazonEC2FullAccess, AWSCloudFormationFullAccess, AWSLambda_FullAccess.Instead of giving permissions to users one by one, you attach them to a group — anyone added inherits them automatically.

2. Tested Access Before Adding the User Logged in as a test user and tried creating a Lambda function. Result: Access Denied ❌ — expected, since they had zero permissions yet.

3. Added the User to the Group Back as admin, added the test user to DevOps. Now they inherit all 5 policies.

4. Tried Again Tried creating the Lambda function again. Result: Still Failed ❌ — but with a more specific error this time: iam:CreateRole not authorized.

Why This Happens Creating a Lambda function with default settings also tries to auto-create a new IAM execution role behind the scenes — so the function has an identity to run under. That requires iam:CreateRole.

But AWSLambda_FullAccess only covers Lambda — not IAM. So even "full access" to one service doesn't mean access to a related one. This is Least Privilege in action — a core AWS security principle.

What's an Execution Role? It's the identity a Lambda function "wears" while running. Two separate layers: • User permissions → can you create the function? • Execution role → what can the function do once running (write logs, read S3, etc.)?

That's why creating a Lambda usually tries to create a role — and why the permission chain broke here.
Takeaway: "FullAccess" to one service ≠ access to everything it touches. Real cloud security is about understanding these hidden dependencies.
#AWS #CloudSecurity #IAM #CyberSecurity #LearningInPublic
