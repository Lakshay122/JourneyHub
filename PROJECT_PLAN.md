# JourneyHub — Project Plan

JourneyHub is a microservice-based railway ticket booking platform designed to handle scalability, concurrent processing, and distributed architecture workloads. This document outlines the planned services and development approach.

---

## 1. Auth Service

### Purpose
To manage user identity, authentication mechanisms, and session tokens.

### Responsibilities
* Signup
* Login
* Password hashing
* Google OAuth
* Token/session management
* Authentication
* Authorization

### Engineering Considerations
* Secure password handling
* Token security
* OAuth security
* Role-based authorization
* Authentication between services

---

## 2. User Service

### Purpose
To manage user profiles, preferences, and personal information independently from authentication concerns.

### Responsibilities
* User profile
* Profile updates
* User preferences
* User-related information

### Engineering Considerations
* Separation between authentication and user data
* Authorization
* Data validation
* Service boundaries

---

## 3. Search Service

### Purpose
To provide fast, reliable, and intelligent search capabilities for stations, trains, and routes.

### Responsibilities
* Source → destination train search
* Station search
* Train search
* Fuzzy search
* Autocomplete

### External Dependencies
* Elasticsearch
* Redis

### Engineering Considerations
* Elasticsearch indexing
* Search relevance
* Fuzzy matching
* Autocomplete
* Search performance
* Caching
* Elasticsearch should not be treated as the primary transactional source of truth

---

## 4. Route Service

### Purpose
To act as the primary catalog and management point for all railway data, including stations and train schedules.

### Responsibilities
* Station management
* Train management
* Route management
* Create/update railway routes
* Admin operations

### Engineering Considerations
* Data validation
* Admin authorization
* Relationship between trains, stations, and routes
* Maintaining consistent railway data

---

## 5. Booking Service

### Purpose
To manage the core transactional workload of availability verification and securing tickets.

### Responsibilities
* Availability checking
* Ticket booking
* Seat/resource locking
* Concurrent booking
* Partial booking
* Booking cancellation
* Booking state management

### Engineering Considerations
This service is a major focus of the project.
* Race conditions
* Concurrent requests
* Double booking prevention
* Transactions
* Locking
* Idempotency
* Booking expiration
* Payment failure scenarios
* Retry handling
* Partial booking scenarios

The implementation should be designed carefully rather than relying only on application-level checks.

---

## 6. Payment Service

### Purpose
To manage financial transactions, webhooks, and encapsulate interactions with multiple payment providers.

### Responsibilities
* Payment initiation
* Payment verification
* Payment status
* Refunds
* Payment webhooks
* Multiple payment gateways

### Design Pattern
Use the **Adapter Pattern** to abstract different payment providers.
Conceptually:
`Payment Service → Payment Gateway Interface → Gateway Adapter`
The Booking Service should not be tightly coupled to a specific payment provider.

### Engineering Considerations
* Gateway failure
* Gateway fallback
* Retry handling
* Idempotency
* Webhook verification
* Payment/booking consistency
* Secure handling of payment credentials

---

## 7. Archive Service

### Purpose
To offload historical data management, keeping active operational databases lean and performant.

### Responsibilities
* Archive completed/old bookings
* Process archival asynchronously
* Store historical data
* Retrieve archived journey/booking information when required

### External Dependencies
* BullMQ
* Cassandra

### Engineering Considerations
* Background processing
* Retryable jobs
* Failure handling
* Data consistency
* Archival strategy
* Keeping operational data separate from historical data

---

# External Infrastructure

* **PostgreSQL**: Serves as the primary relational database across transactional microservices ensuring ACID compliance.
* **Prisma**: Acts as the ORM and data-access layer to interact cleanly and safely with PostgreSQL databases.
* **Elasticsearch**: The search engine backing the Search Service for advanced querying, full-text capabilities, and fuzzy matching.
* **Redis**: Used as a fast, in-memory store for caching search results and managing distributed locking or coordination mechanisms.
* **BullMQ**: A robust queue system built on Redis for handling background tasks and asynchronous event processing (e.g., in the Archive Service).
* **SendGrid**: An external provider for sending transactional emails reliably (confirmations, cancellations, etc.).
* **Cassandra**: A highly scalable NoSQL database optimized for heavy write workloads, leveraged by the Archive Service for long-term historical data storage.
* **Docker**: Containerization technology utilized to package services consistently for both development and deployment environments.
* **AWS EC2**: The planned cloud virtual server infrastructure on AWS where the containerized services will be hosted.
* **Domain/HTTPS**: Custom domain configuration with SSL certificates to securely expose the platform endpoints to users.

---

# Development Approach

JourneyHub will be developed incrementally.

The development process should follow:
1. Define the service responsibility.
2. Design HLD.
3. Design LLD.
4. Identify data requirements.
5. Identify external dependencies.
6. Implement the service.
7. Add tests.
8. Integrate with other services.
9. Dockerize.
10. Deploy and validate.

The architecture should evolve based on actual requirements rather than prematurely fixing every design decision.

---
