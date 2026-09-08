# verbum-content

Public-domain scripture and study files for [Verbum Study](https://github.com/Creditch/bible-app).

This repository holds **GitHub Release assets only**. There is no app source here and no server. The running app downloads optional translation packs, `study.sqlite`, and Learn course packs over HTTPS, verifies SHA-256 from `content-manifest.json`, and attaches them on-device.

## Release layout

Each `packs-YYYY-MM-DD` release contains:

- `core.sqlite` — bundled at app build time (BSB, KJV, WEB, plus shared books / Strong's / original-language tables)
- one `{ABBREV}.sqlite` per additional public-domain translation
- `study.sqlite` — optional catechism / commentary / confession / dictionary corpus
- `learn-grc.sqlite` / `learn-hbo.sqlite` — Koine Greek and Biblical Hebrew courses (`kind: learn`)
- `content-manifest.json` — id, kind, URL, size, sha256, content version, core schema version, and `learnSchemaVersion` on Learn entries

Current latest tag: **`packs-2026-09-04`**. Learn course `content_version` on that tag is **`2026.09.08-units-1-8`** (Units 1–8 of both languages). Audio packs (`learn-audio-grc` / `learn-audio-hbo`) are not published yet.

Ingest stays in the private `bible-app-ingest` pipeline. Do not put USFM sources or ingest code here. Licensed ESV/CSB/NIV stay out of this repo.

## Fetching core for a local app build

From the bible-app checkout:

```
make fetch-db TAG=packs-2026-09-04
make fetch-study TAG=packs-2026-09-04
```

The running app fetches `releases/latest/download/content-manifest.json`. Do not cut a new latest tag that omits `core.sqlite`. Learn-only updates clobber `learn-*.sqlite` and `content-manifest.json` on the current latest tag.
