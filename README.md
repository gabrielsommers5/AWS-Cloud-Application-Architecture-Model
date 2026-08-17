# AWS-Cloud-Application-Architecture-Model
An AWS Cloud Application Architecture Model for Hive App

# Hive – Distributed Cloud Architecture & System Design

A scalable, fault-tolerant, and secure cloud backend designed for "Hive"—a unified campus communication and event discovery platform for student organizations.

---

## 🏛️ Architecture Overview

The system employs a serverless-first, hybrid cloud architecture on AWS designed to balance real-time responsiveness, transactional consistency, and cost-efficient scalability.

![Hive AWS Architecture Diagram](./architecture-diagram.png)

---

## 🚀 Key Architectural Highlights

* **Edge Network & Identity:** 
  * Static assets and file uploads are cached via **Amazon CloudFront** and stored in encrypted **Amazon S3** buckets.
  * Distributed DNS resolution through **Amazon Route 53** with **AWS Shield** DDoS mitigation.
  * Centralized user authentication, role management, and session tokens handled via **Amazon Cognito User Pools**.

* **Dual API Ingestion Layer:**
  * **AWS AppSync (GraphQL):** Provides low-latency WebSockets connections for real-time club chat channels and live campus feeds.
  * **Amazon API Gateway (REST):** Manages stateless transactional requests for event creation, RSVPs, and administrative workflows.

* **Hybrid Compute & Data Tier:**
  * **AWS Lambda:** Event-driven microservices running compute logic for message dispatch, post creation, and RSVP processing.
  * **Amazon DynamoDB:** Single-digit millisecond latency NoSQL store for high-throughput messaging, feeds, and post metadata.
  * **Amazon RDS (Multi-AZ):** Relational storage ensuring ACID compliance for structured event planning, club registries, and attendee tracking.

* **Asynchronous Processing & Notifications:**
  * **Amazon SQS + Amazon ECS:** Decoupled background task queue for automated campus feed moderation running on containerized worker tasks.
  * **Amazon EventBridge + Amazon SNS:** Scheduled rules trigger time-sensitive event reminders fanned out via SNS push notifications.

---

## 🔒 Security & Trust Boundaries

* **Zero Direct Public Ingress:** Compute resources (Lambda, ECS) and database layers (RDS, DynamoDB) are strictly contained inside a private **AWS VPC** boundary.
* **Least-Privilege Access:** Comprehensive **AWS IAM** service-linked roles restrict inter-service communication.
* **Data Protection:** End-to-end encryption at rest using **AWS KMS** and in-transit using TLS 1.3 across all edge and internal endpoints.
* **Governance:** System-wide API auditing via **AWS CloudTrail** and continuous operational monitoring with **Amazon CloudWatch** and **AWS X-Ray**.

---

## 🛠️ AWS Services Used

| Category | Services |
| :--- | :--- |
| **Compute & Containers** | AWS Lambda, Amazon ECS, Amazon ECR |
| **Databases & Storage** | Amazon DynamoDB, Amazon RDS, Amazon S3, AWS Backup |
| **Networking & APIs** | Amazon Route 53, Amazon CloudFront, AWS AppSync, Amazon API Gateway, Amazon VPC |
| **Security & Identity** | Amazon Cognito, AWS IAM, AWS KMS, AWS Shield |
| **Messaging & Queues** | Amazon EventBridge, Amazon SQS, Amazon SNS |
| **Monitoring & Analytics** | Amazon CloudWatch, AWS X-Ray, AWS CloudTrail, Amazon Athena, Amazon QuickSight |
