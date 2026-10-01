# API Contracts

## Base path
`/api/v1/cards`

## Endpoints
### GET /api/v1/cards/{token}
Returns a card summary.

Example response:
```json
{
  "id": 1,
  "maskedPan": "**** 1234",
  "status": "ACTIVE",
  "availableBalance": 2500.00
}
```

### POST /api/v1/cards/{token}/authorizations
Creates or replays a debit authorization.

Request body:
```json
{
  "idempotencyKey": "order-1001",
  "amount": 125.50,
  "currency": "INR",
  "merchant": "Demo Store"
}
```

Response:
```json
{
  "transactionId": 1,
  "status": "APPROVED",
  "availableBalance": 2374.50
}
```

### POST /api/v1/cards/{token}/block
Blocks the card.

### POST /api/v1/cards/{token}/unblock
Unblocks the card if not expired.

## Validation result
Status: PASS

The controller and DTO layer are internally consistent, the request payloads are validated, and the response model matches the service behavior described in the README and code.

## Note
The sample intentionally omits full API documentation tooling, authentication, and richer error envelopes. The current design is adequate for a demo service but would need more formal contract governance in production.
