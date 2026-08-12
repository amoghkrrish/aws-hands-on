# AWS Day 1 – S3 Static Website

## Goal
Create a publicly accessible static website hosted on Amazon S3 using only the AWS CLI.

## What I Learned
- Creating an AWS account and an IAM admin user (never use root).
- Installing and configuring AWS CLI on macOS.
- Creating an S3 bucket.
- Uploading files to S3.
- Enabling static website hosting.
- Writing a bucket policy that allows public read access.
- Troubleshooting DNS resolution for the S3 website endpoint.

## Commands Used

### 1. Configure AWS CLI
```bash
aws configure
aws sts get-caller-identity
