---
title: "ECS Fargate & ALB Deployment"
date: 2026-08-07
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Objective
Initialize the serverless ECS Cluster, configure the Application Load Balancer to route traffic, and set up Task Definitions to run microservices combined with secure configuration injection from AWS Secrets Manager.

#### 1. Creating the Amazon ECS Cluster
1. Navigate to the **Amazon ECS** service on the AWS Console.
2. Select **Clusters** -> Click **Create cluster**.
3. Name the cluster: `cloud-finance-cluster`.
4. Under **Infrastructure**: Choose **AWS Fargate** (serverless).
5. Click **Create**.

![ECS Cluster](ecs-cluster.png)

#### 2. Configuring Application Load Balancer (ALB)
1. Go to the **EC2** service -> Section **Load Balancing** -> Select **Load Balancers** -> Click **Create Load Balancer**.
2. Choose **Application Load Balancer**.
3. Configure parameters:
   * **Name:** `cloud-finance-alb`
   * **Scheme:** `Internet-facing`
   * **VPC:** Select `cloud-finance-vpc` and 2 Public Subnets
   * **Security groups:** Select `alb-sg`
4. Create Target Groups (e.g., `tg-gateway` on port `8000`, health check path `/health`) and finalize the ALB creation.

![ALB](alb.png)

#### 3. Initializing Task Definitions and ECS Services
1. In the ECS Console, select **Task definitions** -> **Create new task definition**.
2. Set the family name (e.g., `cloud-finance-gateway-task`), choose **AWS Fargate** as the launch type with `awsvpc` network mode.
3. Define **Container Definitions**: point to the ECR image, open port `8000`, and configure the `secrets` section to automatically pull sensitive values from AWS Secrets Manager into environment variables upon container startup.
4. Return to `cloud-finance-cluster`, click **Create Service** to run the service, attach it to the ALB, and enable **Service Connect** to allow seamless internal inter-service communication.

![ECS Services](ecs-services.png)