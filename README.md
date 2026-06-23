# Serverless Cost‑Optimized Microservice (API Gateway + Lambda + DynamoDB)

This repository contains a **serverless microservice** built with **Amazon API Gateway**, **AWS Lambda**, and **Amazon DynamoDB**, with a focus on:

- Serverless microservice design
- Lambda **power tuning** (performance vs cost)
- **Postman** testing
- **Cost analysis** using AWS Pricing Calculator
- **AWS Well‑Architected Pillars** and how they impact power tuning outcomes


<img width="733" height="940" alt="image" src="https://github.com/user-attachments/assets/06c76538-547d-4563-88df-312868e3f4c6" />



Serverless here means:
No servers to provision or manage.
You pay only for requests and execution time.
Scaling is automatic (API Gateway, Lambda, DynamoDB are all managed).

Microservice here means:

A small, focused service that owns a specific domain (e.g., items).

Clear API contract (CRUD operations).

Independent deployability.

This repo’s microservice:

Exposes CRUD APIs via API Gateway.

Uses a single Lambda function with an operation field to route logic.

Persists data in a DynamoDB table with partition key id.


Lambda Power Tuning
Customers use this to determine optimal memory to allocate to Lambda based on their goal i.e. best performance, or cheapest cost, or a balance etc. (remember Well Architected framework pillars!)

# Steps for Lambda Power Tuning Using Serverless Application Repository

1️⃣ Deploy the Power Tuning State Machine
Go to AWS Serverless Application Repository.

2) Search for: “AWS Lambda Power Tuning” (by Alex Casalboni).

3) Click Deploy.

Choose your region and confirm the CloudFormation stack creation.

This deploys a ##Step Functions state machine that runs multiple Lambda invocations at different memory configurations.

2️⃣ Configure IAM Permissions
Ensure your Lambda function has:

lambda:InvokeFunction

cloudwatch:GetMetricData

states:StartExecution

The SAR template usually creates these automatically, but verify if you’re integrating with existing roles.

3️⃣ Prepare Your Target Lambda Function
Identify the Lambda you want to tune.

Confirm it’s idempotent (safe to run multiple times).

Note its ARN — you’ll pass this to the state machine.

4️⃣ Start the Power Tuning Execution
Use the AWS Console, CLI, or API Gateway endpoint created by the SAR deployment.


<img width="1889" height="600" alt="Screenshot 2026-06-23 105312" src="https://github.com/user-attachments/assets/5bfa3507-0690-4dbe-9b33-09420db49493" />

<img width="1128" height="693" alt="image" src="https://github.com/user-attachments/assets/a94f2407-7e2e-48b6-b01a-16cc73ab7c13" />


Once the execution is complete, copy the # "Visualization url" under the State Output and see the garph.

<img width="975" height="421" alt="image" src="https://github.com/user-attachments/assets/a4062160-92ca-4187-bd03-ca32d0d9dfd1" />

# Key Observations


Invocation Time (ms) and Invocation Cost (USD) were measured across memory sizes: 128 MB, 256 MB, 512 MB, and 1024 MB.

Both time and cost peaked at 256 MB, meaning that configuration was the least efficient.

Performance and cost improved significantly at 512 MB, reaching the lowest combined latency and cost.

At 1024 MB, execution time improved further (fastest runtime), but cost slightly increased compared to 512 MB.

# Optimal Configuration

Best Cost: 512 MB

Best Time: 1024 MB

Worst Cost & Time: 256 MB

So, if your goal is cost efficiency, choose 512 MB.
If your goal is maximum performance, choose 1024 MB.

# Recommendation

For most workloads, 512 MB offers the best balance between speed and cost.

However, if your function is latency‑sensitive (e.g., real‑time API or analytics), 1024 MB may be worth the slight cost increase.





