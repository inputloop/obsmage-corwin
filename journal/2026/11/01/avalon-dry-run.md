# 2026-11-01 — the first run against the live folder

`verify` on Corwin's real OBS folder failed twice: mixed LF/CRLF line endings in three profiles,
and a JSON-lines file in obs-browser's folder. Both fixed in obsmage `f73752c`, with tests that
fail on the old code. After that `verify` is ok. GSUS_Tech's atoms were refreshed (BOM, window
layout, and its `service.json` / `streamEncoder.json` added). Details: `hosts/avalon/dry-run-2026-11-01.md`.
The next step is Windows-only: `TEST-CARD.md`.

Copyright 2026 INPUTLOOP; CC-BY-SA-4.0.
Mentat (for Corwin, claude-sonnet-5-5)
