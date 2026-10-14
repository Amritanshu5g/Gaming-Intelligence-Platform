# v0.3.3 Upcoming Discovery Audit

## Implemented
- Added a key-free upcoming-game discovery collector.
- Uses public official announcement pages for PlayStation Blog, Xbox Wire, Nintendo News, and EA Press Releases.
- Keeps Steam upcoming discovery, which does not require a Steam Web API key.
- Supports additional permitted public pages through `UPCOMING_SOURCES`.
- Stores discovered games and release records in the existing database.
- Attempts to extract explicit calendar dates from release/launch/coming language.
- Never invents an exact release time; `releaseTimeKnown` remains false.
- Marks official announcement discoveries with source and confidence metadata.

## Verification
- JavaScript syntax check: PASS for new and modified collector files.
- Package version bumped to 0.3.3.

## Environment limitation
- Full live collection could not be executed in this build environment because npm dependencies (including Cheerio) are not installed locally. Run `npm install` on the target Windows machine before testing the collector live.

## Important limitation
This is a discovery layer based on public official pages. It is not a private Store API and should not be treated as a complete catalog. Page layouts can change, so source adapters should be monitored and updated when necessary.
