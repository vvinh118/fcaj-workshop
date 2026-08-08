---
title: "Resource Cleanup"
date: 2026-08-07
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

#### Objective
After successfully completing the workshop and testing the system in the cloud, cleaning up resources is crucial to prevent unexpected ongoing charges from AWS services.

#### Cleanup Steps
Perform the deletion or deactivation of resources sequentially from the application layer down to the underlying infrastructure:

1. **Scale Down ECS Services:**
   * Access the Amazon ECS Console and select the `cloud-finance-cluster` cluster.
   * Update the `Desired count` for all Services to `0` to completely stop running containers.
2. **Delete Load Balancers & Target Groups:**
   * Go to the EC2 Console -> Select **Load Balancers**.
   * Delete `cloud-finance-alb`, then navigate to the **Target Groups** tab to delete associated target groups.
3. **Delete RDS PostgreSQL & ElastiCache Redis:**
   * Navigate to the RDS Console -> Select the `cloud-finance-postgres` database and choose **Delete** (you may opt to create a final snapshot or skip it).
   * Go to the ElastiCache Console -> Select the `cloud-finance-redis` cluster and delete it.
4. **Delete NAT Gateways & Elastic IPs:**
   * Access the VPC Dashboard -> Select **NAT gateways** and delete them.
   * Go to **Elastic IPs** to release static IP addresses and prevent holding fees.
5. **Delete CloudFront & S3 Buckets:**
   * Navigate to the CloudFront Console, disable and subsequently delete the `CloudFront Distribution`.
   * Go to the S3 Console, empty and permanently delete the S3 buckets created for the frontend and receipt storage.