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
