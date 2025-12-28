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

Step-by-step build and deployment notes are in [process.md](process.md).