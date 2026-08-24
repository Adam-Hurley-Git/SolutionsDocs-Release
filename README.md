# Solutions Docs

Generates readable technical documentation from an exported **Power Platform**
solution (`.zip`) or canvas app (`.msapp`) — Word, Markdown and HTML, with flow
diagrams, and optional live SharePoint list detail.

This repository exists only to host the download. The source is not public.

---

## Download

Grab the latest `SolutionsDocs-Setup-vX.Y.Z.zip` from the
[Releases page](https://github.com/Adam-Hurley-Git/SolutionsDocs-Release/releases/latest).

**The package is password protected.** The password is not published here — ask
whoever sent you the link.

---

## Install

1. **Extract the whole zip** to any folder.

   Don't run `Install.cmd` straight from the zip preview window. Windows doesn't
   unpack the other files when you do that, and the installer will tell you it
   can't find the payload.

2. **Double-click `Install.cmd`.**

   Windows may warn that the file came from the internet — click **More info →
   Run anyway**. That's expected for any unsigned download.

3. **Enter the password** when prompted.

4. Accept the defaults for the remaining questions.

That's it. A shortcut appears on your Desktop; double-click it to use the tool.
The password is only needed during installation — running the app never asks
for it.

Everything installs under your own user profile at
`%LOCALAPPDATA%\Programs\SolutionsDocs`, so **no admin rights are required** and
nothing system-wide is touched.

---

## Requirements

Windows 10 or 11. Nothing else is needed to generate documentation — the .NET
runtime and Graphviz are bundled.

The optional **SharePoint enrichment** step additionally needs:

| | |
|---|---|
| [PowerShell 7](https://aka.ms/powershell-release) | the enrichment step runs in a real pwsh process |
| `PnP.PowerShell` module | `Install-Module PnP.PowerShell -Scope CurrentUser` |

The installer checks for both and offers to set them up. Without them,
documentation still generates — you just lose the SharePoint step.

---

## Uninstall

Delete `%LOCALAPPDATA%\Programs\SolutionsDocs` and the Desktop shortcut.
Optionally also `%APPDATA%\SolutionsDocs` (cached connector icons and saved
settings) and `%LOCALAPPDATA%\SolutionsDocs` (run logs).

---

## A note on logs

Each run writes two logs, under `%LOCALAPPDATA%\SolutionsDocs\PipelineUI\logs`:

- **`raw-local.log`** — may contain real tenant data: site URLs, list and column
  names, sample values. **Don't share this file.**
- **`summary-shareable.log`** — sanitised. URLs, GUIDs, email addresses and file
  paths are stripped. This is the one to send if someone asks for a log.

---

## Verifying your download

Each release lists the SHA-256 of its asset. To check what you downloaded:

```powershell
Get-FileHash .\SolutionsDocs-Setup-v1.0.0.zip -Algorithm SHA256
```

If it doesn't match, the download was truncated — get it again.

---

## Credits

Built on [PowerDocu](https://github.com/modery/PowerDocu) by René Modery, used
under the MIT licence, with local modifications.
