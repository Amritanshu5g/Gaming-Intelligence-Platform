# v0.3.5 audit and fixes

## Static checks
- All JavaScript files: `node --check` PASS.
- Lightweight audit script: PASS.

## Tests
- Gaming-only article accepted: PASS.
- Movie/non-gaming article rejected: PASS.
- Game persistence: PASS.
- Price-history snapshot creation: PASS.
- Intelligence engine execution: PASS.

## Fixes found during v0.3.4 review
1. **Keyless collectors could be silently disabled.** Steam/Epic now default to enabled unless explicitly set to `false` in `.env`. This prevents a fresh install from showing zero games simply because `STEAM_ENABLED` / `EPIC_ENABLED` were omitted.
2. **Gaming news filter was too strict for known gaming-only feeds.** Known gaming-specific source URLs are now accepted when they contain no explicit non-gaming topic, while explicit movie/TV/politics/etc. signals are still rejected.
3. Added `scripts/audit.js` for repeatable local regression checks.
4. Bumped package version to 0.3.5.

## Remaining limitation
A full live HTTP collection could not be executed in the build environment because `npm install --no-audit --no-fund` timed out. External collectors therefore remain network-dependent and should be live-tested after installation on the user's machine.

## Security/behavior notes
- No provider credentials are generated or embedded.
- Exact release times are not inferred when the source only supplies a date.
- Consumer store passwords are not requested.
- Static CSP/security headers remain enabled.
