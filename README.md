# verbum-content

Public-domain scripture and study files for [Verbum Study](https://github.com/Creditch/bible-app).

This repository holds **GitHub Release assets only**. There is no app source here and no server. The running app downloads optional translation packs, `study.sqlite`, and Learn course packs over HTTPS, verifies SHA-256 from `content-manifest.json`, and attaches them on-device.

## Release layout

The app reads one file: `releases/latest/download/content-manifest.json`. Each entry gives an id, kind, URL, size, sha256, content version, core schema version, and `learnSchemaVersion` on Learn entries. An entry's URL can point at any release, so files stay where they were first published.

- **`packs-2026-09-04`** is the GitHub latest release. It holds the live `content-manifest.json`, plus the translation, atlas and lexicon packs that have not changed since (YLT, GNV, SVV, SYN and others).
- **`content-2026-10-08`** holds `core.sqlite`, `study.sqlite`, the other translation packs, `learn-grc.sqlite` / `learn-hbo.sqlite` (`content_version` **`2026.10.08-units-1-8`**), and the `study-*.sqlite` commentary packs (`kind: study-work`).
- **`study-library-2026-10-01`** holds the first commentary pack build.

Audio packs (`learn-audio-grc` / `learn-audio-hbo`) are not published yet.

Ingest stays in the private `bible-app-ingest` pipeline. Do not put USFM sources or ingest code here. Licensed ESV/CSB/NIV stay out of this repo.

## Fetching core for a local app build

From the bible-app checkout:

```
make fetch-db       # content-2026-10-08, the Makefile's CONTENT_TAG
make fetch-study
```

Do not cut a new latest release without a `content-manifest.json`: the app would get a 404. To publish a pack, upload it to a release, add or update its manifest entry, upload the manifest to the latest release with `--clobber`, then run `python -m src.ingest.verify_release` in `bible-app-ingest`.
