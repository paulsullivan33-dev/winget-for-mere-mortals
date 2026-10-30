# Checking winget Is There

Before the interesting chapters, two minutes of groundwork:
proving winget is present, seeing what version you have, and
knowing the one repair worth trying if it is not.

## The basic checks

Open Windows Terminal or PowerShell and run:

```powershell
winget --version
```

If winget is installed, this prints its version number and
you are done — move on to chapter 4. A current Windows 10 or
Windows 11 machine should answer without fuss.

```powershell
winget --info
```

goes further: it prints detailed version and path
information, including **the folder where winget writes its
log files**. Remember that this exists; chapter 13 sends you
back here the first time an install fails mysteriously.

## If winget is not recognised

`winget` answered with "not recognised as the name of a
cmdlet"? Work down this list:

1. **Check the Windows version.** winget needs Windows 10
   version 1809 (build 17763) or later, or Windows 11.
   `winver` shows what you have. Older than that, winget is
   not available — the machine needs a Windows update first,
   not a winget fix.
2. **Update App Installer.** winget rides inside App
   Installer, so open the Microsoft Store, go to its Library,
   and let App Installer update. Many "winget is missing"
   reports are simply a very old App Installer.
3. **The first-login registration quirk.** On a brand-new
   user account, App Installer may not finish registering
   until the first sign-in completes; if several people share
   the machine, a newer account can find winget mysteriously
   absent. Microsoft's documented fix, run in PowerShell, is:

   ```powershell
   Add-AppxPackage -RegisterByFamilyName -MainPackage Microsoft.DesktopAppInstaller_8wekyb3d8bbwe
   ```

4. **Ask winget to explain itself.** Once the command runs at
   all, `winget --info` shows where its logs are, and
   `winget --logs` opens that folder. Failures leave dated
   `.log` files there (kept for about a week by default).

## A note on terminals and rights

Everything in this guide is typed in PowerShell or Windows
Terminal — your choice; the commands are the same. Most
day-to-day winget work needs no administrator rights: winget
will ask for elevation with a UAC prompt when a particular
install genuinely needs it, and installing for just your own
account never does. A few operations are administrator-only
by design — adding and removing *sources* (chapter 8) is the
main one. Running a permanently elevated terminal is neither
needed nor a good idea.

There is also one context winget pointedly does not support:
running as the **SYSTEM** account, which is how some remote
management tools try to use it. Microsoft's own guidance for
that situation is the PowerShell module covered in
chapter 13, not the winget command itself.
