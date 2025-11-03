Planned updates for aggregator and access key endpoints in openapi.yaml
=====================================================================

1. Retain the existing aggregator schema (per guidance) and focus changes on shared components.
2. Expand the shared `AccessKey` schema to cover the full payload (lifecycle timestamps via the `Timestamp` schema, etc.) and add descriptive metadata so it can be reused across responses.
3. Align list and create access key responses with the observed payloads by updating the reusable response components (`AggregatorResponse`, `ListAccessKeysResponse`, `CreateAccessKeyResponse`) and embedding illustrative examples.
4. Replace inline query parameter definitions for limit/offset/names/is_active with reusable parameter components that document defaults, constraints, and examples.
5. Document the aggregator access key mutation request bodies with property descriptions and richer examples to match the current API contract.
6. Introduce an error envelope component for 401 responses (`api_version` plus nested `error`) and wire it into the existing `Unauthorized` response while preserving other error shapes.
