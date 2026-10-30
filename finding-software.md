# Finding Software

You rarely know a package's exact ID in advance, and you do
not need to: `search` finds candidates, and `show` tells you
what winget knows about one. Between them they answer the two
questions that matter before installing anything — *what is
the package called, and do I trust what it points at?*

## Searching

```powershell
winget search firefox
```

`search` compares your text against package names, IDs and
monikers (short nicknames publishers register, like `git`),
matching anything that *contains* the text, without worrying
about capital letters. The results come back as a table with
the columns that matter:

- **Name** — the friendly name, such as Mozilla Firefox.
- **Id** — the package ID, such as `Mozilla.Firefox`. This
  is the column to copy from: IDs are stable and unambiguous,
  names are not.
- **Version** — the newest version the source knows about.
- **Source** — which catalogue the entry came from
  (`winget` or `msstore`).

A broad word returns a crowd. Narrow the result down instead
of scrolling:

```powershell
winget search --id Mozilla.Firefox
winget search --name Firefox
winget search firefox --source winget
```

and for a search that must match the whole name rather than
find your text inside it, add `-e` (exact):

```powershell
winget search -e --name "Mozilla Firefox"
```

## Looking closer with `show`

Found a candidate? Inspect it before installing:

```powershell
winget show --id Mozilla.Firefox -e
```

`show` prints the package's full catalogue entry: publisher,
description, licence, the homepage, the newest version and —
most valuable of all — details of the installer winget will
fetch, including its address and its recorded hash. This is
your chance to apply the chapter 1 rule: the installer should
come from an address belonging to the maker. If a package
claims to be a well-known program but its installer lives on
an unrelated file-sharing host, stop and think.

`--versions` adds the list of versions available, which
matters when you deliberately want an older one:

```powershell
winget show --id VideoLAN.VLC -e --versions
```

## The other direction: what is already installed

`list` works the search machinery backwards — instead of the
catalogue, it shows what is on *this* machine:

```powershell
winget list
```

Every row is an installed program, matched where possible to
a catalogue package, with its current version and — the
column that earns its keep — the **Available** version, if an
upgrade exists. Filtering works as you would expect:
`winget list --id Git.Git`, `winget list firefox`, and
`winget list --upgrade-available` to see only the programs
with updates waiting. Chapter 7 returns to `list` properly;
for now, run it once and enjoy the novelty of one screen
telling the truth about everything installed on your PC,
including programs that arrived long before winget did.
