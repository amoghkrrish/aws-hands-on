# AWS Day 3 – IAM Role & S3 Access from EC2

## Goal
Allow an EC2 instance to access S3 **without storing access keys**. Use an IAM Role attached to the instance, which provides temporary credentials automatically.

## What I Learned
- Creating an IAM role with a trust policy for EC2.
- Attaching a managed policy (`AmazonS3ReadOnlyAccess`) to the role.
- Launching an EC2 instance with `--iam-instance-profile` to attach the role.
- On the instance, AWS CLI automatically uses the role credentials – no `aws configure` needed.
- Testing least privilege: read works, write is denied.
- Cleaning up all resources to avoid charges.

## Commands Used

### 1. Create IAM Role
```bash
cat > trust-policy.json << 'EOF'
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
EOF

aws iam create-role \
    --role-name EC2-S3-Read-Only \
    --assume-role-policy-document file://trust-policy.json

aws iam attach-role-policy \
    --role-name EC2-S3-Read-Only \
    --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
