\# 🚀 AWS: EC2 Launch Templates



Created EC2 launch templates hands-on in the AWS Console, and learned why they matter.



\---



\## 😩 The problem



Every time you launch an EC2 instance, you have to pick the AMI, instance type, key pair, security group, storage and user data again. For 5 or 10 servers that gets slow and boring, and it's easy to make mistakes.



\## ✅ The solution: Launch Templates



Save all those settings \*\*once\*\* and reuse them whenever you want.



| Benefit | What it means |

|---|---|

| \*\*Consistency\*\* | Every server launches with the same configuration |

| \*\*Saves time\*\* | No repeating the same steps again and again |

| \*\*Fewer mistakes\*\* | No wrong AMI or forgotten security group |

| \*\*Versioning\*\* | Update the template and keep older versions |

| \*\*Works with Auto Scaling\*\* | Auto Scaling Groups use launch templates to create new instances automatically |



\## Files in this folder



| File | What it is |

|---|---|

| `user-data-virginia.sh` | User Data for Template 1 |

| `user-data-europe.sh` | User Data for Template 2 |

| `screenshots/` | Screenshots of each step |



\---



\## 🛠️ What I built



I made \*\*2 launch templates\*\* for web servers. Each had a different User Data script that installs Apache (`httpd`) and shows its own page:



| Template | Page shown |

|---|---|

| 🇺🇸 Template 1 | "You have reached a website for Virginia" |

| 🌍 Template 2 | "You have reached a website for Europe" |



I also used a \*\*different Availability Zone (subnet)\*\* for each one, and a \*\*reusable security group\*\* that allows HTTP (port 80).



!\[Create launch template](screenshots/01-create-launch-template.jpg)



\### Template 1: Virginia



!\[Template 1 settings](screenshots/02-template1-settings.jpg)



!\[Template 1 user data](screenshots/03-template1-user-data.jpg)



\### Template 2: Europe



!\[Template 2 user data](screenshots/04-template2-user-data.jpg)



\### Both templates



!\[Launch templates list](screenshots/05-launch-templates-list.jpg)



\### Launching from a template



!\[Launch from template](screenshots/06-launch-from-template.jpg)



\### Results



!\[Virginia website](screenshots/07-virginia-website.jpg)



!\[Europe website](screenshots/08-europe-website.jpg)



\---



\## 🧠 Key takeaway



Launching servers by hand doesn't scale. Launch templates are the \*\*first step toward automation and high availability\*\* in the cloud.



\## ⏭️ Next



Connect these templates to a \*\*load balancer\*\* and \*\*Auto Scaling\*\*.



`#AWS` `#EC2` `#CloudComputing` `#LaunchTemplates` `#DevOps` `#CyberSecurity` `#LearningInPublic`

