# Proposed OpenAPI Updates for Payments Endpoints

## Operation adjustments
- Update `/v1/aggregators/{raast-aggregator-id}/payments` POST summary to `Create RTP` and add the new guidance-rich description from product docs.
- Attach a reusable header parameter component for `X-SFPY-AGGREGATOR-SECRET-KEY` to both POST and GET operations while keeping the API key security scheme.
- Move the path parameter reuse to the path-level `parameters` array for cleaner reuse and avoid repeating on each operation.

## Request body
- Revise `components.requestBodies.CreatePayment` to describe conditional debitor identifiers (`debitor_raast_id`, `debitor_vault_token`, `debitor_iban`) and enforce the mutually exclusive requirement via `oneOf`.
- Add property descriptions, tighten enums (`type` → `RTP_NOW`, `RTP_LATER`) and numeric constraints (`expiry_in_minutes` max 180, `expiry_in_days` max 40).
- Refresh examples to show the "guideline" combinations shared in the latest docs (one example each for RTP now, later, and alias-based requests).

## Successful responses
- Introduce a dedicated schema (e.g., `PaymentCreationResult`) for the POST response payload (`message`, `token`, `msg_id`, `trace_reference`, `uetr`, `status`, `order_id`, `created_at`) and point `CreatePaymentResponse` to it with an updated example.
- Update `ListPaymentsResponse` so the `data` container exposes `payments` (not `keys`), ensure `count` mirrors the API (string) and supply a trimmed example aligned with the shared sample.
- Expand `components.schemas.Payment` with missing fields (`id`, `aggregator_merchant_id`, `amount`, timestamps, etc.), add descriptions, and keep nested relationships (`txn_logs`, `refunds`, etc.).

## Error handling
- Align `components.responses.InternalError` with the documented structure using the `ApiErrorEnvelope` schema so the error sits under `error` alongside `api_version`.

## Parameters and enums
- Document each existing query parameter on the GET (description + example) and widen enums for `status` and `type` to match the values listed in the shared snippet.

## Ancillary schema tidy-up
- Add missing `description` fields to object schemas touched by the changes (`Payment`, `TransactionLogs`, `PaymentCreationResult`).
