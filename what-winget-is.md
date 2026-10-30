# What winget Is

winget is a program you type commands into that installs,
upgrades and removes other programs on Windows. Instead of
visiting a website, downloading an installer, and clicking
through its wizard, you type one line:

```powershell
winget install Mozilla.Firefox
```

winget finds Firefox in its catalogue, downloads the real
installer from Mozilla, checks the file against a fingerprint
recorded in advance, runs it quietly, and reports whether it
worked. The same one-line treatment covers hundreds of
everyday programs: browsers, editors, media players, developer
tools. The name comes from **Win**dows Packa**ge** Manager —
winget is the command-line half of that service.

The idea is not new. Linux has had package managers for
decades, and macOS users have Homebrew. Windows was the odd
one out: for most of its life, installing software meant a
treasure hunt across vendor websites, each with its own
download page, its own installer, and its own idea of what
else to bundle in. winget is Microsoft's answer, and it has
been part of Windows since Windows 10 version 1809.

## Where it comes from

winget does not live alone. It ships inside a Windows
component called **App Installer**, which Microsoft delivers
through the Microsoft Store. That has two practical
consequences:

- If your PC runs Windows 10 (1809 or later) or Windows 11,
  winget is almost certainly already there. Open a terminal
  and type `winget --version` to check.
- winget updates itself the way Store apps do, in the
  background, without you running any installer for it.

The catalogue it searches — called the **Windows Package
Manager Community Repository**, or winget-pkgs — is a public
project on GitHub maintained by Microsoft with contributions
from anyone. Each package in it is a small text file, a
*manifest*, that says where the official installer lives and
what its fingerprint should be. Chapter 2 pulls this apart.

## The one thing to understand before you start

winget is a delivery service, not a software shop. It does not
host, check or vouch for the programs it installs: the
installer still comes straight from the maker's own website,
and the manifest's fingerprint exists so winget can prove the
file you received is the file the manifest described. That is
a real safeguard — but it means the usual judgement still
applies. **Install only software you would be willing to
download from the maker's site yourself, from sources you
trust.** Chapter 8 explains sources properly; the short
version is that the two built-in sources (Microsoft's
community catalogue and the Microsoft Store) are the sane
defaults, and you should think hard before adding anyone
else's. And one option in this guide, `--ignore-security-hash`,
deliberately turns off the fingerprint check; it appears in
chapter 5 with the warning it deserves.

## What this guide does with it

You will learn to find software, install it quietly and in
the right scope, keep everything up to date with one command,
pin the one program whose updates you do not want, remove
things cleanly, and — the payoff — describe a whole PC's set
of programs in one small file, so a new PC can be set up to
match it in minutes. Chapter 10 is that full workflow, end to
end.

One honest note before starting: winget is a Windows tool,
and this guide was written and checked against Microsoft's
official documentation rather than on a Windows machine in
the lab. The [writing criteria](criteria.md) say exactly
what was verified and how.
