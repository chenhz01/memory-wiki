# Changelog

## [0.2.0] - 2026-09-16

- Added `fresh`: freshness report classifying entries as fresh / stale / rotten / undated (exit 1 when anything is rotten)
- Added `refresh`: stamps `last-verified:` and closes the re-verification loop; effective date = last verification, not birth
- Index now shows a last-verified column
- Acceptance run: 4-quadrant fixture (fresh/stale/rotten/undated) → refresh → re-scan behaved as specified

## [0.1.0] - 2026-09-16

- Initial release: single-file memory_wiki.py (ingest / index / query / lint / log), zero dependencies
- Acceptance run: 5-step fixture (ingest, orphan injection, query ranking, lint FAIL/WARN, index-rebuild recovery) behaved as specified
