# Pending fix: study pack checksum (found 2026-09-24)

The live `content-manifest.json` on `packs-2026-09-04` (generated
2026-09-09T05:25Z) describes a `study.sqlite` that was never uploaded:

| | manifest | published asset (uploaded 2026-09-04T22:41Z) |
|---|---|---|
| sizeBytes | 169,635,840 | 183,156,736 |
| sha256 | `a176ad82f505…` | `d92d0929e030…` |

`ContentPackStore.verifyChecksum` rejects the download, so **every Study
install and update since 2026-09-09 fails** with `checksumMismatch`. The
other 46 entries match their assets.

The published asset is sound. It passes the app's own
`StudyDatabase.validateContent`: integrity ok, no foreign-key violations,
32 works, none empty, no invalid anchors. The fix is therefore the two
fields in this directory's `content-manifest.json`. Nothing else in it
differs from the live file except `generatedAt`. No asset is re-uploaded.

From a machine logged in as Creditch:

```
gh release upload packs-2026-09-04 pending-study-manifest/content-manifest.json \
  --repo Creditch/verbum-content --clobber
```

Then, in `bible-app-ingest`:

```
python -m src.ingest.verify_release     # must print "all 47 manifest entries match"
```

and delete this directory.
