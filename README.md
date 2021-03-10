**Title:** EC2 Auto Scaling with Launch Templates\
**Name:** Robert Mathisen\
**Date:** 3/10/2021 \
\
\
**Process:** <br/>
\
**1) Create a Security Group for a Launch Template.** <br/>
Navigate to EC2 → Network & Security → Security Groups \
Create a Security Group which allows Inbound traffic on Port 80 (HTTP) from Custom source 0.0.0.0/0 \

**2) Create a Key Pair for the Launch Template.** <br/>
EC2 → Network & Security → Key Pairs \
Create a pem (SSH) or ppk (PuTTY) Key Pair

**3) Create the Launch Template.** <br/>
EC2 → Instances → Launch Template \
AMI: Amazon Linux 2 AMI (HVM), SSD Volume Type with Architecture: 64-bit (x86) \
Instance Type: t2.micro \
Key Pair: use the Key Pair created in Step 2 \
Networking Platform: VPC \
Networking Security Groups: use the SG created in Step 1 \
User Data: \
#!/bin/bash \
sudo su \
yum update -y \
yum install -y httpd \
systemctl start httpd \
systemctl enable httpd \
echo "`<html> <h1>` Response coming from server `</h1> </ html>`" /var/www/html/index.html

**3) Create an Auto Scaling Group** <br/>
EC2 → Auto Scaling → Auto Scaling Groups \
Launch Template: Choose the Launch Template created in Step 3 from the drop down menu. \
Network: Default VPC & select multiple Subnets
Group Size: Deired: 2, Minimum: 2, Maximum: 2
Add Tags (identify ASG instances): Key: Name, Value: EC2Instance

**4) Test your Auto Scaling Group!** <br/>
EC2 → Instances → Instances
Terminate an Instance. You will notice your ASG Instance count will drop from 2 to 1 and the Status will be "Updating capacity" once the termination is completed. Then, notice a new Instance will be launched to meet the Desired Capacity. \

If you Stop an Instance, the Instance will be Terminated, and another will be launched to meet the Desired Capacity.











