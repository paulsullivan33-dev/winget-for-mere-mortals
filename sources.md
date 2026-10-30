# Sources — Where Packages Come From

Everything winget installs comes from a **source**: a
catalogue service that answers "what packages exist, and
where do their installers live?" Knowing your sources matters
because the catalogue is the trust decision — a source can
offer you anything, and winget will fetch it. This chapter
covers the three built-in sources, the agreements that come
with them, and how sources are added, updated and removed.

## The three built-in sources

A fresh winget installation knows these sources. Running
`winget source list` shows them in this shape:

```text
Name        Argument                                      Explicit
------------------------------------------------------------------
msstore     https://storeedgefd.dsx.mp.microsoft.com/v9.0 false
winget      https://cdn.winget.microsoft.com/cache        false
winget-font https://cdn.winget.microsoft.com/fonts        true
```

- **winget** — the community repository. This is the source
  behind nearly every command in this guide: thousands of
  ordinary desktop programs, each described by a manifest
  pointing at the maker's own installer download and checked
  against a recorded hash. When you give no `--source`,
  winget searches here (and the Store) automatically.
- **msstore** — the Microsoft Store's catalogue. Packages
  here are addressed by Store product code (like
  `XP9KHM4BK9FZ7Q`), not by name-like IDs, and installing
  from it means accepting the Store's terms — see agreements,
  below. Chapter 11 compares Store-source installs with the
  community source in depth.
- **winget-font** — fonts, kept in their own catalogue. It is
  different in one way worth understanding: it is **explicit**,
  meaning searches ignore it unless you aim at it on purpose
  with `--source winget-font`. Microsoft keeps fonts out of
  general searches so that looking for a program is not
  drowned in typefaces. (`winget source edit winget-font
  --explicit false` would make it join general searches; few
  people need to.)

## Source agreements

The first time you use a source that carries terms — the
Microsoft Store source is the standing example — winget stops
and shows the agreement, asking you to accept before it will
search or install from it. That is deliberate: the Store's
terms include geographic availability rules for its apps. In
scripts, `--accept-source-agreements` accepts in advance
(and only after you have actually read the terms once,
interactively, like a person).

## Keeping sources fresh

Catalogues are cached on your machine and refreshed in the
background — by default winget checks for an updated
catalogue every 15 minutes when you use it (a settings value,
chapter 9). To refresh on demand:

```powershell
winget source update
winget source update --name winget
```

`source list --name winget` shows one source in detail,
including when it was last updated — the first thing to check
if a brand-new program version "does not exist" as far as
your machine is concerned.

## Adding and removing sources

New sources can be added — companies run private ones for
their own software, for example:

```powershell
winget source add --name MyCompany --arg https://packages.example.com/catalogue
```

Adding and removing sources requires **administrator** rights
(`winget source remove --name MyCompany` removes one). Take
the rights requirement as a hint about the stakes: a source's
manifests decide what gets downloaded and run on your
machine, so a third-party source deserves the same suspicion
as a third-party app store. Add only sources run by
organisations you trust, for a reason you can state.

If sources ever get into a tangle — an old experiment, a
half-removed private catalogue — the factory reset is:

```powershell
winget source reset --force
```

(administrator again), which removes every non-default source
and leaves the built-in three. You lose nothing but the
additions.
