# Settings

winget keeps its preferences in one file, in the JSON format.
You rarely need it — the defaults are sane — but four or five
settings are worth knowing by name: turning off telemetry,
setting your default install scope, quietening the progress
display, and saying where portable programs live.

## Opening the file

```powershell
winget settings
```

This opens the settings file in your default JSON editor
(Notepad, if nothing else claims.json files). The file lives
in App Installer's data folder, alongside the logs:

```text
%LOCALAPPDATA%\Packages\Microsoft.DesktopAppInstaller_8wekyb3d8bbwe\LocalState\settings.json
```

A new file contains almost nothing but a `$schema` line
pointing at Microsoft's settings schema
(`https://aka.ms/winget-settings.schema.json`) — that line is
what makes a decent editor offer autocompletion and warnings
for the keys below. Everything is optional; delete a key to
return it to its default. (Two neighbouring commands work on
a different class of setting: `winget settings --enable` and
`--disable` toggle *administrator* settings such as the
permission to install from local manifest files, and
`winget settings export` prints the admin settings as JSON.)

## The settings worth your time

**Privacy.** winget can emit basic telemetry events about
command usage. Switch it off:

```json
"telemetry": { "disable": true }
```

**Install defaults.** If you nearly always want the same
scope, architecture or installer kinds, say so once:

```json
"installBehavior": {
  "preferences": {
    "scope": "user",
    "architectures": ["x64"],
    "locale": ["en-US"]
  }
}
```

Per-command options still win when you give them; these are
only the defaults. `installBehavior` is also where
`"disableInstallNotes": true` silences the little notes
installers sometimes ask to show you, and where the roots for
**portable** packages are set: by default user-scope portables
live in `%LOCALAPPDATA%\Microsoft\WinGet\Packages\` and
machine-scope ones in `%PROGRAMFILES%\WinGet\Packages\`.

**The progress bar.** Pure taste, but it is *your* taste:

```json
"visual": { "progressBar": "retro" }
```

`progressBar` accepts `accent` (the default, following your
Windows accent colour), `rainbow`, `retro`, `sixel` and
`disabled`. The same group holds `anonymizeDisplayedPaths`,
which replaces your username in displayed paths — useful in
screenshots and screen shares.

**Source freshness.** `"source": { "autoUpdateIntervalInMinutes": 15 }`
is the default rhythm at which winget refreshes its catalogue
cache when used. Set it to `0` to take manual control
(`winget source update` becomes your job).

**Downloads and logs.** Downloads go to your Downloads
folder by default (`downloadBehavior.defaultDownloadDirectory`
changes that). If installs ever fail mysteriously on a
corporate network, `network.downloader` can be switched from
`do` (Windows Delivery Optimization, the default) to
`wininet`. Log verbosity lives under `logging`
(`"level": "info"` by default; `verbose` is the one
chapter 13 asks for), and log files are tidied automatically
— about a week's worth, 128 MB in total, by default.

## A worked example

A cautious user's whole file might be:

```json
{
  "$schema": "https://aka.ms/winget-settings.schema.json",
  "telemetry": { "disable": true },
  "installBehavior": {
    "preferences": { "scope": "user" },
    "disableInstallNotes": true
  },
  "visual": { "progressBar": "accent", "anonymizeDisplayedPaths": true }
}
```

Save, and the settings apply to the next winget command — no
restart of anything. If winget starts complaining about the
file itself, the cause is JSON syntax (a missing comma is the
classic); remove the last thing you added and reintroduce it
slowly.
