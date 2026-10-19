# Digital Banking Fraud Detection System

## 1. Project Overview

This project is a simulated digital banking system that supports customer accounts, money transfers using virtual funds, transaction history, and fraud detection.

**Important:** This is a learning and portfolio project. It does not process real bank transactions.

## 2. System Components

### Spring Boot
- Provides REST APIs.
- Handles authentication and authorization.
- Validates transfers and coordinates business logic.

### PostgreSQL
- Stores users, accounts, transfers, and the transaction ledger.
- Acts as the durable source of truth for financial records.

### Redis
- Stores short-lived fraud detection counters and velocity signals.
- Helps identify unusual transaction patterns.

### Kafka
- Transmits transaction events between application components.
- Supports asynchronous processing, retries, and event-driven workflows.

### React
- Provides the customer and fraud analyst user interface.

## 3. Money Transfer Flow

1. The customer submits a transfer request.
2. The API authenticates the customer and validates the request.
3. The system checks the account balance and idempotency key.
4. The fraud engine evaluates the transaction risk.
5. The system approves, rejects, or sends the transaction for review.
6. Approved transfers are processed using safe database transactions and a tracked workflow.
7. Transaction events are published for downstream processing.
8. The customer can view the final transfer status and transaction history.

## 4. Fraud Detection Flow

1. Receive the transfer request.
2. Evaluate configurable rules such as transfer amount and transaction frequency.
3. Use Redis counters for short-term transaction velocity signals.
4. Calculate a risk score.
5. Decide whether to approve, reject, or flag the transaction for manual review.
6. Record the decision and its reason for auditing.

## 5. Reliability and Data Consistency

- PostgreSQL is the source of truth for balances and ledger entries.
- Redis and Kafka must not replace the financial database.
- Idempotency prevents duplicate requests from causing duplicate financial effects.
- A transactional outbox helps reliably publish events after database commits.
- A Saga workflow and compensating actions help manage failures across multiple steps.
- Automated tests will cover concurrency, retries, duplicate requests, and failure recovery.

## 6. Security

- Authenticate users before allowing protected operations.
- Enforce role-based access for customers and fraud analysts.
- Never store plaintext passwords or commit credentials to GitHub.
- Keep audit records for important financial and administrative actions.

## 7. Planned Technology Stack

- Java and Spring Boot
- Spring Security
- PostgreSQL and Flyway
- Redis
- Apache Kafka
- React and TypeScript
- Docker Compose
- JUnit and Testcontainers
- GitHub Actions

## 8. Implementation Strategy

The project will be built incrementally:

1. Requirements and architecture.
2. Core banking API and database consistency.
3. Fraud rules and risk assessment.
4. Kafka events and reliable event publishing.
5. Saga orchestration and recovery.
6. Frontend, security, testing, and deployment.

The system is a simulated banking application for learning and demonstration, not a certified production banking platform.
