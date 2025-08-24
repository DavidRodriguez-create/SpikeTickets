# SpikeTickets
🎟️ SpikeTickets – Scalable Ticketing for High-Demand Events  SpikeTickets is a modern, microservices-based backend platform designed to handle high-traffic ticket sales for concerts, festivals, and large-scale events. Built for resilience and scalability, it ensures fast, reliable, and secure transactions — even during the biggest demand spikes.

spiketickets-mvp/
│
├── event-service/
│   └── src/main/java/org/spiketickets/event/
├── ticket-service/
│   └── src/main/java/org/spiketickets/ticket/
├── order-service/
├── payment-service/
├── email-service/
└── shared-lib/  # shared DTOs, utils, clients


🏗️ Phase 3: Create Quarkus Microservices

Each microservice is a separate Quarkus project (can use Maven or Gradle).

1. event-service
Endpoints:

POST /events: Create event

GET /events/{id}: Get event

GET /events: List all

Entities:

Event: id, name, date, venue, totalTickets

2. ticket-service
Responsibilities:

Manage ticket inventory

Prevent overbooking with atomic reservations (e.g., Redis Locking)

Endpoints:

POST /tickets/reserve: Reserve ticket

POST /tickets/release: Release (cancel)

GET /tickets/availability?eventId=...: Availability check

3. order-service
Responsibilities:

Create order and handle status updates

Call payment-service and ticket-service

Endpoints:

POST /orders: Create order (includes user info, ticket info)

GET /orders/{id}: Fetch order status

Flow:

Call ticket-service to reserve

Call payment-service to pay

On success, finalize order

Send email confirmation

4. payment-service
Integration:

Use Stripe Java SDK or mock

In sandbox, simulate payments

Endpoints:

POST /payments: Charge card

GET /payments/{id}: Status

5. email-service
Implementation:

Use quarkus-mailer or send via SendGrid (HTTP API)

Endpoint:

POST /email/send: Send email


| Feature                                | Status |
| -------------------------------------- | ------ |
| Microservices bootstrapped w/ Quarkus  | ❌      |
| PostgreSQL integration with Panache    | ❌      |
| Kafka/Redis queue support for spike    | ❌      |
| Stripe payment flow (mock OK)          | ❌      |
| Redis-based ticket locking/reservation | ❌      |
| REST APIs for ticket purchase          | ❌      |
| Confirmation email service             | ❌      |
| Containerized + deployed               | ❌      |
