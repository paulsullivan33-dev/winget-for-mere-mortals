# The Moving Parts

Four pieces make winget work. None of them is complicated,
and knowing which piece does what makes every later chapter —
especially troubleshooting — much easier.

## The winget command

The part you touch. `winget` is a command-line program: you
type a verb, some options, and the name or ID of a package.

```powershell
winget install --id Git.Git -e
```

The verbs you will use most are `search`, `show`, `install`,
`upgrade`, `list`, `uninstall`, `export` and `import`.
Microsoft's full command list also includes `source`,
`settings`, `pin`, `hash`, `validate`, `download`, `repair`
and `configure`, and each command explains itself:
`winget install --help` prints its usage and every option.
Two global habits worth forming early:

- `winget --version` prints the version and is the standard
  "is it alive?" test.
- `winget --info` prints version and path information,
  including where the log files live — the first stop in
  chapter 13.

Commands can be shortened with aliases for a few verbs:
`winget update` works in place of `upgrade`, and
`winget add` in place of `install`. This guide uses the full
names; the aliases exist if you see them elsewhere.

## App Installer

The Windows component that contains winget. Being part of
App Installer is why winget appears on Windows 10 and 11
without you installing it, and why it updates through the
Microsoft Store. On Windows Server it arrives with
Windows Server 2025. If winget is missing or broken, it is
almost always App Installer that needs attention — chapter 3
covers the checks and the known fix.

## Sources and manifests

winget does not keep its catalogue on your PC. When you ask
for a package, it asks a **source** — a catalogue service —
what is available. Three sources are built in:

| Source | What it holds |
|---|---|
| `winget` | The community repository: thousands of ordinary Windows programs, each described by a manifest |
| `msstore` | Microsoft Store apps, addressed by product code rather than name |
| `winget-font` | Fonts (held apart from the main catalogue, for reasons chapter 8 explains) |

A **manifest** is the catalogue entry for one version of one
program. It names the package and its publisher, gives the
**package ID** — a stable identifier like `Mozilla.Firefox`,
`Git.Git` or `7zip.7zip` — states the download address of the
official installer, records the installer's **SHA-256 hash**
(its fingerprint), and says what kind of installer it is and
how to run it quietly. The community repository behind the
`winget` source is the public `microsoft/winget-pkgs` project
on GitHub, where manifests are submitted and reviewed like
code.

## The installers themselves

winget is a manager, not a format. Underneath, programs still
ship as the same installers they always were, and winget
handles them all: MSI and MSIX packages, EXE installers of
several families (Inno Setup, Nullsoft, WiX and Burn among
them), APPX packages, plain ZIP archives, and **portable**
programs that are simply copied into a folder and added to
your PATH. The manifest tells winget which kind it is dealing
with and what silent switches to use, which is why a command
that looks identical can quietly do quite different work.

The division of labour, then: the source holds the
descriptions, the manifest holds the facts, the vendor's
website holds the installer, and winget fetches, verifies and
runs it. When something goes wrong, it is worth asking which
of the four just failed — chapter 13 is organised around
exactly that question.
