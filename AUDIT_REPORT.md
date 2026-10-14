# Gaming Intelligence Platform v0.3.1 Audit

## Result
The v0.3 package was reviewed file-by-file and syntax-checked. Several issues were found and corrected before this build was repackaged.

## Fixed
- Connector enable flags were declared but previously ignored by the collectors. Disabled connectors now make no outbound request.
- Provider connectors previously only counted records and did not ingest games/offers/releases. They now normalize common JSON item shapes into the shared store.
- Server host was hard-coded to loopback. It is now configurable through `HOST` while retaining the safer loopback default.
- Package version and README version were inconsistent. They are now aligned to 0.3.1.
- Frontend external links now accept only `http:` and `https:` URLs, reducing URL-scheme injection risk from untrusted source data.

## Verified
- JavaScript syntax check: PASS for all project `.js` files.
- Provider disabled-path test: PASS; no network request was made.
- Provider normalization test: PASS; a mock game became a game, release/offer data was persisted.
- Express 5 SPA fallback uses `/{*splat}`.
- Admin token comparison uses `crypto.timingSafeEqual` after length checking.
- JSON writes use a temporary file followed by rename.
- `.env` and `node_modules` are excluded by `.gitignore`.

## Remaining limitations / not bugs
1. Microsoft/Xbox/Game Pass is an adapter boundary, not a turnkey public catalog API. Microsoft documents service-to-service Store APIs, but access/authentication and Partner Center configuration are required for the relevant scenarios. Some Game Pass status operations require publisher authorization.
2. PlayStation, PS Plus, Nintendo, Ubisoft, EA, Battle.net, Google Play, Apple App Store, EA Play and Ubisoft+ still require an authorized/licensed provider endpoint. The project intentionally does not bypass private APIs, CAPTCHAs or authentication.
3. Steam/Epic/Trends/news collectors remain the currently usable public-source collectors in the base build.
4. JSON persistence is suitable for an MVP, not a high-volume production deployment. PostgreSQL + Redis/job queues should replace it before scale-up.
5. The in-memory rate limiter is single-process and should be replaced by a reverse proxy/WAF plus distributed limiting for production.
6. The manual admin token is sent from the browser to the same-origin endpoint. For production, use a proper admin authentication/session system rather than a static token stored client-side.
7. Source-specific terms, rate limits and licensing still need to be reviewed before commercial deployment.

## External verification
Microsoft's current documentation confirms that its Store service APIs support service-to-service catalog/entitlement workflows, recommend Microsoft Entra ID authentication, and document Game Pass status queries subject to authorization/configuration.
