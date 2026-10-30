# Removing Software

Uninstalling is the least glamorous verb and the one where a
package manager earns trust: the program goes, its files go,
and Windows' own list of installed programs agrees afterwards.
winget's verb is `uninstall`, and it works on programs winget
installed and on programs that were already on the machine.

## The plain uninstall

```powershell
winget uninstall --id VideoLAN.VLC -e
```

The same query rules as install apply: a loose name matches
loosely, so prefer the `--id … -e` form, especially since
several programs with similar names are exactly the situation
where removing the wrong one hurts. If a query matches more
than one installed program, winget lists them and stops
rather than guess. Add `-h` (`--silent`) to suppress the
uninstaller wizard where the package supports it, and
`--version` to remove one specific version when a program
keeps several versions side by side.

What actually happens depends on how the program was
installed in the first place: winget runs the program's own
registered uninstaller — the same mechanism behind Settings →
Apps — with the silent switches from the manifest where it
has them. A UAC prompt may appear for machine-scope programs,
and a badly behaved legacy uninstaller may still show its
wizard despite `-h`. That is the installer's choice, not
winget disobeying you.

## Portable packages and tidying up

Portable packages — the kind winget simply copies into a
folder and puts on your PATH — are removed by deleting that
folder and the PATH entry. The settings file can make
uninstallation of portables thorough by default
(`uninstallBehavior.purgePortablePackage`, chapter 9), so no
configuration files linger in the package folder afterwards.

## Keeping the inventory honest

Removal is also housekeeping, so this is the chapter where
`list` becomes a habit:

```powershell
winget list
winget list --source winget
```

Run `winget list` every few months and read it with fresh
eyes. A winget-managed machine tends to accumulate the same
clutter as any other — the trial program from spring, the
second media player, the utility replaced by another utility
— but here it is all on one screen, each with an exact ID you
can hand straight to `uninstall`. Sorting a printed `list`
output into "keep / unsure / remove" and working down it is
the cheapest performance upgrade a mature Windows machine
gets.

One limitation to know before you rely on it: winget can only
uninstall programs that registered themselves with Windows
properly. A program you once ran by unzipping it into a
random folder by hand — not through winget — has no
registration to find and no uninstaller to run; removing
those is still manual work, and chapter 12 is honest about
the rest of the boundary.
