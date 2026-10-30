# Glossary

**App Installer** — the Windows component
that contains winget. It is delivered and
updated through the Microsoft Store, which
is why winget is present on Windows 10
(1809+) and Windows 11 without a separate
download.

**Blocking pin** — the strictest pin type:
winget will not upgrade the package at
all, targeted or otherwise, until the pin
is removed. Set with
`winget pin add --blocking`.

**Catalogue** — the list of packages a
source knows, with their manifests. Cached
on your machine and refreshed in the
background or by `winget source update`.

**Exact match (`-e` / `--exact`)** — an
option making a query match the whole
name or ID, capitals included, instead of
any part of it.

**Explicit source** — a source excluded
from general searches unless named with
`--source`. The `winget-font` source is
explicit by default.

**Gating pin** — a pin that lets a
package upgrade only inside a version
range you name, such as `1.2.*`. Set with
`winget pin add --version`.

**Hash** — a file's SHA-256 fingerprint.
Manifests record the installer's hash;
winget verifies downloads against it and
stops on a mismatch.

**Installer type** — the format of the
underlying installer winget runs: MSI,
MSIX, APPX, EXE families (Inno, Nullsoft,
WiX, Burn), ZIP or portable.

**Manifest** — the catalogue entry for
one version of one package: its ID,
publisher, the official installer address,
the installer's hash, and how to install
it quietly. Manifests live in the public
microsoft/winget-pkgs repository.

**msstore** — the built-in source for
Microsoft Store apps, whose packages are
identified by Store product code rather
than a name-like ID.

**Package** — one program as winget knows
it: an ID, versions, and the installers
behind them. `Git.Git` is a package;
Firefox the browser is the program.

**Package ID** — a package's stable
identifier, shaped `Publisher.Package`,
such as `Mozilla.Firefox` or `7zip.7zip`.
IDs are the precise way to name a target.

**Pinning** — telling winget to leave a
package out of upgrades. Plain pinning
skips it in `--all`; see also Blocking
pin and Gating pin.

**Portable package** — a program winget
"installs" by copying it into a package
folder and adding it to your PATH, with
no traditional installer involved.

**Query** — the text winget matches
against names, IDs and monikers when you
don't specify a field. Loose by default:
case-insensitive and partial.

**Scope** — whether a program is
installed per user (your account only)
or per machine (all accounts, into
Program Files). Chosen with `--scope`
or as a default in settings.

**Source** — a catalogue service winget
consults: `winget` (community), `msstore`
(Store) and `winget-font` (fonts) are
built in; others can be added by an
administrator.

**Source agreement** — a source's terms,
shown and accepted before first use
(`--accept-source-agreements` in
scripts). Distinct from a package's own
licence prompt, the *package agreement*
(`--accept-package-agreements`).

**winget** — Microsoft's command-line
client for the Windows Package Manager
service: the program this guide teaches.
