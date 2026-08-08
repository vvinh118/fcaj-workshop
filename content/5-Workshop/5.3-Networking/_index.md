---
title: "Network Infrastructure (VPC)"
date: 2026-08-07
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Objective
Establish an isolated Virtual Private Cloud (VPC) that clearly separates public zones (**Public Subnets**) for the Load Balancer handling internet traffic from private zones (**Private Subnets**) designed to securely protect application containers and databases.

#### 1. Creating the Amazon VPC
1. Access the AWS Management Console, search for and select the **VPC** service.
2. Navigate to the **VPC Dashboard** -> Click **Create VPC**.
3. Choose the **VPC and more** configuration option.
4. Configure the parameters as follows:
   * **Name tag auto-generation:** `cloud-finance-vpc`
   * **IPv4 CIDR block:** `10.0.0.0/16`
   * **Tenancy:** `Default`
   * **Number of Availability Zones (AZs):** `2` (select regions like `ap-southeast-1a` and `ap-southeast-1b`)
   * **Number of public subnets:** `2`
   * **Number of private subnets:** `4` (allocated into 2 for ECS applications and 2 for databases)
   * **NAT gateways:** Select `1 NAT gateway` (configured as Single AZ to optimize demo costs)
   * **VPC endpoints:** None required
5. Click **Create VPC** and wait for the system to automatically provision the network infrastructure.

![VPC Setup](vpc-created.png)

#### 2. Configuring Security Groups (Firewalls)
We need to set up 4 distinct Security Groups to strictly control traffic flow across tiers:
+ `alb-sg` (Load Balancer Security Group): Allows inbound traffic on ports `80` (HTTP) and `443` (HTTPS) from any source (`0.0.0.0/0`).
+ `ecs-tasks-sg` (Microservices Security Group): Allows inbound traffic on port `8000` exclusively from `alb-sg` and handles internal inter-service communication.
+ `rds-sg` (PostgreSQL Security Group): Allows inbound traffic on port `5432` strictly originating from `ecs-tasks-sg`. Never expose this database directly to the public internet.
+ `redis-sg` (ElastiCache Redis Security Group): Allows inbound traffic on port `6379` strictly originating from `ecs-tasks-sg` (specifically utilized by the Notification Worker).

![Security Groups](security-groups.png)