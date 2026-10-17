\# 📈 Learning AWS Auto Scaling Groups (ASG)



How EC2 Auto Scaling Groups help build \*\*scalable, highly available, and self-healing\*\* applications. Part of my AWS SAA-C03 preparation.



\---



\## 🔹 What is an Auto Scaling Group?



An ASG automatically manages the \*\*number of EC2 instances\*\* running for an application. It uses 3 values:



| Value | Meaning |

|---|---|

| \*\*Minimum\*\* | Lowest number of instances |

| \*\*Desired\*\* | Number the ASG tries to maintain |

| \*\*Maximum\*\* | Highest number allowed |



Example: `Min = 1 | Desired = 2 | Max = 4`



Minimum keeps the application running. Maximum controls costs during unexpected traffic spikes.



!\[Capacity settings](screenshots/04-asg-capacity-min-desired-max.jpg)



\---



\## 🔹 Launch Template



The ASG needs a launch template to know \*\*how\*\* to launch EC2 instances. It can define the AMI, instance type, key pair, security groups, storage, IAM role, and more.



\- \*\*Launch Template\*\* = EC2 blueprint

\- \*\*ASG\*\* = manages the number of EC2 instances



!\[Launch template](screenshots/01-asg-choose-launch-template.jpg)



!\[Network and subnets](screenshots/02-asg-network-subnets.jpg)



\---



\## 🔹 ASG + Load Balancer



ASG commonly works with an ALB or NLB.



```

Internet

&#x20;  ↓

Load Balancer

&#x20;  ↓

Target Group

&#x20;  ↓

EC2 ← ASG → EC2

```



The load balancer distributes traffic. The ASG manages EC2 capacity.



!\[Attach load balancer](screenshots/03-asg-attach-load-balancer.jpg)



!\[Instances launched](screenshots/06-asg-instances-launched.jpg)



\---



\## 🔹 Health Checks and Self-Healing



If an EC2 instance becomes unhealthy, the ASG can \*\*replace it\*\* to maintain desired capacity.



| Health check | Question it answers |

|---|---|

| \*\*EC2\*\* | Is the server running? |

| \*\*Load Balancer\*\* | Is the application actually responding? |



An EC2 instance can be running while its web application is broken. A load balancer can check an endpoint such as `/index.html` and verify the response.



A \*\*health check grace period\*\* gives a newly launched instance time to finish starting before health checks affect it.



\### Self-healing test



I terminated one instance manually, and the ASG launched a replacement.



!\[Terminate an instance](screenshots/07-self-healing-terminate-instance.jpg)



!\[Replacement instance](screenshots/08-asg-replacement-instance.jpg)



\---



\## 🔹 Scaling Policies



| # | Type | How it works |

|---|---|---|

| 1 | \*\*Manual scaling\*\* | Manually change desired capacity |

| 2 | \*\*Dynamic scaling\*\* | Scale based on CloudWatch metrics (CPU, request count, queue metrics) |

| 3 | \*\*Target tracking\*\* | Set a target like 40% average CPU, and the ASG adjusts capacity toward it |

| 4 | \*\*Scheduled scaling\*\* | Scale at predictable times, such as monthly workloads |

| 5 | \*\*Predictive scaling\*\* | Use historical usage patterns to anticipate future demand |



!\[Scaling policy](screenshots/05-asg-scaling-policy.jpg)



\---



\## 🔹 Instance Refresh



When deploying a new AMI or application version, \*\*Instance Refresh\*\* gradually replaces old instances with new ones.



```

Launch new instance

&#x20;      ↓

Check health

&#x20;      ↓

Replace old instance

&#x20;      ↓

Repeat

```



This makes updates safer.



!\[Instance refresh](screenshots/09-instance-refresh.jpg)



\---



\## 🔹 Key takeaway



| Component | Role |

|---|---|

| \*\*Launch Template\*\* | HOW to launch EC2 |

| \*\*Auto Scaling Group\*\* | HOW MANY EC2 instances |

| \*\*Load Balancer\*\* | WHERE traffic goes |

| \*\*CloudWatch\*\* | Provides metrics for scaling |

| \*\*Health Checks\*\* | Help maintain healthy capacity |



An ASG isn't simply about adding servers. It provides \*\*automatic scaling, health monitoring, instance replacement, and better availability\*\*.



`#AWS` `#AWSSAA` `#EC2` `#AutoScaling` `#CloudWatch` `#ALB` `#NLB` `#CloudComputing` `#DevOps` `#CloudSecurity` `#CyberSecurity` `#LearningInPublic`

