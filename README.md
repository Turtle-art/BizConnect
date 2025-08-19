# **BizConnect – Serverless Business Directory Platform**

BizConnect is a **serverless microservices application** that allows businesses to list their services, and customers to search, review, and interact with them.
It’s built with **.NET (Lambdas)**, **Angular**, **AWS managed services**, and **Amazon SQS** for microservice communication, designed for **low cost and easy scaling**.

---

## 🚀 Features

* Business registration & profile management

* Customer reviews & ratings
* Secure authentication with **AWS Cognito**
* Asynchronous event-driven workflows using **Amazon SQS**
* Notifications (welcome emails, review alerts, billing receipts) via **Amazon SES**
* Fully serverless & auto-scaling infrastructure

---

## 🏗️ Architecture

* **Frontend**: Angular app hosted on **Amazon S3** + distributed via **CloudFront**
* **Backend APIs**: **.NET 8 AWS Lambda functions** exposed through **Amazon API Gateway**
* **Auth**: **Amazon Cognito** for signup, login, and JWT-based authorization
* **Data Storage**:

  * **DynamoDB** (serverless, pay-per-request, for reviews/analytics) or
  * **Aurora Serverless v2** (PostgreSQL, for structured relational data)
* **Event Messaging**: **Amazon SQS** queues for decoupled service-to-service communication
* **Notifications**: **Amazon SES** for email delivery
* **Monitoring**: **CloudWatch** for logs and metrics

---

## ⚙️ Microservices

| Service                  | Responsibilities                             |
| ------------------------ | -------------------------------------------- |
| **User Service**         | User registration, authentication, roles     |
| **Business Service**     | Business profiles, categories, updates       |
| **Review Service**       | Customer reviews & ratings                   |
| **Notification Service** | Sends transactional emails via SES           |
| **Billing Service**      | Subscription, pay-per-lead, commission logic |
| **Analytics Service**    | Usage metrics, reporting                     |

Each service runs as a **Lambda function** and communicates asynchronously via **SQS queues**.

---

## 📦 Deployment

1. **Frontend**

   * Build Angular app (`ng build --prod`)
   * Upload build artifacts to S3 bucket
   * Configure CloudFront for CDN + HTTPS

2. **Backend**

   * Package each .NET service as a Lambda
   * Deploy via AWS SAM / CDK / Serverless Framework
   * Configure API Gateway routes

3. **Infrastructure**

   * DynamoDB or Aurora Serverless for persistence
   * Create SQS queues for event topics (`business.created`, `review.submitted`, etc.)
   * Configure SES for outbound email
   * Set up Cognito user pool for authentication
  
     
<img width="1547" height="1088" alt="bizConnect" src="https://github.com/user-attachments/assets/3b970386-683e-4350-b3db-3575ac6346ac" />

---

## 💰 Cost Optimization

* **Serverless-first**: Pay only when used
* **S3 + CloudFront**: Pennies per month for frontend hosting
* **DynamoDB**: Free tier + pay-per-request pricing
* **Lambda**: Free tier includes 1M requests/month
* **Cognito**: Free up to 50k monthly active users
* **SES**: 62k emails/month free if sent from Lambda

---

## 🛡️ Security

* IAM policies with least privilege per Lambda
* API Gateway + Cognito for request-level auth
* SQS DLQs (Dead Letter Queues) for failed messages
* Encrypted storage (DynamoDB/Aurora, S3)

---

## 📌 Roadmap

* Add business search with **OpenSearch** (later stage)
* Introduce **Kafka (MSK)** when scaling requires event replay & high throughput
* Add mobile app client (React Native/Ionic)

---
