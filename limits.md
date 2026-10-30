# Limits

winget is good at its job. Its job is narrower than "software
on Windows", and this chapter collects the boundaries in one
place so none of them surprises you later.

## What winget manages — and what it does not

winget installs, upgrades and removes *packages it can
identify*. That means programs whose installs registered
properly with Windows and which a source's catalogue can
describe. Outside that fence:

- **Programs installed by unzip-and-run** outside winget —
  no registration, no catalogue entry — are invisible to
  `list`, untouched by `upgrade`, and unremovable by
  `uninstall`. Portable software is only managed when winget
  itself installed it as a portable package.
- **Settings, data and accounts do not travel.** Export and
  import move the programs, not their configuration, browser
  profiles, documents or licences tied to a person.
- **Drivers, Windows itself, and firmware** are other
  systems' jobs: Windows Update, your PC maker's tools.
  winget is not an operating-system patch tool, and a fully
  winget-updated machine can still be a Windows update behind.
- **Nothing can be bought.** Paid Microsoft Store content
  must be purchased through the Store first; winget installs
  against a licence you already hold.

## Version and catalogue honesty

The catalogue is maintained by humans and automation, and it
lags reality. A vendor can ship version N+1 today while the
manifest still describes N — `winget upgrade` will honestly
report nothing available, because as far as its source knows,
nothing is. The reverse failure also exists: a vendor quietly
replaces an installer file without changing the version
number, the recorded hash no longer matches, and chapter 13's
hash-mismatch dance begins. Neither is a scandal; both are
the cost of a catalogue of fingerprints maintained in public.

Versions reported by old installers can also be simply wrong
or absent, which is why `upgrade --include-unknown` exists
and why its results deserve a glance afterwards.

## Scope and installer behaviour are not fully winget's call

Chapter 5's caveats collect here: whether `--scope user` is
honoured depends on the installer family — MSIX reliably,
MSI usually, EXE inconsistently — and a user-scope install can
still demand a UAC prompt. Silent installs are likewise a
request the installer can honour badly: most are silent
because their manifests carry the right switches, and the
occasional one will still flash a wizard or a checkbox page.
winget reports what happened; it cannot make a rude installer
polite.

## Pins restrain winget, not the program

Repeated from chapter 6 because it bites people: a pinned
program with its own built-in updater can upgrade itself
anyway. winget will report the new version next time it
looks, wearing the expression of a tool that did its part.

## Running contexts

winget is a per-user command-line tool for interactive use.
It is deliberately not supported in the **SYSTEM** context,
which rules out some remote-management and imaging workflows;
Microsoft's answer there is the `Microsoft.WinGet.Client`
PowerShell module. Likewise, on Windows Server it arrives
only with Server 2025; older servers are Chocolatey country.

And the meta-limit, stated in the [criteria](criteria.md):
winget cannot be demonstrated on this guide's own lab
machine, which runs Linux. Everything here is taught from
Microsoft's documentation and the public catalogue, checked
as carefully as that allows — but it is documentation-checked
teaching, not lab-demonstrated teaching, and the guide would
rather say so than pretend otherwise.
