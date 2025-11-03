Planned updates for aggregator and access key endpoints in openapi.yaml
=====================================================================

1. Retain the existing aggregator schema (per guidance) and focus changes on shared components.
2. Expand the shared `AccessKey` schema to cover the full payload (lifecycle timestamps via the `Timestamp` schema, etc.) and add descriptive metadata so it can be reused across responses.
3. Align list and create access key responses with the observed payloads by updating the reusable response components (`AggregatorResponse`, `ListAccessKeysResponse`, `CreateAccessKeyResponse`) and embedding illustrative examples.
4. Replace inline query parameter definitions for limit/offset/names/is_active with reusable parameter components that document defaults, constraints, and examples.
5. Document the aggregator access key mutation request bodies with property descriptions and richer examples to match the current API contract.
6. Introduce an error envelope component for 401 responses (`api_version` plus nested `error`) and wire it into the existing `Unauthorized` response while preserving other error shapes.


Additional updates for aggregator merchants endpoints in openapi.yaml
=======================================================================

1. Align the `CreateMerchant` request schema with the documented fields (`merchant_external_id`, `iban`, `name`, `enabled`, `raast_merchant_id`, and `rate_card` with `ratecard_kind`, `fixed_rate`, `tax_rate`) and refresh examples to mirror the payload above.
2. Update the `UpdateMerchant` request body to match the simplified structure (`name`, `enabled`, `iban`, `rate_card` with `fixed_rate`, `tax_rate`, `tax_region`, `variable_rate`) and relax required fields to reflect optional updates.
3. Introduce reusable query parameter components for the merchant list filters (`limit`, `offset`, `enabled`, `merchant_identifiers`, `names`) so the paths reuse consistent string-typed definitions and examples.
4. Reshape the `ListMerchantsResponse` component to return `data.merchants` plus a string `count`, ensuring the example reflects the provided 200 response.
5. Verify `CreateMerchantResponse`, `FindMerchantResponse`, and `UpdateMerchantsResponse` reuse the enriched `Merchant` schema (including `bank_account`, `raast_merchant`, `rate_card`) and align property descriptions such as `rate_card.tax_rate` with the observed types.
