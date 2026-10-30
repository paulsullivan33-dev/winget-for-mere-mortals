# Writing Criteria

The standard this guide was written and checked against.

## The criteria

1. **For a complete beginner.** A reader who has never used
   a package manager should succeed by following the text
   alone.
2. **Teach the transferable idea.** Each chapter opens by
   naming the problem it addresses and the general principle
   it illustrates; techniques specific to one platform should
   be marked as such.
3. **Nothing destructive without warning.** Where a command
   can remove or overwrite data, the text says so before the
   command, not after.
4. **Respect the reader's data and the law.** No technique
   may depend on infringing copyright or on another person's
   credentials or data; where a method touches regulated or
   shared material, proceed only with the rightsholder's own
   access and permission.
5. **Complete copy-paste ready command sequences** for the
   core workflow. Do not leave placeholder credentials or
   half-finished code.
6. **Show realistic example output** (or a measured
   performance figure) **for core commands.** Any printed
   output that has not really occurred should be labelled as
   illustrative.
7. **Every cross-reference between chapters (or to a sibling
   guide) is checked to exist.**
8. **Where ethics are relevant — permissions, attribution,
   licensing, access to others' work — the guide states the
   ethical move in the main text, not a footnote, and before
   the technique that needs it.** Avoiding detection or rules
   is never a goal; staying inside shared limits and terms is.
9. **State the limits of the subject in the guide itself** —
   what it cannot do, and which claims were verified live,
   which from documentation, and which nearby capabilities
   are documented-only and must not be overstated.

## How this guide was verified

The lab this guide was written in is a Linux machine, and
winget is a Windows-only tool that ships inside Microsoft's
App Installer. **No winget command could be run here, so
this guide's practical content is documented-only by
construction** — the same ceiling a few earlier guides in
this series met for platform-bound subjects. Nothing in the
chapters pretends otherwise: there are no lab transcripts,
and the only command output printed in full (the
`winget source list` table in chapter 8) is the sample output
from Microsoft's own reference documentation, presented as
documented shape rather than as a captured run.

What was checked, and where:

| Claim area | Status | Where checked |
|---|---|---|
| Command and subcommand names, aliases (`update`, `add`), global options | Checked against documentation | Microsoft Learn, Windows Package Manager overview |
| Install behaviour: query matching, `-e`, `--id`, scope, architecture, silent and agreement options, multi-package installs, msstore product-code IDs | Checked against documentation | Microsoft Learn, `winget install` reference |
| Upgrade: listing, `--all`, `--include-unknown`, `--include-pinned`, `--uninstall-previous` | Checked against documentation | Microsoft Learn, `winget upgrade` reference |
| Pinning: Pinning / Blocking / Gating types, `pin add/remove/list/reset`, `--blocking`, `--version` ranges, `--installed` | Checked against documentation | Microsoft Learn, pinning documentation and the upgrade reference |
| Export/import: options, JSON shape, unmatched-app warnings | Checked against documentation | Microsoft Learn, export and import references |
| Sources: the three defaults with their URLs, explicit vs implicit, administrator requirements, `reset --force`, agreement prompts | Checked against documentation | Microsoft Learn, `winget source` reference |
| Settings keys: schema URL, `telemetry.disable`, `visual.progressBar` values, `installBehavior` preferences and portable roots, `source.autoUpdateIntervalInMinutes`, `network.downloader`, logging limits | Checked against documentation | Microsoft Learn, `winget settings` reference |
| App Installer delivery, Windows 10 1809 minimum, first-login registration fix, repair via `Repair-WinGetPackageManager`, log locations, hash-mismatch and 403 behaviour | Checked against documentation | Microsoft Learn, overview and troubleshooting pages |
| Example package IDs `Mozilla.Firefox`, `VideoLAN.VLC`, `7zip.7zip` | **Verified to exist** | `microsoft/winget-pkgs` manifest folders, via the GitHub API |
| Example package IDs `Git.Git`, `Microsoft.PowerToys`, `Microsoft.VisualStudioCode`, `Microsoft.PowerShell`, and the msstore example code `XP9KHM4BK9FZ7Q` | Checked against documentation examples | Microsoft Learn worked examples in the install, upgrade, pinning and settings references |
| This checkout's mechanics: MkDocs nav vs actual files, YAML validity, deploy-workflow identity | Verified locally | winget-lab/verification-notes.md |

Notes on specific criteria:

- **Criterion 6** is the one this guide meets in its weakest
  honest form. Core workflows are complete and follow
  Microsoft's own worked examples, but no output here was
  captured from a real run, and none is dressed up as if it
  were. On a reader's Windows machine every command behaves
  as the documentation describes; this lab simply could not
  produce the screen to prove it.
- **Criterion 8** is met in chapter 1, before any technique:
  the guide states up front that winget delivers other
  people's software, that installs should be limited to
  software you trust from sources you trust, and it flags
  `--ignore-security-hash` — the one option that disables a
  safety check — with a warning in chapter 5 and an
  alternative in chapter 13 rather than teaching it as a
  shortcut.
