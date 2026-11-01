# Test card: obsmage on Avalon

For Corwin, 2026-11-01. Everything here reads, except where it says it writes, and the only files
it writes are new ones named in the step. **Nothing in `%APPDATA%\obs-studio` is changed by any
step.** Use `cmd.exe` (in msys2 write the paths with `/c/...` and `$APPDATA`).

Observed so far: both tools pass their tests under Python 3.8 on Linux, and they ran against your
live OBS folder through the mount (`hosts/avalon/dry-run-2026-11-01.md`). Not observed: any of
this on Windows itself. Step 4 is the first time the Windows code runs.

## 0. Get the code (there are no clones on Avalon yet)

I put two git bundles in `F:\claude\projects\_omg-drop\`. A bundle is a repository in one file.

    cd /d F:\claude\projects
    git clone -b main _omg-drop\obsmage.bundle obsmage
    git clone -b main _omg-drop\obsmage-corwin.bundle obsmage-corwin

Prints `Cloning into 'obsmage'...` and the same for `obsmage-corwin`. If your GitHub login works
in git, this is the same thing and keeps `origin` right:
`git clone https://github.com/inputloop/obsmage.git` (and `obsmage-corwin`). With the bundles, point
`origin` at GitHub afterwards: `git -C obsmage remote set-url origin https://github.com/inputloop/obsmage.git`
(same for `obsmage-corwin`).

## 1. Python 3.8

    set PY=C:\Users\corwi\AppData\Local\Programs\Python\Python38-32\python.exe
    %PY% --version

Prints `Python 3.8.x` (32-bit; a newer one from `py` or Python312 also works, 3.8 is the floor).

## 2. The tests

    cd /d F:\claude\projects\obsmage
    %PY% -W ignore -m unittest discover -s tests

Should end `Ran 33 tests` and `OK`. (The shell suites `tests\e2e*.sh` need a POSIX shell; run them
from msys2 if you want them. They are not part of this card.) If a test fails, send me the last
20 lines: Windows is where a failure would be news.

## 3. Check your live OBS folder is lossless (reads only)

    %PY% tools\omg_atoms.py verify "%APPDATA%\obs-studio"

Should print one line: `verify: ok, lossless and no secret in the atoms`. About half a minute.
It splits into a temporary folder, joins back, compares byte for byte, and deletes the temporary
folder (the credentials vault in it is mode-locked to you with `icacls`; if that fails it prints a
`warning:` line, and the folder is still temporary). OBS may stay open; if it names a `MISMATCH`
for a file OBS was writing at that moment, close OBS and run it again.

## 4. The one step that needs Windows: ask Windows which screens you have

    cd /d F:\claude\projects\obsmage
    %PY% tools\omg_compose.py displays --out ..\obsmage-corwin\hosts\avalon\displays-live.json

Should print `Wrote ...displays-live.json (N display(s))`, with N the number of monitors Windows
shows now. Open the file in a text editor. For each display look for:

- `id` like `\\?\DISPLAY#AMX1100#5&2ebfd20c&0&UID8448#{e6f07b5f-...}`. This is the stable id OBS
  stores. If it is `null`, tell me which display and what `unknown.id` says.
- `x`, `y`, `w`, `h` match Settings > System > Display (full pixels, not scaled).
- Exactly one has `"primary": true`.

If it fails with a Python error, send me the whole text; this is the code nobody has run yet.

## 5. Audit the active collection against the real screens (reads only)

    %PY% tools\omg_compose.py audit "%APPDATA%\obs-studio\basic\scenes\MISC_MULTI_POINT_RECORDING.json" --displays ..\obsmage-corwin\hosts\avalon\displays-live.json

Should print 14 lines like `'DC_Left' [monitor_capture] is bound by id ... resolves to display #2 ...`,
then `Displays no source captures:`. The old dry run said "no current display" for most lines,
because it used a guessed list. With the real list, lines that still say "no current display" are
sources whose screen is not plugged in (or whose id changed), and that is worth knowing before
the next stream. The five points in `RECIPE.md` ("Raised by the instrument") should now be
checkable against it.

## 6. See what composing would do (writes one new file, in your temp folder)

    %PY% tools\omg_compose.py compose "%APPDATA%\obs-studio\basic\scenes\MISC_MULTI_POINT_RECORDING.json" --displays ..\obsmage-corwin\hosts\avalon\displays-live.json --out "%TEMP%\composed-misc.json"

Prints a report in words, one line per decision (`Bound ... by stable id`, `Created source ...`,
`Hid item ... Not deleted`, `Added item ...`) and last `Wrote ...composed-misc.json`. The live
collection is untouched. There is no `--write` in this card on purpose.

## 7. Look at it in OBS (this is the part to judge by eye)

1. In OBS: Scene Collection > Import. Pick `%TEMP%\composed-misc.json`. If the dialog lets you
   name it, call it `MISC composed test` (I have not seen that dialog on Avalon; if it wants the
   same name as your live collection, cancel and tell me).
2. Scene Collection > `MISC composed test`.
3. Open the `Screenmap` scene and `Mini Screenmap`. Look for: every plugged-in screen shown once,
   placed in the same left-to-right and up-down arrangement as on your desk; sources that used to
   say "index" now also carry the stable id; items for unplugged screens hidden, not deleted.
4. Click a few display sources and check each one shows the screen its name claims.

Good result: the layout matches the desk and no screen shows the wrong content. Bad result: any
source showing the wrong screen. Tell me the source name and the screen you expected.

## Undo

- Scene Collection > `MISC composed test` > switch back to your usual collection, then
  Scene Collection > Remove (pick the test one). Your own collection was never edited.
- Delete `%TEMP%\composed-misc.json`.
- To remove the code: delete `F:\claude\projects\obsmage`, `F:\claude\projects\obsmage-corwin`
  and `F:\claude\projects\_omg-drop`. The tools install nothing and set no registry keys.

## What this card does not test

The OBS plugin (`obsmage-core`) is Linux-only so far; it loaded in OBS on gw33
(`docs/REQUIREMENTS.md` in obsmage) and has no Windows build yet. Writing back to your live OBS
folder (`join`, `compose --write`) is left for after steps 4 to 7 look right.

Copyright 2026 INPUTLOOP; CC-BY-SA-4.0.
Mentat (for Corwin, claude-sonnet-5-5)
