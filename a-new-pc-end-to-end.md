# A New PC, End to End

Everything so far converges here. A new Windows PC normally
means an afternoon of browser tabs, downloads and wizards.
With winget, the same job is: describe the old machine, carry
one small file across, replay it. Allow fifteen unhurried
minutes, most of them spent watching progress bars.

## Step 1: describe the old machine

On the PC being replaced:

```powershell
winget export -o C:\Users\you\Desktop\my-apps.json
```

winget examines what is installed, matches programs against
its sources, and writes a JSON file listing the matches:
which source each came from, and each package's ID. One
option changes the file's meaning:

- Plain `export` records *which* programs, not which
  versions. The new machine gets each program's current
  version — usually what you want on moving day.
- `export --include-versions` pins the recorded versions
  into the file, for a machine that must be reproduced
  exactly, quirks and all.

Expect a warning or two: export will tell you about installed
programs it could not match to any source. Those are manual
installs on the new machine — typically a handful, typically
the oldest and oddest ones. Note them; there is no wing under
winget for a program no catalogue knows.

The file itself is plain text, and reading it is instructive.
It has a `Sources` list, and under each, `Packages` with a
`PackageIdentifier` per program:

```json
{
  "Sources": [
    {
      "Packages": [
        { "PackageIdentifier": "Mozilla.Firefox" },
        { "PackageIdentifier": "Git.Git" },
        { "PackageIdentifier": "7zip.7zip" }
      ]
    }
  ]
}
```

Edit it freely before the move: delete the programs you never
actually used (moving day is the best audit your software
list will ever get), and this file's *shape* is also how you
would write a standard setup file by hand for any machine —
yours, a family member's, a fresh work laptop.

## Step 2: set up the new machine

Copy `my-apps.json` over — USB stick, cloud folder, email to
yourself, it is a few kilobytes. Then, on the new PC:

1. Sign in and let Windows finish its own first-run work.
   Update App Installer through the Microsoft Store if
   prompted, then confirm `winget --version` answers
   (chapter 3 covers the one registration fix a brand-new
   account sometimes needs).
2. Accept the source agreements once, interactively, so you
   have genuinely seen them:

   ```powershell
   winget source list
   ```

3. Replay the file:

   ```powershell
   winget import -i C:\path\to\my-apps.json --accept-package-agreements --accept-source-agreements
   ```

`import` installs the listed packages one by one, each with
the full ceremony of chapter 5: download from the maker,
hash check, silent install. Programs already present are
reported and skipped, not reinstalled. Options worth knowing:

- `--ignore-unavailable` — carry on past any package that
  cannot be found, rather than stopping the whole replay.
  Almost always right for a move.
- `--ignore-versions` — if the file pins versions, take the
  current ones instead.
- `--no-upgrade` — leave anything already installed at its
  existing version rather than bringing it up to date.

## Step 3: finish the edges

- Install the unmatched programs export warned you about,
  from their makers, by hand — the honest residue.
- Sign in to the programs that need it. winget moves
  software, not accounts, settings, browser profiles or
  documents; your files still travel the usual way (backup,
  cloud sync, migration tool).
- Re-apply your pins (chapter 6) and settings (chapter 9):
  neither travels inside the export file, so keep a copy of
  your `settings.json` with it if you customised one.
- Finish with the new machine's first full report:
  `winget list`. Compare it against the old machine's list;
  they should agree except for the deliberate edits.

That is the capstone because it uses everything: a source you
trust, IDs you can read, silent installs with agreements
accepted in advance, and a mismatch list handled honestly
rather than silently. A text file you can read, diff and keep
in version control is now the difference between "a PC like
my old one" and *this* PC, set up *this* way — and that file,
not any backup image, is the part worth keeping.
