# Serverless Cost‑Optimized Microservice (API Gateway + Lambda + DynamoDB)

This repository contains a **serverless microservice** built with **Amazon API Gateway**, **AWS Lambda**, and **Amazon DynamoDB**, with a focus on:

- Serverless microservice design
- Lambda **power tuning** (performance vs cost)
- **Postman** testing
- **Cost analysis** using AWS Pricing Calculator
- **AWS Well‑Architected Pillars** and how they impact power tuning outcomes

---

## 1. Architecture overview

```text
End User (Browser / Mobile / Postman)
        |
        | HTTPS (TLS 1.2+ / 1.3)
        v
+------------------------+
|   Amazon API Gateway   |
| - REST endpoints       |
| - Auth, throttling     |
+-----------+------------+
            |
            v
+------------------------+
| AWS Lambda (CRUD)      |
| - create/read/update   |
|   delete on DynamoDB   |
| - Power tuned          |
+-----------+------------+
            |
            v
+------------------------+
| Amazon DynamoDB        |
| - NoSQL table          |
| - KMS encryption       |
+------------------------+
