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
Create a Launch Template using an AMI. For this project, I'll be using 'Amazon Linux 2 AMI (HVM), SSD Volume Type with Architecture: 64-bit (x86)' \
