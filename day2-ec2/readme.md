# AWS Day 2 – EC2 Virtual Server

## Goal
Launch an EC2 instance, SSH into it, install nginx, and access it via public IP.

## Commands Used

### Create key pair
aws ec2 create-key-pair --key-name amogh-ec2-key --query 'KeyMaterial' --output text > amogh-ec2-key.pem
chmod 400 amogh-ec2-key.pem

### Create security group
aws ec2 create-security-group --group-name amogh-web-sg --description "Web SG" --vpc-id <vpc-id>
aws ec2 authorize-security-group-ingress --group-id <sg-id> --protocol tcp --port 22 --cidr 0.0.0.0/0
aws ec2 authorize-security-group-ingress --group-id <sg-id> --protocol tcp --port 80 --cidr 0.0.0.0/0

### Launch instance
aws ec2 run-instances --image-id <ami-id> --instance-type t2.micro --key-name amogh-ec2-key --security-group-ids <sg-id> --count 1 --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=amogh-web-server}]'

### SSH
ssh -i ~/.ssh/amogh-ec2-key.pem ec2-user@<public-ip>

### Install nginx
sudo dnf update -y
sudo dnf install -y nginx
sudo systemctl start nginx

### Clean up
aws ec2 terminate-instances --instance-ids <instance-id>
aws ec2 delete-security-group --group-id <sg-id>
aws ec2 delete-key-pair --key-name amogh-ec2-key
