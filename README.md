# DMS Release Feed (Public)

This repository hosts the public release metadata feed for DMS OS.

It serves two purposes:
- Machine-readable JSON endpoints for backend polling.
- A simple human-readable release portal on GitHub Pages.

Pages base URL:
- `https://seascapesubsea.github.io/dms-release-feed/`

## Feed Schema v1

Core compatibility contract:
- `latest.json` must contain a top-level `latest` object.
- `latest` must expose either `version` or `tag` (both preferred).
- `latest.file` must point to a valid per-release JSON file.
- Each per-release JSON file must contain `changelog` (array of strings preferred).
- `release_url` should be present whenever available (can be an empty string when not set).

Current product key:
- `product: "dms-os"`

## Endpoints

Canonical endpoints:
- `https://seascapesubsea.github.io/dms-release-feed/latest.json`
- `https://seascapesubsea.github.io/dms-release-feed/releases/index.json`
- `https://seascapesubsea.github.io/dms-release-feed/releases/v0.0.0-bootstrap.json`
- `https://seascapesubsea.github.io/dms-release-feed/` (portal page)

## Update Flow

The private DMS release workflow is responsible for updating:
- `latest.json`
- `releases/index.json`
- `releases/<tag>.json`

When publishing a new release:
1. Write the new `releases/<tag>.json` file.
2. Update `releases/index.json` to include it.
3. Update `latest.json` so `latest.file` points to the new release file.

Important invariant:
- `latest.file` must always resolve to a valid JSON release file.

## GitHub Pages

Expected Pages configuration:
- Source branch: `main`
- Source folder: `/` (repository root)

With this setup, GitHub Pages serves both the JSON feed and the portal page from the same repo.
