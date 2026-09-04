# verbum-content

Public-domain scripture and study files for [Verbum Study](https://github.com/Creditch/bible-app).

This repository holds **GitHub Release assets only**. There is no app source here and no server. The running app downloads optional translation packs and `study.sqlite` over HTTPS, verifies SHA-256 from `content-manifest.json`, and attaches them on-device.

## Release layout

Each `packs-YYYY-MM-DD` release contains:

- `core.sqlite` — bundled at app build time (BSB, KJV, WEB, plus shared books / Strong's / original-language tables)
- one `{ABBREV}.sqlite` per additional public-domain translation
- `study.sqlite` — optional catechism / commentary / confession / dictionary corpus
- `content-manifest.json` — id, kind, URL, size, sha256, content version, core schema version

Ingest stays in the private `bible-app-ingest` pipeline. Do not put USFM sources or ingest code here.

## Fetching core for a local app build

From the bible-app checkout:

```
make fetch-db TAG=packs-2026-09-04
make fetch-study TAG=packs-2026-09-04
```
