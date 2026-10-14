# Gaming Intelligence Platform — Connector Guide

The platform uses adapters instead of asking users for store passwords.

## Microsoft / Xbox / Game Pass

Set `MICROSOFT_STORE_ACCESS_TOKEN` and the authorized catalog endpoints in `XBOX_CATALOG_URL` and `GAMEPASS_CATALOG_URL` when you have the required Microsoft partner/service authorization.

Microsoft documents Store service APIs for service-to-service catalog/entitlement workflows. Some Game Pass status operations require publisher authorization. The project therefore does not pretend that a consumer Microsoft login is a catalog API.

## Other stores

PlayStation, PS Plus, Nintendo, Ubisoft, EA, Battle.net, Google Play, Apple App Store, EA Play and Ubisoft+ use provider adapters. Set the corresponding `*_PROVIDER_URL` and optional key only when you have an authorized or licensed data source.

The adapters expect JSON and accept these common shapes:

- an array: `[{...}]`
- `{ "items": [...] }`
- `{ "products": [...] }`
- `{ "value": [...] }`

This lets us swap providers without changing the rest of the platform.

## Security

- Never put a consumer store password in `.env`.
- Keep API keys server-side.
- Use a secret manager in production.
- Restrict outbound calls to known provider hosts in production.
- Respect each provider's terms, rate limits and licensing.
