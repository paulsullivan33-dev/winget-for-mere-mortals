# Keeping Software Up to Date

Keeping forty programs current by hand means forty separate
updaters, forty "a new version is available" popups, and —
realistically — thirty-eight programs quietly out of date.
winget replaces all of that with one command and one verb:
`upgrade`.

## See what is waiting

```powershell
winget upgrade
```

With no target, `upgrade` does not change anything: it lists
every installed program for which a newer version is known,
with the current and available versions side by side. It is
the same view as `winget list --upgrade-available`. Run it
weekly and you have a truthful patch report for the whole
machine — including programs you installed years before
winget existed, as long as they are recognised in the
catalogue.

## Upgrade one, some, or all

```powershell
winget upgrade --id Mozilla.Firefox -e
winget upgrade --all
```

`--all` works through the list and upgrades everything it
can. (It is also spelled `-r` or `--recurse`, and the whole
command answers to the alias `winget update`.) Two behaviours
to know:

- Some installed programs report no version at all — older
  installers often never recorded one — so winget cannot tell
  whether the catalogue's copy is newer. Those are skipped by
  `--all` unless you add `-u` (`--include-unknown`), which
  upgrades them anyway on the assumption the catalogue is
  newer. Usually right; occasionally a downgrade in disguise
  for oddly-versioned programs.
- Normally an upgrade *replaces* the old version using
  whatever the new installer does. `--uninstall-previous`
  asks winget to remove the old version first, for the
  programs whose installers stack copies side by side instead
  of replacing them.

## Pinning: the program you do not want upgraded

Sooner or later there is one program whose new version breaks
something you depend on, or whose redesign you are avoiding.
`winget pin` is how you exempt it — deliberately, and on the
record:

```powershell
winget pin add --id Microsoft.PowerShell -e
```

There are three kinds of pin, and the differences matter:

- **Pinning** (the default) — the package is skipped by
  `winget upgrade --all`. A *targeted* upgrade still works:
  `winget upgrade --id Microsoft.PowerShell` upgrades it
  anyway, and `--all --include-pinned` brings pinned packages
  back into a mass upgrade. This is "not unless I say so".
- **Blocking** — `winget pin add --id X --blocking`. Nothing
  upgrades the package through winget, targeted or otherwise,
  until the pin is removed (a targeted `--force` upgrade is
  the only exception). This is "not at all".
- **Gating** — `winget pin add --id X --version 1.2.*`. The
  package may upgrade freely *within* the range you name —
  `1.2.0` up to the last `1.2.x` — and no further. This is
  "patch yes, new feature release no", and it is the most
  useful of the three for cautious people.

Managing pins is part of the same command:

```powershell
winget pin list
winget pin remove --id Microsoft.PowerShell -e
winget pin reset --force
```

`pin add --installed` pins a package at exactly the version
currently installed — handy for a gating pin you build from
today's version. Two honest limits: a pin restrains *winget*,
not the program — plenty of programs have their own built-in
updaters and will cheerfully upgrade themselves behind
winget's back — and `winget upgrade` does report pinned
packages in its output as upgrades being held back, which is
how you remember the pin exists.

The habit this chapter is really teaching: run
`winget upgrade`, read the list, then `winget upgrade --all`.
A pinned handful, reviewed now and then, is a policy. An
un-updated everything is a vulnerability with good
intentions.
