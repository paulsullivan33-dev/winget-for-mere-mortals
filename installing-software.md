# Installing Software

This is the chapter the whole guide hangs off. The basic act
is one line; the options around it — exact matching, silence,
scope, architecture — are what make it reliable enough to use
in scripts and on other people's machines.

## The plain install

```powershell
winget install Mozilla.Firefox
```

winget treats the argument as a *query*: it is matched,
ignoring capitals, against package names, IDs and monikers.
If exactly one package matches, it installs. If several do —
a name like "Firefox" matches the browser and its developer
and ESR editions — winget refuses to guess and lists the
candidates instead. That refusal is a feature: never let a
tool choose which program you meant.

## Pin the target down with IDs

Professional habit: install by ID, exactly.

```powershell
winget install --id Git.Git -e
```

- `--id` says "match the ID field", not the name.
- `-e` (`--exact`) requires the whole ID to match, exactly as
  written, capitals included. Without it, `--id Git` would
  happily match anything whose ID contains "Git".

Add `--source winget` if the same program also exists in the
Store and you want the community-catalogue copy (the
difference matters — chapter 11 explains it).

Microsoft Store apps are the exception to the pattern: they
have no name-like IDs at all, only product codes, and you
install them from the `msstore` source:

```powershell
winget install XP9KHM4BK9FZ7Q -s msstore
```

(that code is the one Microsoft's own documentation uses as
its example). Find a Store app's code on its Store page URL
or with `winget search --source msstore`.

## Quiet installs and consent prompts

By default winget runs installers with the silent switches
recorded in the manifest — no wizard, no clicking Next. Three
options adjust how much you are asked along the way:

- `-h` (`--silent`) — request the *most* silent mode the
  installer offers. Some installers show progress unless this
  is given.
- `-i` (`--interactive`) — the opposite: let the installer's
  wizard run normally. Occasionally useful when you want to
  change an install location the silent path would fix.
- Two kinds of agreement can appear. **Source agreements**
  are a catalogue's terms (the Microsoft Store source has
  them); `--accept-source-agreements` accepts them in
  advance. **Package agreements** are the program's own
  licence prompt; `--accept-package-agreements` accepts
  those. For a completely unattended install, scripts combine
  both with `-h`.

## Scope: for you, or for everyone

Windows installs programs either **per user** (into your own
folders, no admin rights) or **per machine** (into Program
Files, for every account, elevation required). Choose with:

```powershell
winget install --id Microsoft.PowerToys -e --scope user
winget install --id Microsoft.PowerToys -e --scope machine
```

Honest caveats, straight from Microsoft's documentation:
packages vary in what they support — MSIX packages respect
scope reliably, most MSI packages do, but many EXE installers
are inconsistent about it, and a user-scope install can still
pop a UAC prompt depending on the installer and whether your
account is an administrator. Set a default scope once in
settings (chapter 9) if you find yourself typing it often.

## Architecture, version, and location

- `--architecture` (short `-a`) picks `x64`, `x86` or `arm64`
  builds when several exist — mostly for pinning down a
  legacy program on an ARM machine, or vice versa.
- `--version` (short `-v`) installs a specific version
  instead of the newest: `winget install --id 7zip.7zip -e --version 24.09`.
  (`winget show --versions` lists what is on offer.)
- `--location` (short `-l`) suggests an install folder, for
  the installers that honour one.
- `--override` passes your own extra arguments to the
  installer, replacing the manifest's silent switches — a
  tool for the rare manifest whose defaults are wrong for
  you.

## Several at once, and the hash warning

One command can install a line of packages, one after
another:

```powershell
winget install Microsoft.VisualStudioCode Microsoft.PowerShell Git.Git
```

That is the seed of chapter 10's new-PC workflow.

Finally, the option to treat with respect:
`--ignore-security-hash`. Normally winget verifies the
downloaded installer against the manifest's SHA-256
fingerprint and *stops* if they differ. This option skips the
check. Microsoft does not recommend it, and neither does this
guide: a mismatch usually means the vendor quietly replaced
the file (common, mildly annoying) but it is also exactly
what a tampered download looks like. Chapter 13 explains what
to do instead — usually, wait a day for the manifest to catch
up, or get the program from the vendor yourself.
