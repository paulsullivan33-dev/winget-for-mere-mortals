# winget for Mere Mortals

Software on Windows used to mean a tour of websites: search
for the program, find the real download page among the
imitators, fetch an installer, click Next through its wizard,
decline the bundled extras, repeat for every program and
every new PC. **winget**, Microsoft's Windows Package
Manager, replaces the tour with one command per program —
`winget install Mozilla.Firefox` — and one more,
`winget upgrade --all`, that keeps everything current at
once.

This guide teaches winget the way you will actually use it:
finding software and checking it before installing, quiet
installs with the right scope, upgrades with pins for the
programs you want left alone, sources and settings, and the
capstone — exporting one machine's whole set of programs to
a small text file and replaying it onto a new PC. No
administrator career required; some commands need a UAC
prompt, and the guide says which, and why, as they come up.

## Chapters

1. [What winget Is](what-winget-is.md) — the tool, where it
   comes from, and the trust rule to learn first.
2. [The Moving Parts](the-moving-parts.md) — the command,
   App Installer, sources, manifests and installers.
3. [Checking winget Is There](checking-winget.md) — version
   checks, the missing-winget fixes.
4. [Finding Software](finding-software.md) — `search`,
   `show`, and a first look at `list`.
5. [Installing Software](installing-software.md) — IDs and
   exact matching, silent installs, scope, architecture,
   several at once.
6. [Keeping Software Up to Date](keeping-up-to-date.md) —
   `upgrade`, `--all`, and pinning what must not move.
7. [Removing Software](removing-software.md) — `uninstall`
   and honest housekeeping with `list`.
8. [Sources](sources.md) — the community catalogue, the
   Store source, fonts, agreements, adding your own.
9. [Settings](settings.md) — the JSON file: telemetry,
   defaults, portable folders, progress bars.
10. [A New PC, End to End](a-new-pc-end-to-end.md) —
    `export`, `import`, and the full move, edges included.
11. [The Neighbours](the-neighbours.md) — the Store app,
    Chocolatey, Scoop, and doing it by hand.
12. [Limits](limits.md) — what winget cannot see, move or
    guarantee, stated plainly.
13. [Troubleshooting](troubleshooting.md) — logs, hash
    mismatches, failed installers, and the documented repair.
14. [Glossary](glossary.md)

## What you need

A PC running Windows 10 version 1809 or later, or Windows
11, and a terminal — Windows Terminal, PowerShell or Command
Prompt will do. Nothing to buy and nothing extra to install:
winget is part of Windows. Every program used as an example
in this guide (Firefox, VLC, 7-Zip, Git, PowerToys) is free,
and every package ID printed here was checked against the
real community repository; the [writing criteria](criteria.md)
explain how, and are candid that this guide's checking was
done against Microsoft's documentation rather than on a
Windows lab machine.

## Related guides

- [PowerShell for Mere Mortals](https://paulsullivan33-dev.github.io/powershell-for-mere-mortals/)
  — winget is typed at a prompt; this is the prompt, taught
  properly: commands, pipelines, and scripts of your own.
- [Homebrew for Mere Mortals](https://paulsullivan33-dev.github.io/homebrew-for-mere-mortals/)
  — the same idea on macOS and Linux: one command to install,
  one to upgrade, a catalogue behind both. Reading the two
  side by side shows how much of package management is the
  same everywhere.

## License

Text: [CC BY 4.0](LICENSE). Code: [MIT](LICENSE-CODE).
