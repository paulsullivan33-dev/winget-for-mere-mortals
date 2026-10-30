# Verification notes — winget lab

This guide's lab is a Linux sandbox. winget is a Windows-only
tool delivered inside Microsoft's App Installer, so **no winget
command was run for this guide**. There are no transcripts,
because there is nothing to transcribe: inventing sample output
would be worse than having none.

Instead, every command name, option, settings key and behaviour
in the guide was checked against Microsoft's own documentation
on 2026-10-30, and every package ID used as an example was
checked against the real community repository. The sources:

## Microsoft Learn — Windows Package Manager docs

Base: https://learn.microsoft.com/en-us/windows/package-manager/

- `winget/` — the tool overview: command list, global options,
  supported installer formats, App Installer delivery, the
  Windows 10 1809 minimum, the first-login registration fix.
- `winget/install` — install usage, the full option table
  (scope, architecture, silent, exact, the two agreement
  options, `--ignore-security-hash`), multi-package installs,
  msstore product-code IDs, local manifests.
- `winget/upgrade` — upgrade usage, `--all`, `--include-unknown`,
  `--include-pinned`, `--uninstall-previous`.
- `winget/pinning` — the three pin types (Pinning, Blocking,
  Gating), `pin add/remove/list/reset`, `--blocking`,
  `--version` with wildcards such as `0.70.*`, `--installed`.
  (The en-US page refused one fetch; the content was read from
  the same page's search-index copy and cross-checked against
  the `upgrade` page's pin notes.)
- `winget/export` and `winget/import` — usage, options, and the
  JSON shape (Sources, Packages, PackageIdentifier, Version).
- `winget/source` — the three default sources with their real
  URLs and the `winget source list` sample output, the
  explicit/implicit distinction (winget-font is explicit by
  default), add/remove/reset needing administrator rights.
- `winget/settings` — the settings file behaviour and the key
  reference: `source.autoUpdateIntervalInMinutes`,
  `visual.progressBar` values, `telemetry.disable`,
  `installBehavior.preferences` (scope, locale, architectures,
  installerTypes), portable package roots, `logging`,
  `network.downloader`, `downloadBehavior`, admin settings via
  `--enable`/`--disable`.
- `winget/troubleshooting` — log location (DiagOutputDir),
  `--logs` / `--verbose-logs`, `winget --info`, the
  `winget error` lookup command, scope inconsistency of EXE
  installers, the 403 download block, repair through the
  Microsoft.WinGet.Client PowerShell module.

## Package IDs checked against microsoft/winget-pkgs

Checked through the GitHub API on 2026-10-30 — each of these
has a real manifest folder in the community repository:

- `Mozilla.Firefox` — manifests/m/Mozilla/Firefox (versions
  from 100.x onward present).
- `VideoLAN.VLC` — manifests/v/VideoLAN/VLC (3.0.x line and a
  Nightly folder present).
- `7zip.7zip` — manifests/7/7zip/7zip (versions to 26.x).

Further IDs appear in Microsoft's own documentation examples,
which is the check the guide relies on for them:

- `Microsoft.PowerToys` and `Git.Git` — the install and
  upgrade pages' own worked examples.
- `Microsoft.VisualStudioCode` — the settings page
  (`winget install Microsoft.VisualStudioCode`) and the
  multi-package install example.
- `Microsoft.PowerShell` — the multi-package install example
  and the pin documentation's worked example.

The Microsoft Store example ID `XP9KHM4BK9FZ7Q` in chapter 5
is the one Microsoft's install page itself uses to show that
msstore IDs are product codes, not names.

## What this lab did verify locally

- The MkDocs configuration parses as YAML, and every file
  named in its navigation exists in the checkout.
- The deploy workflow is byte-identical to the series
  reference (md5 5de4fbd078823c303e22ba9fc2cdfa76).
- The related guides linked from the README (PowerShell,
  Homebrew) exist in the series index.
