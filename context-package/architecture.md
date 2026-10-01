# Architecture

## Summary
This project is a compact Spring Boot microservice for debit card lifecycle management and authorization checks. It follows a layered pattern typical of a small banking sample:

- Web layer: `controller` package exposes REST endpoints.
- Service layer: `service` package contains business logic and transaction boundaries.
- Persistence layer: `repository` package wraps Spring Data JPA repositories.
- Domain model: `entity` package models cards, customers, and transactions.
- DTOs and exceptions: `dto`, `exception`, and `config` packages support validation and error handling.

## Runtime composition
- `DebitCardServiceApplication` bootstraps the application and enables scheduling and configuration properties.
- `CardController` is the REST boundary for querying, authorizing, blocking, and unblocking cards.
- `CardService` validates business rules, coordinates repository access, and wraps operations in transactions.
- `DebitCardRepository` and `CardTransactionRepository` provide persistence access and idempotency lookup.
- `CardProperties` binds debit limits from `application.yml`.
- H2 is configured as the embedded database for local development.

## Data flow
1. Client sends request to `/api/v1/cards/{token}`.
2. Controller delegates to `CardService`.
3. Service loads the `DebitCard` using the token.
4. Service validates card state, balance, expiry, and limits.
5. If authorization is valid, it debits the card and records a `CardTransaction`.
6. Repository persistence returns data back to the controller and client.

## Architectural assessment
Status: PASS

Why it passes:
- Clear separation of concerns.
- Spring stereotype annotations are used correctly.
- JPA entities and repositories are aligned with a conventional domain model.
- Validation and exception handling are in place for business errors.

Warnings:
- This is not production-grade security or observability; there is no OAuth2, audit trail, or tracing.
- The project is intentionally a demo and uses an in-memory H2 database plus `ddl-auto` semantics.
- Daily limit logic is present in configuration but not fully implemented as an atomic aggregate check.
