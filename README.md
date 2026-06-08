# Backend Engineer Technical Assessment (Rust)

## Overview

This assessment is designed to evaluate practical backend engineering skills using Rust, including API development, asynchronous programming, database integration, authentication, and system design.

The assessment consists of:

* **Task 1 — Backend API (Required)**
* **Task 2 — Real-Time Market Stream (Bonus)**

---

# Task 1 — Backend API

### Objective

Build a small REST API for a simplified stock portfolio system using the provided Kick Off repository.

### Skills Evaluated

* Rust fundamentals
* Async programming
* REST API design
* Database integration
* Authentication & authorization
* Error handling
* Project organization and maintainability

---

## Technical Requirements

### Stack

* Rust (stable)
* Axum *(preferred)* or Actix Web
* PostgreSQL
* SQLx or SeaORM

---

## Required Endpoints

### Authentication

#### Register User

```http
POST /register
```

Creates a new user account.

---

#### Login

```http
POST /login
```

Authentates a user and returns a JWT token.

---

### Portfolio

#### Get Portfolio

```http
GET /portfolio
```

Authentication required.

Returns the user's current portfolio holdings.

Example response:

```json
{
  "AAPL": 25,
  "TSLA": 10,
  "NVDA": 5
}
```

---

#### Buy Shares

```http
POST /portfolio/buy
```

Authentication required.

Example request:

```json
{
  "symbol": "AAPL",
  "shares": 10
}
```

---

#### Sell Shares

```http
POST /portfolio/sell
```

Authentication required.

Example request:

```json
{
  "symbol": "AAPL",
  "shares": 5
}
```

---

## Business Rules

### Portfolio Aggregation

Portfolio responses must return the total number of shares owned per symbol.

Example:

```json
{
  "AAPL": 15,
  "TSLA": 20
}
```

---

### Selling Restrictions

Users must **not** be able to sell more shares than they currently own.

Invalid example:

```text
Owned: 10 AAPL
Attempting to sell: 15 AAPL
```

Expected result:

```http
400 Bad Request
```

or an equivalent business validation error.

---

### Transactions

Use database transactions where appropriate to ensure consistency of portfolio updates.

---

## Deliverables

Submit the following:

### Source Code

Complete working implementation.

### Documentation

A `README.md` containing:

* Project overview
* Setup instructions
* Database migration steps
* Environment configuration
* Running locally

### Docker Support

Provide:

```text
docker-compose.yml
```

for local development.

### API Examples

Include examples using either:

* cURL
* HTTP files
* Postman collection

---

# Task 2 — Real-Time Market Stream (Bonus)

### Objective

Build a WebSocket service that broadcasts simulated stock prices in real time.

### Skills Evaluated

* Concurrency
* Async Rust
* WebSockets
* Streaming data
* Performance awareness
* Client connection management

---

## Requirements

### WebSocket Endpoint

```http
GET /ws
```

---

### Market Simulation

Generate simulated price updates every second for at least five stock symbols.

Example:

```json
{
  "symbol": "AAPL",
  "price": 192.14,
  "timestamp": "2026-06-08T12:00:00Z"
}
```

Suggested symbols:

```text
AAPL
TSLA
NVDA
MSFT
AMZN
```

---

### Functional Requirements

#### Multiple Concurrent Clients

The server must support multiple active WebSocket connections simultaneously.

#### Graceful Disconnect Handling

Disconnected clients should be cleaned up without affecting other active connections.

#### Non-Blocking Runtime

Avoid blocking operations within the async runtime.

Use asynchronous primitives and patterns appropriate for Rust.

---

# Evaluation Criteria

Candidates will be assessed on:

| Area              | Focus                                  |
| ----------------- | -------------------------------------- |
| Rust Fundamentals | Ownership, borrowing, type safety      |
| Async Programming | Tokio, async/await usage               |
| API Design        | Endpoint structure and maintainability |
| Database Usage    | Schema design, queries, transactions   |
| Authentication    | JWT implementation and security        |
| Error Handling    | Robust and idiomatic error management  |
| Code Quality      | Readability, organization, testing     |
| Concurrency       | WebSocket architecture and scalability |
| Documentation     | Clarity and completeness               |

---

# Submission

Please provide:

* Source code repository
* README documentation
* Docker configuration
* Migration scripts
* Example API requests
* Bonus WebSocket implementation (optional)

Good luck, and we look forward to reviewing your solution.
