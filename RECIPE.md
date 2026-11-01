# obsmage-corwin — Corwin's recipe (AVALON, GIZA)

This is one person's rig, built on [inputloop/obsmage](https://github.com/inputloop/obsmage)
(founding commit `bfc62d9`). The generic tree knows nothing about these screens, these cameras or
these scenes. This repository is where they live.

## Layout

| Path | What |
|---|---|
| `STAGES.md` | Roll-up of every **profile** atom (video, output, audio, services); as of 2026-11-01 only the GSUS Tech profile, now with its `service.json` and `streamEncoder.json` (14 more profiles sit on Avalon, not yet split) |
| `SCENES.md` | Roll-up of every **scene-collection** atom (the 2024 Avalon collection and the active MISC_MULTI_POINT_RECORDING) |
| `atoms/` | The atoms both roll-ups come from (`omg_atoms.py split`) |
| `hosts/avalon/` | Avalon's display audits, the physical layout inferred from the hand-made Screenmap, and `dry-run-2026-11-01.md` (what a read-only run against the live folder showed) |
| `TEST-CARD.md` | The Windows commands to test the tools on Avalon, what each prints, how to undo |
| `hosts/giza/` | GIZA: waiting on what GIZA is now (see the questions there) |
| `journal/YYYY/MM/DD/` | Why things changed |

Credentials (Twitch token and refresh token, websocket secret and salt, any stream key) are
`secret`-class atoms. In git they show only as `@secret(len=N)`. Their values live in OBS's own
profile on Avalon and in `.omg/vault.kv` there (git-ignored, mode 600). This repository is private
by default, and it still carries no credential.

## The two-roll-up seam

`STAGES.md` and `SCENES.md` are both editable. Edit a block, then:

```sh
python3 ../obsmage/tools/omg_atoms.py unroll STAGES.md atoms/basic/profiles
python3 ../obsmage/tools/omg_atoms.py unroll SCENES.md atoms/basic/scenes
python3 ../obsmage/tools/omg_atoms.py join atoms "$APPDATA/obs-studio" --vault .omg/vault.kv   # on Avalon, with OBS closed
```

If both the atoms and the roll-up changed since the pin, unroll stops, names the clash and writes
nothing. Git is the transport on Avalon and GIZA. Forge runners (GitHub, Forgejo, inputloop's own)
run the same commands headless; secret atoms never leave the host, so a runner can roll up and check
but never join a live profile.

## Raised by the instrument (not acted on; yours to judge)

From `hosts/avalon/audit-*.txt`, 2026-11-01:

1. **Active collection: two sources share one monitor that their names say are different.**
   "Upper (Left Upper)" and "Display Capture - USAB01" are both bound to `…AMX1100…UID8448`.
   USAB01 reads like the USB display (it used to be index 4).
2. **Three sources share `…UID256`:** "DC_Center - slice", "USB LH_03 (left upper square)",
   "Upoper Right". The slice may be a deliberate crop; LH_03 on the centre display looks doubtful.
3. **Still bound by index:** "USB LH_01" (5) and "USB LH_01 - Left Upper (tall)" (6). They will
   drift on the next re-plug. `omg_compose.py compose` would add their stable ids once the
   current display list is captured on Avalon (`omg_compose.py displays` there).
4. **Unbound:** "Display Capture 4" (OBS reads that as monitor 0).
5. The 2024 Avalon collection has 8 index-bound, 3 id-bound and 1 unbound capture. It is the
   older shape; the active collection has already moved most of the way to stable ids.

## Next on Avalon (needs the Windows side: `TEST-CARD.md` has the steps in order)

```sh
python tools/omg_compose.py displays > hosts/avalon/displays-live.json        # real geometry and ids
python tools/omg_compose.py audit  "%APPDATA%/obs-studio/basic/scenes/MISC_MULTI_POINT_RECORDING.json" --displays hosts/avalon/displays-live.json
python tools/omg_compose.py compose "%APPDATA%/obs-studio/basic/scenes/MISC_MULTI_POINT_RECORDING.json" --displays hosts/avalon/displays-live.json --out composed.json
```

`compose` without `--write` changes nothing. Read its report, then decide.

Copyright 2026 INPUTLOOP; CC-BY-SA-4.0.
Mentat (for Corwin; claude-opus-5-5)
