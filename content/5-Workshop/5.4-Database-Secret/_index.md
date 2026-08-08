---
title: "Data Tiers & Secrets Management"
date: 2026-08-07
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

#### Objective
Initialize the Amazon RDS PostgreSQL relational database following the *Database-per-service* pattern, set up an ElastiCache Redis cache cluster for asynchronous message queuing, and centrally manage all sensitive configurations securely using AWS Secrets Manager.

#### 1. Creating Amazon RDS PostgreSQL (Database-per-service Pattern)
1. Navigate to the **RDS** service on the AWS Console -> Click **Create database**.
2. Choose **Standard create** and select the **PostgreSQL** engine.
3. Under **Templates**, select **Free tier** or **Dev/Test** (Single-AZ mode to optimize demo costs).
4. Configure parameters:
   * **DB instance identifier:** `cloud-finance-postgres`
   * **Master username:** `postgres`
   * **Master password:** Set a strong password
   * **Connectivity:** Select VPC `cloud-finance-vpc`, set **Public access** to `No` (securely isolated within Private Subnets), and attach the `rds-sg` Security Group.
5. Click **Create database**. Once provisioned, create independent logical databases corresponding to each microservice (`auth_db`, `finance_db`, `ai_db`, `notifications_db`, `planning_db`, `recurring_db`).

![RDS PostgreSQL](rds-postgres.png)

#### 2. Creating Amazon ElastiCache for Redis
1. Go to the **ElastiCache** service -> Select **Redis caches** -> Click **Create Redis cluster**.
2. Configure settings:
   * **Name:** `cloud-finance-redis`
   * **Node type:** `cache.t4g.micro`
   * **Number of replicas:** `0` (optimized for demo environments)
   * **Subnet and VPC:** Select `cloud-finance-vpc` and assign the `redis-sg` Security Group.
3. Click **Create**.

![ElastiCache Redis](elasticache-redis.png)

#### 3. Configuring AWS Secrets Manager
Instead of storing raw `.env` files on servers, all sensitive configuration details are centrally and securely managed here:
1. Navigate to the **Secrets Manager** service -> Click **Store a new secret**.
2. Choose **Other type of secret**, and enter the Key/Value pairs containing database connection strings, the Gemini API key, and the JWT secret string.
3. Name the secret `cloud-finance/production-secrets` and complete creation.

![Secrets Manager](secrets-manager.png)