# Transaction Notification Pipeline on AWS

Serverless pipeline that delivers real-time bank transaction notifications to end users using AWS Lambda and DynamoDB. Built for the EAZYCard service to close the gap between internal back-office alerts and timely customer-facing notifications.

## Problem Statement

Before this pipeline, the bank sent transaction events only to the internal EAZYCard operations app. End users never saw real-time alerts for their own transactions, creating slow reactions to fraud, limited transparency, and a frustrating customer experience.

## Solution and Impact

- Real-time accessibility: users now receive instant transaction notifications instead of waiting for back-office relays.
- Scalability: auto-scales from thousands to millions of events without throughput loss thanks to serverless components.
- Cost efficiency: pay-per-use Lambda and DynamoDB eliminate idle infrastructure costs.
- Security: immediate alerts help users spot suspicious activity faster.
- Low ops overhead: no servers to manage; monitoring and logging stay centralized.

## Architecture

![Architecture](<Architecture App.png>)

## AWS Services

- API Gateway: routes external requests, auth, throttling, and caching for the notification API surface.
- Secrets Manager: stores credentials and API keys securely.
- IAM: roles and permissions for Lambda, EventBridge, DynamoDB, SES, and supporting services.
- S3: object storage for artifacts (code bundles, configs, or archives).
- DynamoDB: low-latency NoSQL store for transaction records and notification state.
- Lambda: serverless compute for ingest, processing, and notification dispatch.
- SES: outbound email delivery for user notifications.
- EventBridge: event routing between producers and the notification workflow.
- CloudWatch (Logs, Metrics): centralized logging, metrics, and alarms.

## Implementation Process

1) Design architecture: diagram API Gateway, Lambda, DynamoDB, SES, EventBridge, CloudWatch, and S3 for artifacts.
2) Configure access: create IAM roles/permissions and store secrets in Secrets Manager.
3) Set up data and storage: model DynamoDB tables for users/transactions; create S3 bucket for Lambda artifacts.
4) Build business logic: implement Lambda functions for ingest, processing, and notification dispatch; wire API Gateway endpoints.
5) Orchestrate events: add EventBridge rules that trigger Lambda from bank transaction events.
6) Notify users: configure SES (domain/email verification) for outbound mail.
7) Observe and protect: enable CloudWatch logs/metrics/alarms for Lambda and API Gateway.
8) Test and scale: run functional/integration tests and load scenarios; deploy via IaC (e.g., CloudFormation or terraform) and keep maintenance plans in place.