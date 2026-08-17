# AWS Day 4 – VPC Networking (Public & Private Subnets)

## Goal
Build a custom VPC with public and private subnets, an Internet Gateway, route tables, and launch an EC2 instance in the public subnet. Verify the full request flow: Internet → IGW → Route Table → Public Subnet → EC2.

## What I Learned
- Creating a VPC with a CIDR block (`10.0.0.0/16`).
- Attaching an Internet Gateway to allow internet access.
- Creating subnets in different Availability Zones.
- Configuring a route table for the public subnet (`0.0.0.0/0 → IGW`).
- Associating the route table with the subnet.
- Launching an EC2 instance in the public subnet with `--associate-public-ip-address`.
- The instance could reach the internet (`curl checkip.amazonaws.com`).
- Cleaning up all resources in the correct order.

## Architecture

