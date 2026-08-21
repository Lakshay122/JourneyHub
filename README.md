# JourneyHub

JourneyHub is a production-oriented railway ticket booking platform inspired by systems like IRCTC. The project is built with a microservice architecture and designed to demonstrate real-world backend engineering and distributed-system concepts.

## Planned Services

* **Auth Service**
  Features: User signup, user login, password authentication, Google OAuth, authentication/token management, and authentication-related security.
* **User Service**
  Features: User profile management, update profile, user information, user preferences, and user-related operations.
* **Search Service**
  Features: Search trains from source to destination, search by station, Elasticsearch integration, fuzzy search, autocomplete, fast search results, and search result caching using Redis where appropriate.
* **Route Service**
  Features: Station management, train management, route management, add new station, add new train, add/update routes, and admin operations for railway data.
* **Booking Service**
  Features: Train/seat availability, ticket booking, concurrent booking handling, prevent double booking, seat/resource locking, partial booking, booking confirmation, booking cancellation, booking status management, and idempotent booking operations.
* **Payment Service**
  Features: Payment initiation, payment verification, payment status management, multiple payment gateway support, payment gateway abstraction, Adapter Pattern for payment providers, gateway fallback/failover, payment retry handling, payment webhook handling, and refund handling where applicable.
* **Archive Service**
  Features: Identify completed/old booking data, archive completed journeys/bookings, asynchronous archival processing, store historical data in Cassandra, and keep active transactional data separate from historical data.

---

# External Services & Infrastructure

### PostgreSQL
Primary relational database for transactional services.

### Prisma
ORM/data-access layer for PostgreSQL.

### Elasticsearch
Used by Search Service for:
* Full-text search
* Fuzzy search
* Autocomplete
* Train/station search

### Redis
Used for:
* Caching
* Temporary data
* Performance optimization
* Distributed coordination/locking where appropriate

### BullMQ
Used for asynchronous/background jobs such as:
* Booking-related background processing
* Email jobs
* Archive jobs
* Other non-blocking operations

### SendGrid
Used for transactional emails such as:
* Booking confirmation
* Cancellation
* Payment notifications
* Account-related emails

### Cassandra
Used by Archive Service for historical booking/journey data.

### Docker
Used for containerizing services and creating reproducible environments.

### AWS EC2
Planned cloud infrastructure for deploying the services.

### Domain & HTTPS
The final project will be deployed under a custom domain with HTTPS.

---

# Engineering Concepts

JourneyHub will focus on the following planned capabilities:
* High-Level Design (HLD)
* Low-Level Design (LLD)
* Microservice architecture
* SOLID principles
* Clean architecture
* Design patterns
* Concurrency
* Distributed systems
* Caching
* Asynchronous processing
* Fault tolerance
* Idempotency
* Scalability
* Security
* Production-oriented deployment

*(Note: These have not yet been implemented and are planned capabilities that will be incrementally designed during development.)*
