---
title: "Frontend Deployment on S3 & CloudFront"
date: 2026-08-07
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

#### Objective
Store the Single Page Application (ReactJS) frontend source code on Amazon S3, utilize Amazon CloudFront for high-speed static content delivery via OAC security mechanisms, and integrate AWS WAF to protect the application against malicious attacks.

#### 1. Configuring S3 Bucket for Frontend
1. Access the **Amazon S3** service on the AWS Console -> Click **Create bucket**.
2. Name the bucket (e.g., `cloud-finance-frontend-<account-id>`) and enable **Block all public access** to ensure strict security.
3. Build the ReactJS source code locally using the `npm run build` command and upload the entire `dist` folder contents to this S3 bucket.

![S3 Buckets](s3-buckets.png)

#### 2. Configuring Amazon CloudFront Distribution
1. Navigate to the **Amazon CloudFront** service -> Click **Create distribution**.
2. **Origin domain:** Select the frontend S3 bucket created previously.
3. **Origin access:** Choose **Origin access control (OAC)** and create a new OAC configuration so that CloudFront remains the sole authorized channel accessing S3 directly.
4. **Behavior configuration:**
   * Configure routing for static assets back to S3.
   * Set up forwarding rules so requests prefixed with `/api/*` or `/ws/*` route directly to the **Application Load Balancer (ALB)**.
5. Integrate **AWS WAF** into the CloudFront distribution to filter and block malicious traffic patterns.

![CloudFront](cloudfront.png)