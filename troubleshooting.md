# Troubleshooting

When winget misbehaves, it usually leaves evidence. Work in
this order: what did the command print, what do the logs say,
and which of the four moving parts from chapter 2 is actually
at fault?

## Start with the logs

Every winget run writes a log. Find them with:

```powershell
winget --info
```

which prints the **DiagOutputDir** path — by default under
App Installer's LocalState folder — or open the folder
directly with `winget --logs`. Logs are named by date and are
kept about a week (128 MB in total, 16 MB per file, by
default). For a failure you are actively chasing, reproduce it
with more detail captured:

```powershell
winget install --id Some.Package -e --verbose-logs
```

`--verbose-logs` (also `--verbose`) writes the fullest logs;
`--logs`/`--open-logs` just open the folder. The settings file
(chapter 9) can raise the standing level under `logging` while
you investigate.

Error codes mean something specific. If an installer fails
with a bare number — the classic is 1603, an MSI's generic
"something went wrong" — ask winget to translate:

```powershell
winget error 1603
```

## "No applicable installer found"

The package exists, but nothing in its manifest fits your
machine: wrong architecture (an x64-only program on an ARM
PC), or your scope/installer-type preferences exclude every
build it offers. Check `winget show --id … -e` for what
installers exist, loosen a preference, or accept this program
is not for this machine.

## Hash mismatch

The download completed, but its SHA-256 fingerprint does not
match the manifest, so winget stops. Causes, in order of
likelihood:

1. **The vendor replaced the file in place** — re-released
   the same version with a small fix, or their download now
   serves a slightly different build. The manifest catches up
   once a contributor or Microsoft's automation re-records
   the hash, usually within a day or so. Waiting is the fix.
2. **A stale or partial download.** Clear it out and retry;
   also try `winget source update` in case your cached
   catalogue is the stale half of the disagreement.
3. **The wrong file entirely** — a vendor's site redirecting
   the "download" to an error page or a different product.

What not to do: `--ignore-security-hash` (chapter 5) makes
the install proceed unverified. It exists for moments when
you have *independently* confirmed the file is right — for
example, by downloading it from the vendor yourself and
checking it with `winget hash installer.exe`, which prints a
file's SHA-256 so you can compare it against the manifest's
or the vendor's published value. As a standing habit it
removes the one check that makes catalogue-based installing
safe.

## Installs that fail, stall or demand unexpected prompts

- **Exit codes** in the output are the installer's own;
  `winget error <code>` translates the known ones, and the
  log records the installer's command line if you need to run
  it by hand and watch it complain directly.
- **A 403 Forbidden on download** usually means the vendor's
  server is refusing winget's user-agent (Microsoft documents
  the exact agent string winget sends). The vendor's own
  download page is the workaround; winget cannot disguise
  itself, and arguably should not.
- **A UAC prompt where you expected silence** — chapter 5's
  scope caveat: EXE installers in particular decide for
  themselves. Machine scope, or an administrator account,
  changes the answer. Not a fault.
- **"The package is pinned"** during an upgrade — not a fault
  either; chapter 6. Change the pin or upgrade with intent.
- **Something else is installing.** Windows installer
  machinery serialises: an in-progress Windows Update or
  another install can make winget queue or fail. Wait, retry.

## winget itself is broken

If the command errors before doing anything, or vanishes
from a machine that had it: update App Installer from the
Store first (chapter 3), then try the documented repair,
which reinstalls the package manager machinery through
PowerShell:

```powershell
Install-PackageProvider -Name NuGet -Force
Install-Module -Name Microsoft.WinGet.Client -Force -Repository PSGallery
Repair-WinGetPackageManager -Force -Latest
```

That module, `Microsoft.WinGet.Client`, is also Microsoft's
supported route for the contexts winget-the-command declines
— notably scripts running as SYSTEM — and offers cmdlets
(`Find-WinGetPackage`, `Install-WinGetPackage` and friends)
for driving the same sources from PowerShell.

## When to stop troubleshooting

If the logs point at the vendor's server, a hash that does
not yet match a re-released file, or an installer that fails
identically when run by hand, the problem is no longer
winget's. Install the program manually from the maker, run
`winget list` afterwards to confirm Windows registered it,
and let winget pick the program up from there — most
well-behaved programs become manageable mid-life, even if
they did not arrive by winget's road.
