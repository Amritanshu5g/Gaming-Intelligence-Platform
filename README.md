# Gaming Intelligence Platform v0.3.4

A dark, automatic gaming intelligence dashboard focused on **gaming-only news**, upcoming releases, trends, deals, free games, game discovery and transparent activity signals.

## What v0.3.4 adds
- Redesigned black/blue dashboard while preserving the original simple UI direction.
- Magnetic cursor retained and expanded to cards, stats, buttons and links.
- Gaming-only news pipeline with relevance filtering and multiple gaming-focused RSS sources.
- Gaming Radar combining fresh news, upcoming releases and offers.
- Popular / rising games view based on observable activity signals (not game quality).
- Searchable game discovery.
- Per-game intelligence modal with platforms, release records, related news, official links and historical price snapshots.
- Keyless Steam specials collector for public deal discovery.
- Historical price snapshots (up to 180 points per store/region record).
- Upcoming-release countdowns only when an exact timestamp is actually supplied.
- Cross-source game identity normalization by title/developer fingerprint.

## Run
```bash
npm install
npm start
```
Then open `http://localhost:3000`.

Set `ADMIN_TOKEN` in `.env` for protected administrative collection endpoints. Collection is handled automatically by the server; there is no manual **Collect now** button.

## Data policy
The project uses public/authorized sources and provider adapters. It does not require consumer store passwords and does not bypass CAPTCHAs, authentication, paywalls or anti-bot controls.

Some console/store/subscription connectors still require an authorized/licensed provider endpoint. They are intentionally not faked as live APIs.

## News
The News tab is explicitly filtered for gaming relevance. Non-gaming stories are rejected before they enter the dashboard. Configure additional RSS feeds with `NEWS_RSS_FEEDS`; configured feeds are merged with the built-in gaming feeds.

## Price history
Historical price data accumulates after repeated collections. A brand-new installation will not have a historical-low graph until multiple price snapshots have been collected.


## v0.3.6 expanded upcoming discovery
The upcoming-release collector now checks multiple public release calendars: Nintendo Coming Soon, Gematsu Release Dates, GamesRadar, GameSpot, PlayStation Blog and Xbox Wire. It stores release precision (day/quarter/year) and never converts a year-only or quarter-only window into a fake exact timestamp.


## v0.3.7
Added live Top 50, Trending Games, and Top 50 Free-to-Play charts with sorting by rank, current players, peak, 24h change, and title.


## v0.3.8 — Cross-source Game Activity Engine
Builds an activity record for every game currently known to the platform. It combines available Steam live-player/trending signals with Google Trends, gaming-news mentions, store offers, and upcoming-release signals. Missing source data remains explicitly unavailable rather than being invented. `/api/activity` exposes coverage and sortable activity records.


## v0.3.9 Popular Free/Discounted Games
Adds a cross-source Popular Free/Deals view. It filters all currently collected game records to active free or discounted offers and sorts them by observable activity, live players, discount percentage, or title. Coverage is limited to offers successfully collected from configured sources.


## v0.4.0
- Removed the Search Trends dashboard tab.
- Kept trend signals available internally for activity scoring.
- Restored a dedicated Top 50 Games view.
- Top 50 collection prefers the official Steam most-played chart and falls back to SteamCharts Top Games when the public Steam page does not expose the full table.
- Added sorting controls for Top 50 and Trending Games.
- Expanded upcoming discovery with the current PlayStation upcoming-games page.
- Upcoming discovery remains multi-source rather than claiming universal coverage.


### v0.4.2
- Expanded Trending Games from the 5-item SteamCharts Trending block to a 50-game observable list.
- Preserves official SteamCharts 24h movement when available and fills remaining slots from high-current-activity games.

## v0.5.0 cross-platform expansion
- Adds keyless public-page collectors for PlayStation Store deals, Nintendo eShop sales/deals, GOG discounted games, Ubisoft Store deals, Epic free games, and Steam specials.
- Adds active sale-event detection and `/api/sales`.
- Expands persisted game/offer/release visibility so the UI is not artificially limited to ~100 records.
- Platform collectors remain source-limited: the system only stores information exposed by permitted public/official pages or configured authorized APIs.

## v0.5.0 cross-platform expansion
- Adds keyless public-page collectors for PlayStation Store deals, Nintendo eShop sales/deals, GOG discounted games, Ubisoft Store deals, Epic free games, and Steam specials.
- Adds active sale-event detection and `/api/sales`.
- Expands persisted game/offer/release visibility so the UI is not artificially limited to ~100 records.
- Platform collectors remain source-limited: the system only stores information exposed by permitted public/official pages or configured authorized APIs.

## v0.5.0 cross-platform expansion
- Adds keyless public-page collectors for PlayStation Store, Nintendo eShop, GOG, Ubisoft Store, Xbox catalog, Battle.net, Google Play Games, Apple App Store Games, EA Games, Epic free games, and Steam specials.
- Adds active sale-event detection and `/api/sales`.
- Expands game/offer/release visibility to thousands of records instead of the previous ~100-record snapshot limits.
- Keeps authorized Microsoft/marketplace connectors for data that requires approved access.
- Public collectors only use permitted official/public pages and do not bypass authentication, CAPTCHAs, paywalls, or access controls.


## v0.5.1
- Removed the manual Collect now button from the public dashboard.
- Automatic/background collection remains enabled.
- Protected admin collection endpoint remains available for server-side administration.

## v0.5.2 image coverage fix
- Preserves previously known non-empty artwork instead of overwriting it with blank image fields.
- Adds Steam header-art resolution from public Steam app URLs for chart/deal games.
- Extracts page artwork from platform release/deal cards when an image is exposed.
- Adds graceful broken-image fallback in the dashboard.

## v0.5.3 chart reliability
Top 50 now combines the first two SteamCharts pages (25 + 25) and never replaces a valid chart with an empty collection response. Steam HTTP requests use a browser-like User-Agent and standard Accept/Language headers.

## v0.5.4 UI cleanup
- Reworked the public dashboard spacing, card grid, navigation, stats, sale-event layout, chart cards, and mobile breakpoints.
- Reduced visual movement from the magnetic cursor so cards and stats no longer shift around the page.
- Chart cards now render available artwork/store images instead of plain text-only cards.
- Improved artwork fallbacks and removed stale Source Health wording from empty states.

## v0.5.5 image reliability
- Adds multiple Steam artwork fallbacks for chart games.
- Preserves and merges image candidate URLs instead of replacing them.
- Adds browser fallback cycling with referrer suppression for hotlink-sensitive CDNs.
- Handles lazy-loaded artwork attributes from release pages.
- Broken artwork becomes a clean placeholder instead of a broken/blank card.

- v0.5.5 additionally propagates artwork candidates through cross-platform/provider collectors and uses a consistent 16:9 art frame to reduce distorted artwork.

## v0.5.5 image reliability
- Multiple artwork candidates and browser fallback cycling.
- Cross-platform collectors preserve candidate artwork URLs.
- Steam chart artwork has three CDN fallbacks.
- Lazy-loaded release-page artwork attributes are recognized.
- 16:9 artwork frame reduces visible distortion.


## v0.5.6
- Removed the Free Top 50 dashboard tab and its stats tile.
- Free Games and Popular Free/Deals remain available.

## v0.5.7
Fixed a startup regression where `src/collectors/index.js` imported `collectSteam` from `steam.js`, but `steam.js` incorrectly exported `collectSteamDeals`. Restored the Steam upcoming collector and preserved artwork candidate handling.

## v0.6.0 Master Cross-Platform Game Catalog

v0.6.0 changes the data model from a small dashboard snapshot to an incremental master catalog. Each normalized game can hold multiple platform records, official store links, platform-specific product IDs, pricing/discount observations, artwork candidates, and release observations. The `Games` view is now a paginated master catalog.

Catalog adapters included in this build:
- Steam IStoreService full catalog when `STEAM_WEB_API_KEY` is configured; otherwise an incremental public Steam Store search fallback.
- PlayStation Store India PS5 and PS4 catalog pages.
- Xbox Browse All Games incremental catalog pages.
- GOG All Games incremental catalog pages.
- Ubisoft Store Games incremental catalog pages.
- Epic Games Store browse pages where the public HTML exposes product cards.
- Existing public/authorized collectors continue to feed the same master game identity.

The catalog index advances its page/cursor on each background collection instead of attempting to download every page in one request. This prevents a large catalog from blocking the entire collector loop. Set `CATALOG_PAGES_PER_RUN` or the platform-specific overrides to control the indexing rate.

`GET /api/catalog` returns master-catalog totals and platform coverage. `GET /api/games?page=1&pageSize=100&platform=Steam&q=elden` provides paginated catalog records.

Not every platform exposes a complete unrestricted public catalog API. Where an authorized API/provider is required, the provider connector remains available and is merged into the same catalog rather than inventing missing data.

## v0.6.1 — Live Sale Events
- Added an automatic official sale-event collector.
- Detects active Steam seasonal sale pages (Spring, Summer, Autumn, Winter).
- Stores verified start/end dates and exposes only currently active events in the dashboard.
- Sales & Deals shows a LIVE badge and links to the official sale page.
- This architecture can be extended with official sale pages for other platforms without inventing sale status.


## v0.6.2 Free-offer verification
- Tightened free-game detection so unrelated page text containing the word 'free' cannot classify a paid game as free.
- Requires explicit free-price/badge signals for generic cross-platform pages.
- Sanitizes persisted invalid free offers on startup: paid offers are reclassified as sales when discounted, otherwise removed from the free-offer set.
