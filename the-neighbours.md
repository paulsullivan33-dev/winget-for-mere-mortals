# The Neighbours

winget does not exist in a vacuum. Depending on your habits
it rubs along with the Microsoft Store's own app, two older
community package managers, and the traditional method —
downloading installers from websites yourself. Here is how
they differ, and where each still wins.

## The Microsoft Store app (and the `msstore` source)

The Store and winget are not rivals so much as two doors to
overlapping shelves. The same Store app can be installed by
clicking in the Store app or by `winget install` from the
`msstore` source. What winget adds is scriptability and a
single update list. What the Store app adds is everything
visual and commercial: screenshots, reviews, age ratings, and
— decisively — **buying**. winget cannot purchase anything;
paid Store apps must be bought in the Store first, after which
winget can install and update the licence you own.

The subtler difference is the *same program in two sources*.
Git, VS Code and many others exist both in the community
catalogue and in the Store, and they are not identical goods:
the Store copy is packaged and serviced by the Store's
machinery (sometimes sandboxed differently, sometimes lagging
or leading in version), while the community copy is the
vendor's classic installer, verified by hash. Pick one
deliberately per program — `--source` exists for this — and do
not be surprised when `winget list` shows cousins rather than
twins. For classic desktop programs, this guide's default is
the community source; for Store-only apps and games, the
Store is the only door there is.

## Chocolatey

The elder of Windows package management: Chocolatey has done
winget's job since 2011, wraps installers in its own package
format with PowerShell install scripts, and has a vast
community repository plus a long track record in company IT.
It still wins for some business software and for people with
years of Chocolatey packages already written. Its costs are
an extra runtime to install and trust, and install scripts
that do more arbitrary work than a winget manifest's simple
"download, hash, run" — power that cuts both ways.

## Scoop

Scoop takes the opposite philosophy: portable programs only,
installed into a folder in your profile, no admin rights, no
registry, no installers at all if it can help it. For
command-line tools and a developer's utility belt it is
genuinely lovely, and its per-user, self-contained style
influenced how winget treats portable packages. Its catalogue
is narrower and more developer-focused than winget's, and it
does not aspire to manage your whole machine.

## Doing it by hand

The old way still has one unbeatable feature: it works for
everything, including the program too obscure, too new or too
corporate for any catalogue. This guide is not precious about
it — chapter 10's workflow ends with manual installs for
exactly the programs export could not match. The realistic
goal is not "never visit a vendor site again" but "stop
visiting thirty of them every time a PC is replaced, and let
the machine report honestly on the rest."

## So which should you use?

If you run Windows 10 or 11 and your software is mainstream:
winget, because it is already there, needs nothing extra to
trust, and covers search, install, upgrade, pin, export and
import in one tool. Add Scoop if your life is command-line
utilities kept tidily in your profile. Keep Chocolatey if
you already have it working or manage business machines with
it. Use the Store app for buying things and for Store-only
apps. None of these choices is a marriage; programs installed
by one tool generally show up in the others' lists, because
underneath they are all arguing with the same Windows
installer machinery.
