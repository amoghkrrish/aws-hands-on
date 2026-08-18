# AWS Day 5 – RDS (Managed MySQL Database)

## Goal
Launch a free-tier MySQL RDS instance in the default VPC, launch an EC2 instance in the same VPC, and connect from EC2 to RDS using a security group that allows MySQL only from the EC2 security group. This demonstrates the classic 3‑tier architecture: Web Server (EC2) → Database (RDS).

## What I Learned
- RDS is a managed database service – AWS handles backups, updates, and high availability.
- Creating a security group for RDS that allows inbound MySQL (port 3306) **only from the EC2 security group** (source security group referencing).
- Creating a security group for EC2 that allows SSH (port 22) and HTTP (port 80).
- Launching a free-tier `db.t3.micro` MySQL RDS instance with `--no-publicly-accessible` (private).
- Launching an EC2 instance in the same VPC and same availability zone.
- Connecting to the RDS endpoint from EC2 using the MySQL client (`mariadb105` package on Amazon Linux 2023).
- Creating a database, table, and inserting/querying data.
- Cleaning up RDS, EC2, security groups, and key pair.

## Architecture

