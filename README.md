# AWS High Availability & Disaster Recovery Architecture

## Project Overview

This project demonstrates a highly available, scalable, and disaster recovery architecture on AWS using core networking, compute, database, and backup services.

The infrastructure is designed to provide:

- High Availability across multiple Availability Zones
- Automatic Load Distribution
- Auto Scaling for EC2 Instances
- Database High Availability using Amazon RDS Multi-AZ
- Automated Disaster Recovery using AWS Backup
- Improved Fault Tolerance and Business Continuity

---

# Architecture Components

- Amazon VPC
- Internet Gateway
- NAT Gateway
- Public Subnets (2 Availability Zones)
- Private DB Subnets (2 Availability Zones)
- Route Tables
- Security Groups
- Amazon EC2
- Application Load Balancer (ALB)
- Auto Scaling Group (ASG)
- Amazon RDS (Multi-AZ)
- DB Subnet Group
- AWS Backup
- Backup Vault
- CloudWatch Monitoring

---

# Architecture Diagram

![Architecture](screenshot/aws-ha-architecture.png)

---

# Workflow

1. User sends a request to the Application Load Balancer.
2. ALB distributes traffic to EC2 instances.
3. EC2 communicates with Amazon RDS inside private DB subnets.
4. Amazon RDS replicates data automatically to the standby instance in another Availability Zone.
5. AWS Backup creates scheduled recovery points.
6. If the primary database fails, RDS performs automatic failover.
7. If data is accidentally deleted or corrupted, it can be restored using AWS Backup.

---

# Implementation Steps

## Step 1 - Create VPC

- Created a VPC with CIDR block `10.0.0.0/16`

---

## Step 2 - Create Networking

Created:

- 2 Public Subnets
- 2 Private DB Subnets
- Internet Gateway
- NAT Gateway
- Public Route Table
- Private Route Table

---

## Step 3 - Deploy EC2

Created an Ubuntu EC2 instance.

Installed Apache using User Data:

```bash
#!/bin/bash
apt update -y
apt install apache2 -y
systemctl start apache2
systemctl enable apache2
echo "Hello from AWS High Availability Project" > /var/www/html/index.html
```

---

## Step 4 - Configure Load Balancer

- Created Application Load Balancer
- Created Target Group
- Registered EC2
- Configured Health Check

---

## Step 5 - Configure Auto Scaling

Created Launch Template

Configured Auto Scaling Group

- Minimum Capacity = 2
- Desired Capacity = 2
- Maximum Capacity = 4

Configured Target Tracking Policy

- CPU Utilization = 50%

---

## Step 6 - Configure Amazon RDS

Created Amazon RDS Database

- MySQL Engine
- Multi-AZ Deployment
- DB Subnet Group
- Private Subnets
- Automated Backups Enabled

---

## Step 7 - Configure AWS Backup

Created

- Backup Plan
- Backup Rule
- Backup Assignment
- Backup Vault

The backup plan automatically creates recovery points for disaster recovery.

---

# Results

- High Availability achieved across multiple Availability Zones.
- Automatic traffic distribution using ALB.
- Automatic EC2 scaling using Auto Scaling Group.
- Database redundancy using Amazon RDS Multi-AZ.
- Automated backup and recovery using AWS Backup.
- Improved Disaster Recovery capability.

---

# Screenshots

## VPC

![VPC](screenshot/vpc.png)

---

## Application Load Balancer

![ALB](screenshot/ALB.png)

---

## Auto Scaling Group

![ASG](screenshot/ASG-activity.png)

---

## EC2 Health Check

![Health Check](screenshot/instance-health-check.png)

---

## CloudWatch Monitoring

![Monitoring](screenshot/monitoring.png)

---

## Amazon RDS

![RDS](screenshot/rds-overview.png)

---

## AWS Backup Plan

![Backup Plan](screenshot/backup-plan.png)

---

## Estimated Cost

![Estimated Cost](screenshot/estimated-cost.png)

---

# Key Learnings

- Amazon VPC
- Public and Private Subnets
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- EC2 Deployment
- Application Load Balancer
- Auto Scaling Group
- Amazon RDS Multi-AZ
- DB Subnet Group
- AWS Backup
- Disaster Recovery Strategy
- CloudWatch Monitoring

---

# Conclusion

This project demonstrates how to design a production-ready AWS architecture that combines High Availability and Disaster Recovery. The infrastructure ensures continuous application availability, automatic scaling, database redundancy, and automated backup for reliable recovery during failures.

---

# Author

**Sapna Kumari**
