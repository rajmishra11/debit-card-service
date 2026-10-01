# Domain Constraints

## Core business rules
1. Card lookup requires a valid token and returns a masked PAN plus status and balance.
2. A card can be blocked or unblocked.
3. A card must be `ACTIVE` before authorization succeeds.
4. Authorization rejects requests above the configured single-transaction limit.
5. Authorization rejects attempts that exceed available balance.
6. Expired cards cannot be unblocked.
7. Idempotency key reuse returns the same approval result instead of creating duplicate authorizations.

## Entities and invariants
- `DebitCard` holds token, masked PAN, status, balance, expiry date, and customer relation.
- `CardTransaction` stores the authorization record, including currency, merchant, status, and timestamp.
- `CardStatus` is treated as an enumerated lifecycle state.
- `TransactionStatus` reflects approval outcomes.

## Validation result
Status: PASS

The service logic enforces the key business constraints at the domain-service layer, and the repository enforces a unique idempotency constraint at the data layer.

## Production note
The sample is intentionally simple. In production, daily limits and balance calculations should be enforced atomically with database constraints and concurrency-safe transactional logic.
