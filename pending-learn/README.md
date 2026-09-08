# Pending Learn Units 1–8 publish

Validated packs are staged on private `Creditch/bible-app-ingest` release
`learn-2026-09-08` (`--latest=false`, so `make fetch-db` is unchanged).
The cloud agent cannot clobber this public repo's Release assets (403).

From a machine logged in as Creditch / Lead:

```
gh release download learn-2026-09-08 --repo Creditch/bible-app-ingest --dir /tmp/learn-ship
gh release upload packs-2026-09-04 \
  /tmp/learn-ship/learn-grc.sqlite \
  /tmp/learn-ship/learn-hbo.sqlite \
  /tmp/learn-ship/content-manifest.json \
  --repo Creditch/verbum-content --clobber
```

Do **not** `gh release create` a new date tag. `releases/latest` must keep
`core.sqlite`.

| Pack | `content_version` / manifest `version` | sha256 |
|---|---|---|
| `learn-grc` | `2026.09.08-units-1-8` | `d4cb769b9b456e4e43f105787afa04699b9ce5e49d0de44722821514cb6e317f` |
| `learn-hbo` | `2026.09.08-units-1-8` | `690964c85d88989258c6f8b2b9d2f055a95df787e0e8b988791d16d4e671e5b6` |

After upload, delete this `pending-learn/` directory (or leave it as the
checksum ledger). Audio packs stay unpublished.
