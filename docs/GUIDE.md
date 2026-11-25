# Player guide

**English** · [Français](#français)

How to install and play *Stargate SG-1: The Alliance — Redial* **V0.1**. The port aims to play like the
December 2005 Xbox build; every deliberate difference is in [CHANGELOG.md](../CHANGELOG.md). Other documents:
[README](../README.md) (short overview), [installer details](#installer-details) (options, files written, updates),
[known issues](KNOWN_ISSUES.md), [cheats and console commands](CHEATS.md).

Contents: [Install](#install) · [Installer details](#installer-details) · [First launch](#first-launch) · [Menus](#menus) · [Controls](#controls) ·
[Options](#options) · [Difficulty](#difficulty) · [Saves](#saves) · [Multiplayer](#multiplayer) ·
[Updating and uninstalling](#updating-and-uninstalling) · [Troubleshooting](#troubleshooting)

## Install

### What you need

- **64-bit Windows** (tested on Windows 11).
- **Unreal Tournament 2004** for Windows, your own copy, with the **latest OldUnreal patch** installed over it:
  build 3374 of 2026-10-20 or later, from <https://github.com/OldUnreal/UT2004Patches/releases> (follow the
  instructions on that page). Older builds are refused by the installer.
- **The game files**: the 2019 release of the prototype, `Stargate_SG-1_-_The_Alliance-2005-12-15.7z` (about
  1 GB), from <https://archive.org/details/StargateSG1TheAlliance20051215>. You do not need to extract it.
- **The installer**: `Stargate-Redial-Alliance-v0.1-win64.zip` from the
  [Releases page](https://github.com/Stargate-Redial/alliance-redial/releases).
- About **9 GB** of free space and an **Internet connection** during the installation (it downloads helper
  programs from their official pages, checked against known hashes).

### Steps

1. Right-click the installer zip, choose *Properties*, tick *Unblock*, click *OK*. Then extract it anywhere, for
   example on your desktop.
2. Double-click **Stargate Redial Setup.exe**, or drop the `.7z` onto it. The installer window opens (in French
   when Windows is in French; a link switches the language).
   - **Game files**: it finds the `.7z` in your Downloads folder, on the desktop or next to the installer.
     Otherwise click *Browse…* (or *Use an extracted folder…*), or drop the file on the window.
   - **UT2004 folder**: it finds UT2004 through the registry and Steam. Otherwise click *Browse…* and choose the
     folder that holds `System\UT2004.exe`. If the OldUnreal patch is missing or too old, the window says so
     and links to the patch page.
   - **Install**: *Put a shortcut on the desktop* is ticked (untick it if you do not want one; the Start menu
     always gets one), keep *Check for updates when the game starts* ticked (see
     [Updating](#updating-and-uninstalling)), then click *Install*.
3. Wait. The window shows each step with a tick, the overall progress and the time left: about 3 minutes on an
   8-core PC, 5 to 6 minutes on a 4-core one, plus the extraction of the archive. *Cancel* stops safely.
4. Click **Play**. Later, start **Stargate Redial - The Alliance** from the Start menu or the desktop (or in
   `<UT2004>\SGAlliance`). While it runs, its taskbar button has the Redial name and icon.

The game is installed as a UT2004 mod: your UT2004 itself is not changed. Your keyboard layout (QWERTY or
AZERTY) is detected, and an Xbox-style controller is switched on (the game also does it by itself when it starts).

### Windows warnings

The installer is not code-signed (a fan project cannot buy a certificate).

- **SmartScreen** may say "Windows protected your PC": click *More info*, then *Run anyway*. It may ask about
  **Stargate Redial Setup.exe**; the window then starts `app\tools\sgredial.exe`, which may be asked about too.
- **Smart App Control** (Windows 11): when it is on, unsigned programs are blocked and there is no per-program
  exception, so the installer cannot run. Turning Smart App Control off is your decision; on some Windows 11
  versions it cannot be turned back on without reinstalling Windows.
- **Antivirus**: some flag the installer because it is a compiled Python program. Compare the zip's SHA-256 with
  the `.sha256` file on the Releases page; if it matches, restore the file and allow it.

## Installer details

The exact figures, the installer's options, what it writes on your PC, and how updates and the uninstaller work.

### Download details

- **The installer**: `Stargate-Redial-Alliance-v<version>-win64.zip` from the
  [Releases page](https://github.com/Stargate-Redial/alliance-redial/releases). The `.sha256` file next to it
  holds its SHA-256.
- **The game files**: `Stargate_SG-1_-_The_Alliance-2005-12-15.7z` (1,015,500,550 bytes, SHA-256
  `d70e15d5ceb479bb8443f2c0bcf2d8884f913a02033d7d8a8e33f80e622d47f4`) from
  <https://archive.org/details/StargateSG1TheAlliance20051215>.
- **UT2004** (Windows) with the **latest OldUnreal patch**: build 3374 of 2026-10-20 or later, from
  <https://github.com/OldUnreal/UT2004Patches/releases>. Earlier 3374 builds are refused: the port uses the
  newer build's Hor+ widescreen field of view. No UT2004 yet: OldUnreal's full-game installer,
  <https://www.oldunreal.com/downloads/ut2004/full-game-installers/>.
- Nothing else: Python, ffmpeg and 7-Zip are **not** needed. The installer needs an Internet connection: it
  downloads an ffmpeg build for the audio (about 28 MB, once) from its official page, checked against a pinned
  SHA-256 hash. Plan about 9 GB of free space (work folder up to 6.5 GB, mod 2.5 GB).

### Install details

- Tip: right-click the zip, *Properties*, tick *Unblock*, *OK*, then extract: Windows then shows fewer warnings.
- You can drop the `.7z` onto **Stargate Redial Setup.exe**. The window checks the file (size and SHA-256), finds
  UT2004 through the registry and Steam, and tells you if the OldUnreal patch is missing or too old.
- *Show details* in the window shows the installer's messages. Expect about 3 minutes on an 8-core PC and 5 to 6
  minutes on a 4-core one, plus the extraction of the archive. *Cancel* stops it safely: nothing is left
  half-installed, and running the installer again continues where it stopped.
- The window opens in French when Windows is in French, in English otherwise (a link switches the language).
- The antivirus warning: the installer is a Python program compiled with Nuitka, a pattern that some antivirus
  heuristics dislike. Compare the zip's SHA-256 with the one on the Releases page.
- Online games use OldUnreal's master server (the list comes from your OldUnreal `Default.ini`); LAN games use
  UT2004's LAN discovery.

### Installer options (command line)

The window offers the usual choices. For every option, run the installer program itself from a command prompt
(in the extracted folder); it works exactly as the window's installer, with text output:

```bat
app\tools\sgredial.exe --archive "D:\Downloads\Stargate_SG-1_-_The_Alliance-2005-12-15.7z" --dry-run
app\tools\sgredial.exe --help
```

| Option | Effect |
|---|---|
| `--archive <7z>` / `--extracted <folder>` | the release archive, or the folder where you already extracted it (every file is checked) |
| `--ut2004 <folder>` | your UT2004 folder, if it is not found |
| `--workdir <folder>` | work folder (default `%LOCALAPPDATA%\SGAlliance-build`, several GB) |
| `--dry-run` | checks the prerequisites and the archive, prints the plan, changes nothing |
| `--jobs N`, `--sequential` | fewer processes at a time, to keep the PC responsive |
| `--lightmaps runtime` | UT2004 relights the maps instead of using the game's baked lighting |
| `--skies keep` | keeps the 2005 sky textures (by default the installer smooths their compression blocks and stores them uncompressed) |
| `--desktop-shortcut` | also puts the launcher on your desktop (the Start menu always gets it) |
| `--no-update-check` | the Play shortcut starts the game directly, without checking for a new version |
| `--keyboard qwerty\|azerty` | key preset (default: from your Windows keyboard layout; the game's Options > Controls page can switch it later) |
| `--gamepad on\|off` | forces the controller on or off and records your choice (the game otherwise turns on a controller it finds at start) |
| `--reset-keys` (or `--reset-video`, `--reset-pad`) | restores the default keys, video settings or pad layout; installs and updates otherwise keep yours |
| `--verify` | on an installed, up-to-date mod: checks every installed file by its SHA-256 |
| `--force` | rebuilds everything; also allows installing an older version over a newer one |
| `--ffmpeg <ffmpeg.exe>`, `--sevenzip <7z.exe>` | use these instead of downloading them |
| `--server` (`--server-settings <ini>`, `--server-bundle <file>`) | after the install, also sets up dedicated servers in `<UT2004>\SGAlliance\Server` (and a bundle for a Linux server): [SERVER.md](SERVER.md) |
| `--uninstall` (`--dry-run`, `--purge-saves`) | see [Uninstall in detail](#uninstall-in-detail) |

### What the installer writes

The mod goes to `<UT2004>\SGAlliance` and has its own `SGAlliance.ini`; your UT2004 settings are not touched.
**One exception:** UT2004 reads per-class configuration files only from its own `System` folder, even for a
mod, so the installer copies these there: `Tweak_*.ini` (the game's tuning values, about 137 files),
`SGAMusic.ini`, `SGSpeechData.ini`, `SGLipSyncData.ini`, `SGMeshMaterials.ini` and `SGChapterBriefings.ini`. The
game itself later writes
`SGSpeech.ini` (settings) and `SGASaves.ini`, `PlayerProfile.ini`, `Stats.ini` (saves, settings, statistics)
there. After each install or update the installer also has UT2004's own tool write the game's map list for the
mod's maps there (`SGA-*.ucl`, one per map: the files the game would otherwise write at its first start, which made
that start take minutes); uninstalling removes them. No UT2004 file is replaced. Every file the installer wrote, in
the mod folder and in
`<UT2004>\System`, is listed with its SHA-256 in `SGAlliance\.redial\manifest.json` (the ones in
`<UT2004>\System` also in `SGAlliance\installed-outside-mod.txt`). With the update check (the default),
`SGAlliance\Launcher` holds a copy of the installer program (about 40 MB) that the Play shortcut starts.

The mod is built in the work folder first and copied into `<UT2004>\SGAlliance` only at the very end, in one step
that is undone if it is interrupted: a failed or stopped install never leaves a half-installed mod, and running
the installer again resumes where it stopped. The work folder keeps the extracted release and the build, so that
a second run or an update only redoes what changed; you can delete it once the game works (the next update then
rebuilds everything, which takes a few minutes longer).

### Updating in detail

**When the game starts.** Online games need the same version on both sides, so the **Stargate Redial - The
Alliance** shortcut first asks GitHub whether a newer release exists (this project's public Releases page). It
sends nothing about you or your PC: no account, no identifier, no cookie, only a plain request for the latest
release. It waits 2 seconds at most; offline, or with no newer version, the game starts at once. When there is
one, a small window shows what's new in that version (the release notes from GitHub, in your Windows language
when they exist in it) and offers *Update*, *Later* or *Skip this version* (skipped versions are remembered in
`%LOCALAPPDATA%\Stargate-Redial\update-state.json`). *Update* downloads the new zip with its `.sha256` and its
signature into `%LOCALAPPDATA%\Stargate-Redial\updates`, checks that it is the file the project signed (an
Ed25519 signature checked against the key built into the installer; a file that does not verify is deleted and
nothing is installed), then opens the new version's installer, which updates the game with your current options
and offers *Play* at the end. The update needs the game files again: the work folder still holds them unless you
deleted it; otherwise the window asks for the `.7z` (found in your Downloads folder like the first time).

To turn the check off, untick *Check for updates when the game starts* in the installer window (or install with
`--no-update-check`): the shortcut then starts the game directly. `Stargate Redial - The Alliance.cmd` in
`<UT2004>\SGAlliance` never checks.

**By hand.** When a new version is released, download its zip, extract it (into a new folder, or over the old one)
and run **Stargate Redial Setup.exe** again: the window shows *Update v0.1 → v0.2* and reuses the options you
chose before (desktop shortcut, update check, keyboard, controller). Do not uninstall first. The previous
version's zip and folder can be deleted.

- The installer reads the installed version and says what it does (*Update v0.1 → v0.2*; on the command line
  `updating 0.1 -> 0.2`). Installing an older version over a newer one asks for confirmation (`--force` on the
  command line).
- **Your data is never replaced**: key bindings, video, audio and controller settings, your other changes to the
  mod's settings files, saved games and checkpoints, screenshots and logs. Settings files are merged: a
  setting you changed keeps your value unless the new version changes that very default (the installer then
  lists it); settings a new version introduces are added. Before an update changes anything, your settings and
  saves are copied to `SGAlliance\.redial\backups` (the last 5 updates are kept).
- Files of the old version that the new one no longer has are removed (only if you did not change them); files
  the installer did not write are never touched.
- Only what changed is rebuilt. Running the installer again on an up-to-date install only checks the files: it
  takes seconds.
- If an update is interrupted (power cut, closed window), run it again: an interrupted copy into the mod folder
  is undone first, so you always have either the old or the new version complete, never a mix.
- Saved games are kept as they are, and newer versions keep reading the saves of older ones. Before an update the
  installer lists your saves by format and warns if the new version could not load some of them (they are kept
  and backed up, never deleted). Anything to know about a release is in [CHANGELOG.md](../CHANGELOG.md).

### Uninstall in detail

Run **Stargate Redial Setup.exe**, go to the last step and click *Uninstall…*; tick *Also delete my saves,
settings and statistics* only if you want that. From a command prompt: `app\tools\sgredial.exe --uninstall`
(add `--dry-run` to see every file first, `--purge-saves` to delete the saves too).

- It deletes exactly the files listed in the manifest (`SGAlliance\.redial\manifest.json`), wherever they are,
  and the installer's records. In `<UT2004>\System` it also deletes the game's own settings file `SGSpeech.ini`
  (and an `SGAlliance.ini` there, if the game made one) when every section in it belongs to this mod. It never
  deletes by file-name pattern.
- Files the installer did not write stay, with the folders that hold them: screenshots, logs, your own files. The
  `SGAlliance` folder is removed only if nothing else is left in it.
- **Saves are kept**: `SGAlliance\Saves`, `SGASaves.ini`, `PlayerProfile.ini`, `Stats.ini` and the update backups
  (`SGAlliance\.redial\backups`) stay. Add `--purge-saves` to delete them too.

## First launch

1. Start **Stargate Redial - The Alliance**. The game opens in full screen at your desktop resolution, shows
   the original logo screen, then the main menu over a Stargate scene. The main menu shows "Stargate Redial
   V0.1" in its bottom-right corner. The installer has already prepared the map list of the mod; if UT2004 itself
   was never started before, its first start still lists UT2004's own maps once, so the logo screen stays a little
   longer that one time.
2. **Nothing to set up.** The game keeps your saves, progress, difficulty, volumes, keys, mouse settings and
   multiplayer name, outfit and packs by itself; there is no profile to create or choose. (An install that already
   had profiles keeps using the one played last; the others stay on disk.)
3. Menus work with the mouse, the keyboard (arrows, Enter = select, Escape or Backspace = back, Delete and Insert
   for the other buttons) and a controller (d-pad or left stick, A select, B back). One item is highlighted at a
   time: the one under the mouse when you move it, else the one the keys or the pad moved to; Enter acts on it. The
   buttons at the bottom of a page are clickable and name their key: **Back (Esc)** on the left, the page's action
   on the right (**Select (Enter)**, **Load (Enter)**, **Start (Enter)**...). While you use a controller they show
   its buttons instead.

## Menus

### Main menu

- **Continue** loads the most recent checkpoint or quick save, as its 2005 hint text
  says. It is greyed until there is a save. (In the 2005 build it opened a temporary list of every map.)
  To start any mission part, use Single Player → Chapter Selection. The build has no missions 1, 3, 5, 6, 8, 9
  and 11.
- **Exit Game** quits the game after a confirmation, like Escape.
- **Single Player**:
  - **Continue** does what the main menu's Continue does (greyed while there is no save).
  - **New Game** asks whether you want to play the tutorial: *Yes* starts the tutorial (M00), *No* starts
    Mission 2.
  - **Chapter Selection** lists the 61 parts of the story; it shows no chapter pictures (the 2005 data has none).
    On the left it shows the selected chapter's 2005 mission briefing (location, local time and the briefing text,
    as on the in-game BRIEFING tab) above its name; M02A-D, M14A-C and M15A have none in the 2005 data and show
    only their name.
    Done chapters have a check mark and a green name, the current one (the furthest you reached) a gold arrow and a
    gold name, chapters not reached yet a grey name. The list opens on the current chapter; you
    can still start any of them. A click only selects a chapter (its briefing shows on the left); a double click, Enter or
    the **Start** button starts it. The Single Player menu shows your progress, for example
    "Progress: 21 % - chapter 14/61".
  - **Load Game** lists your checkpoints and the quick save ([Saves](#saves)) to load them.
  - **Tutorial** starts M00.
- **Multi-Player**: see [Multiplayer](#multiplayer).
- **Options**: Controls, Multiplayer (your multiplayer character), Video, Audio, Difficulty. See [Options](#options).
- The 2005 **Extras** button is hidden: its page was an empty placeholder.
- **Escape** on the main menu asks whether to quit.

A story mission is a chain of parts (M02A, M02B…): reaching the end of a part loads the next one. M21D, the last
part, returns to the main menu.

### In a mission

- **Escape** (Start on a controller): the pause menu, with *Resume Game*, *Restart*, *Options* and *Return to
  Main Menu*.
- **Tab** (Back): *Mission Information*, with the *OBJECTIVES* and *BRIEFING* tabs (Page Up / Page Down, or
  the d-pad or LB / RB, switch tabs).
- **"Press [E] to Skip"** ends a cutscene at once; the level continues as if you had watched it.
- When you die, **MISSION FAILED** offers *Retry* (from the last checkpoint, when the part has one), *Restart
  Chapter* (from the beginning of the part) and *Load Game*. **F9** loads your quick save from there too.
- Tutorial hints pause the game and name your own keys.

## Controls

Keys can be changed in **Options → Controls**. The controller column is the original 2005 Xbox
layout (the Xbox's white and black buttons are LB and RB, as on the Xbox 360).

| Action | Keyboard QWERTY | AZERTY | Controller |
|---|---|---|---|
| Move | W A S D, arrows | Z Q S D, arrows | left stick |
| Look | mouse | mouse | right stick |
| Sprint | Shift, or double-tap forward | same | push the left stick forward twice |
| Jump | Space | Space | A |
| Crouch (hold / toggle) | Ctrl / C | same | — / click the left stick |
| Walk | Caps Lock | Caps Lock | — |
| Fire / secondary fire | left / right mouse button | same | RT / LT |
| Zoom (scoped weapons) | middle mouse button | same | click the right stick |
| Use, pick up, skip a cutscene | E, Enter | E, Enter | X |
| Reload | R | R | X |
| Last weapon | Q | A | Y |
| Weapon selection | mouse wheel, 1 to 0 | same | d-pad up / down |
| Throw a grenade | 4 (grenades), then fire | same | d-pad to the grenades, then RT |
| Binoculars | B | B | d-pad left |
| Cloak (needs a shield belt) | F | F | B |
| Concentrate fire (hold: choose a squad member) | X | X | RB |
| Take cover | Z | W | LB |
| Squad: hold position | H | H | — |
| Squad: follow me | G | G | — |
| Mission information | Tab | Tab | Back |
| Scores (multiplayer) | F1 | F1 | — |
| Quick save / quick load | F5 / F9 | F5 / F9 | — |
| Chat / team chat (multiplayer) | T / Y | T / Y | — |
| Torch on/off (P90 with torch; every P90 in the campaign) | L | L | — |
| Quick voice menu (multiplayer) | V | V | — |
| Pause menu | Escape | Escape | Start |
| Console | `` ` `` (left of 1) | `²` or `ù` | — |
| Screenshot | F12 | F12 | — |

Good to know:

- **Screenshot: F12** (row *Screenshot* of the Controls page, to change the key). The pictures are saved in the
  `ScreenShots` folder of your UT2004 install (`<UT2004>\ScreenShots`).
- Items, weapons and ammunition are picked up with **Use**, not by walking over them. Use also opens doors,
  works consoles and revives a downed teammate ("administer first aid").
- **Sprint** drains the stamina bar; it refills when you stop. The double-tap of forward, the 2005 way, still
  works.
- **Squad orders** (single player). While an order is on, the member's plate on the left of the screen shows a
  letter: **F** = fire order, **C** = cover order (a sign, not a key).
  - **Concentrate fire, tap X** with an enemy under the crosshair: the whole squad fires at it. Each member shows
    **F** and a marker sits on the target until it is dead. A tap with no enemy in your sights cancels the fire
    order.
  - **Concentrate fire, hold X**: the squad menu opens (CLEAR ORDER and the members' names). The mouse wheel
    (controller: d-pad up / down) picks a member. Release X on an enemy: only that member attacks it, with his or
    her special attack or a grenade. Release X with no enemy in your sights: that member waits up to 45 seconds
    for your next X tap on an enemy. Release X on **CLEAR ORDER**: every fire order is cancelled.
    Another way to pick one member (the tutorial's): aim at him or her and tap X, then tap X on the enemy.
  - **Take cover** (Z, AZERTY W): the whole squad looks for cover and shows **C**; press it again to leave cover.
    With the crosshair on one member, only that member takes cover.
  - **Hold position** (H): each member stays where he or she stands (a yellow arrow marks each spot) and fights
    from there while you move on. **Follow me** (G) cancels it and the squad comes back to you.
    A hold order is kept by saves and quick saves; the next mission starts with the squad following you. These two
    orders had no key in 2005 (they were only console commands); the controller has no button for them, one can
    be given on the Controls page (d-pad right is free).
  - **First aid**: a knocked-out teammate calls for help; walk up to him or her and press **E** (Use) while
    "administer first aid" shows (about 2 seconds).
- The **cloak** needs a shield belt; it does not work while sprinting, and the squad cloaks with you.
- **Grenades** have no key of their own (as in 2005): select them with 4 (or the wheel), then fire to throw.
- The **Zat gun** and the **ribbon device** fire about two shots on a full charge, then recharge (full in 6 seconds);
  the charge shows at the top right as a bar and a percentage. The **staff weapon** charges while you hold fire.
- Weapons with a magazine show **clip / reserve** under the weapon name at the top right (for example `50 / 250`:
  50 rounds in the clip, 250 spare); the bar is the clip too. Grenades and C4 show how many you have.

### Changing keys

On the Controls page, *Keyboard Layout* switches between the QWERTY (WASD) and AZERTY (ZQSD) presets. In the
action list: Enter or a double click, then press the new key or mouse button (Escape cancels); Delete removes an
action's keys; Insert restores the layout's defaults. A key taken from another action is moved, and the page says
so. Escape always opens the pause menu, so it cannot be lost. Changes apply at once.

### Controller

An Xbox-style controller (Xbox 360, One or Series) uses the 2005 layout above.

- The game turns the controller on by itself at start when it finds one. A controller switched on after the game
  started is not seen: use Options → Controls → Controller → **Detect (restart)**, which restarts the game to find it.
- Options → Controls, right-hand column: **Controller** Off / On / Detect (restart), **Pad Look Speed** (1.0 = the original
  game) and **Invert Pad Look**.
- All menus work with the controller, and prompts and hints name the controller buttons while you use it.
- Limits (the game reads controllers through DirectInput): pressing **LT and RT together cancels both**, there
  is **no rumble**, and only the first game controller Windows lists is read.
- If the triggers are swapped, add `bSwapTriggers=True` under `[SGShim.SGPadInfo]` in
  `<UT2004>\SGAlliance\System\SGAllianceUser.ini` (game closed).

## Options

**Options** (main menu), also reachable from the pause menu. Video and Audio changes are applied
with *Save* (Enter).

### Video

| Row | Values | Notes |
|---|---|---|
| View Point | First Person, Third Person | kept across levels |
| Resolution | the modes your screen supports | any aspect ratio: the original 4:3 layout is scaled, not stretched |
| Display | Windowed, Full Screen | full screen is borderless and uses the desktop refresh rate |
| Frame Rate Limit | 30 to 240, Unlimited | see [Performance](#performance) |
| Vertical Sync | Off, On | |
| Field of View | 80 to 120 | 90 is the game's own value |
| Widescreen FOV | Hor+, Off | Hor+: wide screens see more at the sides |
| Texture Detail | UltraLow to UltraHigh | |
| Brightness | 10 to 100 | 50 (default) = the picture as made; with Direct3D 9, only in full screen |
| Renderer | Direct3D 9, OpenGL, Direct3D 11 | Direct3D 9 (default) is the original renderer; Direct3D 11 is experimental: anti-aliasing with the bloom, but known glitches ([known issues](KNOWN_ISSUES.md)); applies at the next start (saving offers *Restart now* or *Later*) |
| Anti-Aliasing | Off, 2x, 4x, 8x | Direct3D 11 or OpenGL only; with Direct3D 11 the bloom stays on; applies at the next start (saving offers *Restart now* or *Later*) |
| Texture Filtering | Bilinear, Trilinear, Anisotropic 2x to 16x | |
| Shadows | On, Off | character, tree and scenery shadows (bullet and scorch marks and the torch light stay); applies at once, or from the next level load if the level started with Off |
| World Detail | High, Low | dynamic lights, light coronas, decals, foliage, detail textures; from the next level load |
| Bloom | On, Off | the 2005 build's glow around bright lights and the blur behind the pause menu, plus the soft glow of lights and consoles in the late missions (Perception's PC emissive effect); applies at once. Direct3D 9 and Direct3D 11: with OpenGL the row shows Off |
| Scope Depth of Field | Off, On | in the sniper scope and the binoculars, what the crosshair points at stays sharp and nearer and farther things are softly blurred (Perception's PC effect); off by default; applies at once. Direct3D 9 and Direct3D 11 |

### Audio

| Row | Values | Notes |
|---|---|---|
| Music Volume, Voice Volume, FX Volume | 0 to 1 | kept across launches |
| 3D Audio (HRTF) | Auto, Off, On | headphone 3D sound; applies at the next start (saving offers *Restart now* or *Later*) |
| Sound Channels | 32, 64, 128 | applies at the next start (saving offers *Restart now* or *Later*) |

### Controls

Keyboard Layout, the action list ([Changing keys](#changing-keys)), Mouse Sensitivity, Invert Mouse, Mouse
Smoothing (Off = raw mouse movement), and the controller rows ([Controller](#controller)).

## Difficulty

**Options → Difficulty**: Easy, Medium, Hard or Insane. The default is **Hard**, the 2005
default. The 2005 menus had no way to change it; the four levels are complete in the game's data. The choice is
kept and applies from the next level start, restart or load. As in the original game, it also
changes the strength of your allies.

## Saves

As in 2005, the game saves **at checkpoints**. On PC you can also **quick save** at any time (there is still no
save menu).

- "Checkpoint reached" appears when the game saves. A save is also made when a new part starts.
- **Quick save: F5**, **quick load: F9** (Options → Controls changes the keys). "Quick Saving"
  appears when the game saves. A quick load puts you back where you saved, with your health, weapons and
  ammunition, the enemies you had killed still dead, the doors as you left them and the level's scripted events
  carrying on from where they were. The previous quick save is kept as a backup.
- F9 also works on the pause menu and on the MISSION FAILED page.
- No quick save during a cutscene or a scripted scene that holds you in place ("Cannot quick save now"), and none
  in multiplayer.
- To go back to a checkpoint: *Retry* on the MISSION FAILED page, or **Single Player → Load Game**, which also
  lists the quick save ("Quicksave: Current") and its backup ("Quicksave: Backup").
- *Restart* (pause menu) and *Restart Chapter* start the current part from its beginning.
- Saves are kept by updates and by the uninstaller (see [Uninstall in detail](#uninstall-in-detail)).
- The checkpoint files of the Xbox build (`.sgs`) cannot be loaded.

## Multiplayer

**Multi-Player** offers **LAN** and **Internet** (the 2005 System Link and Xbox Live
pages). The 2005 *Split-Screen* and *Edit Game Modes* buttons are hidden: neither has a page in the 2005 build.

- **LAN → Host Game**: game mode, team (team modes), character, map, bots. The game stays on your local network.
- **LAN → Join Game**: the list of games on your network (it updates itself while it is open), then team and
  character.
- **Internet**: *Create Match* hosts a game listed on OldUnreal's master servers; *Find Match* looks for games there.
  Both server lists (LAN and Internet) show each game's server name, map, game type and players.
- **Options → Multiplayer**: your character, your **Name** in multiplayer games (*Player*
  unless you type another; *Player Name (Ins)* or pad Y opens the on-screen keyboard) and an **Outfit**: standard, desert or
  black uniform for O'Neill, Carter, Jackson, Teal'c and Graham Coulder (bots wear a random one). The same *Outfit*
  and *Name* rows are on the character page when you host or join a game; changes there are kept.
  On that page a click selects a character; **Start** at the bottom right (**Next** when hosting), Enter or a
  double-click confirms.
- **Pack** (same pages, under *Outfit*): the weapons you start with. Its contents show in the box under the rows
  (icons and names); each side remembers its own pack. Tau'ri characters (SG-1, Walter, Coulder, Tok'ra) keep the
  2005 pistol and add: *Assault* = P90 + frag grenades, *Close Quarters* = Shotgun + C4, *Marksman* = Sniper rifle +
  frag grenades, *Zat* = Zat gun + frag grenades, *Staff* = Staff weapon + frag grenades. Goa'uld characters (Jaffa,
  Goa'uld; in team games your team decides) have no pistol: *Warrior* = Staff weapon + shock grenades, *Zat* = Zat
  gun + shock grenades, *Lord* = Ribbon device + personal shield + Zat gun (no grenades). The Stinger and the shield
  are also found on the maps. Bots take a random pack of their side; a server can keep the 2005 start, the pistol
  only, for everyone.
- **Change Character** (Escape during a multiplayer game): the same page, to change character, outfit, name and pack
  (in team games, among your team's characters). **Apply** puts you back at a spawn point at once with the new
  choice; no death, score or life is counted. If you were hit in the last 5 seconds, carry a flag, drive a vehicle
  or are dead, the change applies at your next respawn (a message says so).

Modes and maps (ten maps: seven deathmatch, three capture the flag):

| Mode | Maps | Win |
|---|---|---|
| DeathMatch | DM maps | 30 frags |
| Team DeathMatch | DM maps | the frag limit (team kills count for the team) |
| Capture the Flag | CTF-Abydos, CTF-LostCity, SGCTF-AbydosVsSGC | 5 captures |
| Last Man Standing | DM maps | five lives each: the last player with lives left wins |

Eleven characters can be played (SG-1, the SGC, the Tok'ra, a Goa'uld and three Jaffa). Teams are the Stargate
Team and the Jaffa Team. *System Lord*, listed in 2005, is hidden: its game code is not in the build.

How a match runs (2005 rules):

- A match starts when **at least two players** are in (bots count); each player presses **Fire** to be ready. A
  host alone without bots waits.
- Weapons, health and shields are picked up with **Use**.
- After a team match, one more round is played, then the next map loads.
- Hold **Tab** (Back on the controller) to see the players and scores; F1 also shows them.
- **Chat**: press **T** to talk to everyone, **Y** to talk to your team (Options → Controls changes
  the keys). A typing line opens at the bottom left: **Enter** sends, **Escape** cancels. Messages show under your
  portrait for 10 seconds, the sender's name in their team's colour, team messages marked *(Team)*; while you type,
  the last messages show again. Dead players and spectators can chat too. Without teams (Deathmatch, Last Man
  Standing) team chat goes to everyone, as in UT2004. The console's `say` / `teamsay` still work.
- On a server with a Discord feed (our public servers have one), messages to everyone are also posted in that
  server's Discord channel with your player name; team chat never is.
- **Quick voice menu: V** (Controls row *Voice Menu*). Your character says the line in their own 2005 voice, heard
  by the players nearby, and its text shows in the chat (to your team in team games, except taunts). Pick with
  the number keys or a click (move the mouse to show the cursor); Escape or V closes; you can keep moving. The
  menu offers only the lines your character has in the 2005 game: Taunt, Affirmative, Negative, Take cover,
  Concentrate fire, Ready for SG-1 (Jackson has no Affirmative / Negative, Teal'c no Ready), Taunt, Attack! and Enemy spotted for
  the Jaffa (their own combat shouts); Coulder, Walter, the Tok'ra and the Goa'uld have no voice lines. One line every 3 s, a taunt every
  6 s; not while dead.

To play together, everyone needs **the same Redial version and the same OldUnreal build**; otherwise joining
fails (the server lists dim a server of another version). To host on the Internet behind a router, forward UT2004's usual ports (UDP 7777 and 7778) to your PC and
let UT2004 through the Windows firewall. To run a dedicated server (Windows or Linux), see [SERVER.md](SERVER.md).

### Play with bots, host a game

Bots are computer players. They are not in the 2005 build; the port adds them in DeathMatch, Last Man Standing,
Team DeathMatch and Capture the Flag (SG-1 against the Jaffa in the two team modes). In Capture the Flag they
attack the enemy flag, defend their base, bring their flag back and escort their flag carrier.

- **Alone with bots**: Multi-Player → LAN → Host Game, then pick a mode, a team (team modes), a character and a
  map. Under the map list, set **Bots** (None to 15) and **Bot Skill** (from 0 Very Easy to 7 Elite; 6 Expert by
  default), then click the map or press Enter (A on the controller). When the level has loaded, press **Fire**:
  the match starts with the bots, without waiting for another player.
- Your last choice is remembered: the next time, just pick the map.
- **With friends on your network**: the same Host Game. Your friends choose LAN → Join Game. When a player joins,
  a bot leaves (at its next death), so the number of players stays the same; when a player leaves, a bot comes
  back.
- **On the Internet**: Multi-Player → Internet → *Create Match*, then the same pages. Your game is listed on
  OldUnreal's master servers (open the ports as said above). To join a game: *Find Match*, then pick a server in the
  list. When no game is found, the 2005 message "No matching games were found" takes you back.
- **During the match**, the host can type in the console: `AddBots 2` (two more bots), `KillBots 1` (one bot fewer;
  `KillBots` alone removes them all), `SetBotSkill 4` (the skill of every bot).

## Updating and uninstalling

- **Update when the game starts**: the **Stargate Redial - The Alliance** shortcut first asks GitHub whether a
  newer version exists (2 seconds at most; nothing about you is sent). Online games need the same version on
  both sides, so when there is one a window offers *Update*, *Later* or *Skip this version*. *Update* downloads
  it, checks its signature (a file that does not verify is deleted and nothing is installed) and opens the new
  installer, which updates the game with your options and offers *Play*. If you deleted the work folder, the
  window asks for the `.7z` again. To turn the check off, untick *Check for updates when the game starts* in the
  installer (or install with `--no-update-check`).
- **Update by hand**: download the new installer zip, extract it and run **Stargate Redial Setup.exe** again: it
  shows *Update v0.1 → v0.2*. Do not uninstall first. Your keys, settings and saves are kept, and only
  what changed is rebuilt. Details: [Updating in detail](#updating-in-detail).
- **Uninstall**: run **Stargate Redial Setup.exe** and click *Uninstall…* on its last step. It removes exactly
  the files the installer wrote; saves, screenshots, logs and your own files stay (tick *Also delete my saves…*
  to delete the saves too). Details: [Uninstall in detail](#uninstall-in-detail).
- The installer's work folder `%LOCALAPPDATA%\SGAlliance-build` (several GB, kept to make updates faster) and
  its download cache `%LOCALAPPDATA%\Stargate-Redial\downloads` are not removed by the uninstaller: delete them
  by hand if you no longer need them.

## Troubleshooting

### Installer

| Message or problem | What to do |
|---|---|
| "install the latest OldUnreal patch", "this 3374 build is too old" | Install the latest OldUnreal patch over UT2004 (link above), then run the installer again. |
| "UT2004 was not found" | Click *Browse…* on the *UT2004 folder* step and choose the folder that holds `System\UT2004.exe`. No UT2004 yet: the window links to OldUnreal's full-game installers, then to the patch. |
| The `.7z` is not found, "not the archive.org release", "SHA-256 mismatch" | Download the archive again from archive.org: the file must be exactly 1,015,500,550 bytes. Do not repack it. |
| "the release files do not match the 2005-12-15 release" | Your extracted folder was changed or is incomplete: give the installer the `.7z` instead. |
| "close … first" | Quit the game, UCC or UnrealEd started from the UT2004 folder the message names, then run the installer again. Copies running from other folders do not count. |
| "not enough space" | Free some space, or choose another work folder under *More options* (`--workdir <folder>` on the command line). |
| "could not fetch a third-party program" | Check the Internet connection or firewall. |
| "Access is denied" or a permission error | UT2004 is in a protected folder (such as Program Files): install UT2004 in a folder your user can write to. |
| The installer stopped or the PC was switched off | Run it again: it resumes, and the mod folder is never left half-installed. *Cancel* in the window is safe at any time. |
| "The update was not installed" (when the game starts) | The game starts with your version. A file without a valid signature is never installed: get the zip by hand from the Releases page. Log: `%LOCALAPPDATA%\Stargate-Redial\logs\update.log`. |

The installer's logs are in `%LOCALAPPDATA%\SGAlliance-build\logs` (the window's *Open the log folder* button
opens it; `installer-window.log` there is everything the window showed). The game's log is
`<UT2004>\System\UT2004.log`.

### Game

- **The screen is black, the picture is wrong, or the game does not start after a video change**: run the
  installer again with `--reset-video` (back to the default video settings: Direct3D 9).
- **Black screen or an error at start after choosing Direct3D 11**: on a PC without Direct3D 11 the installer and
  the game's shortcut go back to Direct3D 9 by themselves, and after a start that failed on Direct3D 11 the
  shortcut starts the next one on Direct3D 9. If the screen still stays black, close the game (Alt+F4), open
  `<UT2004>\SGAlliance\System\SGAlliance.ini` with Notepad and, under `[Engine.Engine]`, replace
  `RenderDevice=D3D11Drv.D3D11RenderDevice` with `RenderDevice=D3D9Drv.D3D9RenderDevice`.
- **Window or full screen**: Video → Display. To start in a window, close the game and set
  `StartupFullscreen=False` under `[WinDrv.WindowsClient]` in `<UT2004>\SGAlliance\System\SGAlliance.ini`.
- **The movement keys are in the wrong place**: Options → Controls → Keyboard Layout, or run the installer with
  `--keyboard azerty` (or `qwerty`) and `--reset-keys`.
- **The controller does nothing**: Options → Controls → Controller On, or Detect (restart) if it was switched on after the
  game started. Other controllers than Xbox-style ones may need Steam Input or a similar tool.
- **Too dark**: Brightness on the Video page. With Direct3D 9 it only works in full screen; OpenGL and
  Direct3D 11 also apply it in a window.
- **A mission seems stuck**: a teammate may be stuck somewhere, or a scripted event did not start. Try the last
  checkpoint (pause menu → Restart, or Load Game). The `assemblemembers` console command brings your squad to
  you ([cheats](CHEATS.md)). See also [known issues](KNOWN_ISSUES.md).
- **Multiplayer: the game is not listed**: let UT2004 through the Windows firewall (private networks for LAN),
  and check that every player has the same version.
- **Multiplayer: a server is dimmed and marked "v0.1.1 required" (or "Other version")**, or joining it says "This
  server runs Stargate Redial v... You have v...": you and the server run different Redial versions. Servers never
  send the game's files. If the server is newer, restart the game with its shortcut (it offers the newest version);
  if it is older, wait for its update. UT2004's "Downloading package '...' failed: Server refused to send '...'"
  has the same cause (or a different OldUnreal build).

### Performance

- **Frame Rate Limit**: 144 or 240 rather than *Unlimited*. Vehicle physics lose a little speed at very high
  frame rates. *Vertical Sync* removes tearing.
- **Renderer**: Direct3D 9 (the default) and Direct3D 11 draw the bloom, the pause blur and the sniper scope's
  lens; they cost a little (about half a millisecond per frame at 1080p on a recent PC). Direct3D 11
  (experimental) adds anti-aliasing at about the same frame rate on a recent PC. OpenGL also has anti-aliasing,
  but no bloom.
- **Scope Depth of Field** costs about 1.5 ms per frame, only while you look through the scope or binoculars.
- On a slow PC: *World Detail* Low, *Shadows* Off, a lower resolution or *Texture Detail*.
- On a laptop, make sure Windows runs UT2004 on the dedicated graphics card.

### Reporting a problem

Open an issue on the [GitHub repository](https://github.com/Stargate-Redial/alliance-redial/issues) with the
version (V0.1), what you did, what you saw, and `<UT2004>\System\UT2004.log` (and the installer's logs for an
installation problem). Check [KNOWN_ISSUES.md](KNOWN_ISSUES.md) first.

## Français

Comment installer et jouer à *Stargate SG-1: The Alliance — Redial* **V0.1**. Le portage vise à jouer comme
la version Xbox de décembre 2005 ; chaque différence voulue est listée dans [CHANGELOG.md](../CHANGELOG.md) (en
anglais). Autres documents : [README](../README.md#français) (présentation courte), [détails de l'installeur](#détails-de-linstalleur) (options, fichiers
écrits, mises à jour), [problèmes connus](KNOWN_ISSUES.md#français), [codes de triche et commandes console](CHEATS.md#français).

Sommaire : [Installation](#installation) · [Détails de l'installeur](#détails-de-linstalleur) · [Premier lancement](#premier-lancement) · [Les menus](#les-menus) ·
[Commandes](#commandes) · [Les options](#les-options) · [Difficulté](#difficulté) · [Sauvegardes](#sauvegardes) ·
[Multijoueur](#multijoueur) · [Mise à jour et désinstallation](#mise-à-jour-et-désinstallation) ·
[Dépannage](#dépannage)

### Installation

#### Ce qu'il faut

- **Windows 64 bits** (testé sous Windows 11).
- **Unreal Tournament 2004** pour Windows, votre propre copie, avec la **dernière version du patch OldUnreal**
  installée par-dessus : build 3374 du 2026-10-20 ou plus récent, sur
  <https://github.com/OldUnreal/UT2004Patches/releases> (suivez les instructions de cette page). L'installeur
  refuse les builds plus anciens.
- **Les fichiers du jeu** : la publication de 2019 du prototype, `Stargate_SG-1_-_The_Alliance-2005-12-15.7z`
  (environ 1 Go), sur <https://archive.org/details/StargateSG1TheAlliance20051215>. Inutile de la décompresser.
- **L'installeur** : `Stargate-Redial-Alliance-v0.1-win64.zip` sur la
  [page Releases](https://github.com/Stargate-Redial/alliance-redial/releases).
- Environ **9 Go** d'espace libre et une **connexion Internet** pendant l'installation (des programmes d'aide
  sont téléchargés depuis leurs pages officielles et vérifiés par leur empreinte).

#### Étapes

1. Clic droit sur le zip de l'installeur, *Propriétés*, cochez *Débloquer*, *OK*. Décompressez-le ensuite où
   vous voulez, par exemple sur le bureau.
2. Double-cliquez sur **Stargate Redial Setup.exe**, ou déposez le `.7z` dessus. La fenêtre de l'installeur
   s'ouvre (en français quand Windows est en français ; un lien change la langue).
   - **Fichiers du jeu** : elle trouve le `.7z` dans Téléchargements, sur le bureau ou à côté de l'installeur.
     Sinon, cliquez sur *Parcourir…* (ou *Utiliser un dossier décompressé…*), ou déposez le fichier sur la
     fenêtre.
   - **Dossier UT2004** : elle trouve UT2004 par le registre et Steam. Sinon, cliquez sur *Parcourir…* et
     choisissez le dossier qui contient `System\UT2004.exe`. Si le patch OldUnreal manque ou est trop ancien, la
     fenêtre l'indique avec un lien vers la page du patch.
   - **Installation** : *Mettre un raccourci sur le bureau* est cochée (décochez-la si vous n'en voulez pas ; le
     menu Démarrer en reçoit toujours un), laissez cochée *Vérifier les mises à jour au lancement du jeu* (voir
     *Mise à jour et désinstallation*), puis cliquez sur *Installer*.
3. Patientez. La fenêtre coche chaque étape et montre l'avancement et le temps restant : environ 3 minutes sur
   un PC à 8 cœurs, 5 à 6 minutes avec 4 cœurs, plus l'extraction de l'archive. *Annuler* arrête proprement.
4. Cliquez sur **Jouer**. Plus tard, lancez **Stargate Redial - The Alliance** depuis le menu Démarrer ou le
   bureau (ou dans `<UT2004>\SGAlliance`). Pendant la partie, son bouton dans la barre des tâches porte le nom et
   l'icône de Redial.

Le jeu est installé comme un mod d'UT2004 : votre UT2004 lui-même n'est pas modifié. La disposition de votre
clavier (QWERTY ou AZERTY) est détectée, et une manette de type Xbox est activée (le jeu le fait aussi tout seul au démarrage).

#### Avertissements de Windows

L'installeur n'est pas signé (un projet de fans ne peut pas acheter de certificat).

- **SmartScreen** peut afficher « Windows a protégé votre ordinateur » : cliquez sur *Informations
  complémentaires*, puis *Exécuter quand même*. Il peut poser la question pour **Stargate Redial Setup.exe** ; la
  fenêtre lance ensuite `app\tools\sgredial.exe`, pour lequel la question peut aussi être posée.
- **Contrôle intelligent des applications** (Windows 11) : s'il est activé, les programmes non signés sont
  bloqués sans exception possible, et l'installeur ne peut pas s'exécuter. Le désactiver est votre décision ;
  sur certaines versions de Windows 11, il ne peut plus être réactivé sans réinstaller Windows.
- **Antivirus** : certains signalent l'installeur, parce que c'est un programme Python compilé. Comparez le
  SHA-256 du zip avec le fichier `.sha256` de la page Releases ; s'il correspond, restaurez le fichier et
  autorisez-le.

### Détails de l'installeur

Les chiffres exacts, les options de l'installeur, ce qu'il écrit sur votre PC, et le fonctionnement des mises à
jour et de la désinstallation.

#### Détails du téléchargement

- **L'installeur** : `Stargate-Redial-Alliance-v<version>-win64.zip` sur la
  [page Releases](https://github.com/Stargate-Redial/alliance-redial/releases) (le fichier `.sha256` à côté
  donne son SHA-256).
- **Les fichiers du jeu** : `Stargate_SG-1_-_The_Alliance-2005-12-15.7z` (1 015 500 550 octets, SHA-256
  `d70e15d5ceb479bb8443f2c0bcf2d8884f913a02033d7d8a8e33f80e622d47f4`), sur
  <https://archive.org/details/StargateSG1TheAlliance20051215>.
- **UT2004** avec la **dernière version du patch OldUnreal** : build 3374 du 2026-10-20 ou plus récent, sur
  <https://github.com/OldUnreal/UT2004Patches/releases> ; les builds 3374 plus anciens sont refusés (le portage
  utilise le champ de vision Hor+ des écrans larges du build récent). Pas encore UT2004 : l'installeur complet
  d'OldUnreal, <https://www.oldunreal.com/downloads/ut2004/full-game-installers/>.
- Rien d'autre : ni Python, ni ffmpeg, ni 7-Zip. L'installeur a besoin d'Internet : il télécharge depuis sa page
  officielle, en vérifiant son SHA-256, un ffmpeg pour l'audio (environ 28 Mo, une seule fois). Prévoyez environ
  9 Go d'espace libre (dossier de travail jusqu'à 6,5 Go, mod 2,5 Go).

#### Détails de l'installation

- Astuce : clic droit sur le zip, *Propriétés*, cochez *Débloquer*, *OK*, puis décompressez : Windows affiche
  alors moins d'avertissements.
- Vous pouvez déposer le `.7z` sur **Stargate Redial Setup.exe**. La fenêtre vérifie le fichier (taille et
  SHA-256), trouve UT2004 par le registre et Steam, et signale un patch OldUnreal absent ou trop ancien.
- *Afficher les détails* montre les messages de l'installeur. Comptez environ 3 minutes sur un PC à 8 cœurs et 5
  à 6 minutes avec 4 cœurs, plus l'extraction de l'archive. *Annuler* arrête proprement : rien n'est laissé à
  moitié installé, et relancer l'installeur reprend là où il s'est arrêté.
- La fenêtre s'affiche en français quand Windows est en français, en anglais sinon (un lien change la langue).
- Avertissement d'antivirus : l'installeur est un programme Python compilé avec Nuitka, un type de fichier que
  certaines heuristiques d'antivirus n'aiment pas. Comparez le SHA-256 du zip avec celui de la page Releases.
- Les parties en ligne passent par le serveur maître d'OldUnreal (la liste vient de votre `Default.ini`
  OldUnreal) ; les parties en réseau local utilisent la découverte LAN d'UT2004.

#### Options de l'installeur (ligne de commande)

La fenêtre propose les choix habituels. Pour toutes les options, lancez le programme de l'installeur depuis une
invite de commandes, dans le dossier décompressé ; il fonctionne exactement comme la fenêtre, avec une sortie
texte :

```bat
app\tools\sgredial.exe --archive "D:\Downloads\Stargate_SG-1_-_The_Alliance-2005-12-15.7z" --dry-run
app\tools\sgredial.exe --help
```

| Option | Effet |
|---|---|
| `--archive <7z>` / `--extracted <dossier>` | l'archive de la publication, ou le dossier où vous l'avez déjà décompressée (chaque fichier est vérifié) |
| `--ut2004 <dossier>` | votre dossier UT2004, s'il n'est pas trouvé |
| `--workdir <dossier>` | dossier de travail (par défaut `%LOCALAPPDATA%\SGAlliance-build`, plusieurs Go) |
| `--dry-run` | vérifie les prérequis et l'archive, affiche le plan, ne change rien |
| `--jobs N`, `--sequential` | moins de processus à la fois, pour garder le PC réactif |
| `--lightmaps runtime` | UT2004 recalcule l'éclairage des niveaux au lieu d'utiliser l'éclairage précalculé du jeu |
| `--skies keep` | garde les textures de ciel de 2005 (par défaut l'installeur lisse leurs blocs de compression et les stocke sans compression) |
| `--desktop-shortcut` | place aussi le lanceur sur votre bureau (le menu Démarrer le reçoit toujours) |
| `--no-update-check` | le raccourci Jouer lance directement le jeu, sans chercher de nouvelle version |
| `--keyboard qwerty\|azerty` | disposition des touches (par défaut d'après le clavier Windows ; la page Options > Controls du jeu peut la changer ensuite) |
| `--gamepad on\|off` | force la manette activée ou désactivée et enregistre votre choix (sinon le jeu active une manette trouvée au démarrage) |
| `--reset-keys` (ou `--reset-video`, `--reset-pad`) | rétablit les touches, les réglages vidéo ou la disposition de la manette par défaut ; sinon installations et mises à jour gardent les vôtres |
| `--verify` | sur un mod installé et à jour : vérifie chaque fichier installé par son SHA-256 |
| `--force` | reconstruit tout ; permet aussi d'installer une version plus ancienne par-dessus une plus récente |
| `--ffmpeg <ffmpeg.exe>`, `--sevenzip <7z.exe>` | les utilise au lieu de les télécharger |
| `--server` (`--server-settings <ini>`, `--server-bundle <fichier>`) | après l'installation, prépare aussi les serveurs dédiés dans `<UT2004>\SGAlliance\Server` (et un paquet pour un serveur Linux) : [SERVER.md](SERVER.md#français) |
| `--uninstall` (`--dry-run`, `--purge-saves`) | voir [Désinstallation en détail](#désinstallation-en-détail) |

#### Ce que l'installeur écrit

Le mod va dans `<UT2004>\SGAlliance` et a son propre `SGAlliance.ini` ; vos réglages UT2004 ne sont pas touchés.
**Une exception :** UT2004 ne lit les fichiers de configuration par classe que dans son propre dossier `System`,
même pour un mod ; l'installeur y copie donc `Tweak_*.ini` (les valeurs de réglage du jeu, environ 137
fichiers), `SGAMusic.ini`, `SGSpeechData.ini`, `SGLipSyncData.ini`, `SGMeshMaterials.ini` et
`SGChapterBriefings.ini`. Le jeu y écrit
ensuite lui-même `SGSpeech.ini` (réglages) et `SGASaves.ini`, `PlayerProfile.ini`, `Stats.ini` (sauvegardes,
réglages, statistiques). Après chaque installation ou mise à jour, l'installeur y fait aussi écrire par l'outil
d'UT2004 la liste des cartes du mod (`SGA-*.ucl`, un par carte : les fichiers que le jeu écrirait sinon à son
premier lancement, qui prenait alors plusieurs minutes) ; la désinstallation les supprime. Aucun fichier d'UT2004
n'est remplacé. Chaque fichier écrit par l'installeur, dans le
dossier du mod et dans `<UT2004>\System`, est listé avec son SHA-256 dans `SGAlliance\.redial\manifest.json` (ceux
de `<UT2004>\System` aussi dans `SGAlliance\installed-outside-mod.txt`). Avec la vérification des mises à jour
(par défaut), `SGAlliance\Launcher` contient une copie du programme de l'installeur (environ 40 Mo), que le
raccourci Jouer lance.

Le mod est d'abord construit dans le dossier de travail, puis copié dans `<UT2004>\SGAlliance` tout à la fin, en
une seule étape annulée si elle est interrompue : une installation échouée ou arrêtée ne laisse jamais un mod à
moitié installé, et relancer l'installeur reprend là où il s'est arrêté. Le dossier de travail garde la
publication extraite et la construction, pour qu'une deuxième exécution ou une mise à jour ne refasse que ce qui a
changé ; vous pouvez le supprimer quand le jeu fonctionne (la mise à jour suivante reconstruira alors tout, ce
qui prend quelques minutes de plus).

#### Mise à jour en détail

**Au lancement du jeu.** Pour jouer en ligne, il faut la même version des deux côtés : le raccourci **Play
Stargate SG-1 The Alliance** demande donc d'abord à GitHub (la page Releases publique du projet) s'il existe une
version plus récente. Rien sur vous ni sur votre PC n'est envoyé : ni compte, ni identifiant, ni cookie,
seulement une simple demande de la dernière version. L'attente est de 2 secondes au plus ; hors ligne, ou sans
nouvelle version, le jeu démarre aussitôt. S'il y en a une, une petite fenêtre montre les nouveautés de cette
version (le texte de la publication sur GitHub, dans la langue de votre Windows s'il existe) et propose *Mettre à
jour*, *Plus tard* ou *Ignorer cette version* (les versions ignorées sont retenues dans
`%LOCALAPPDATA%\Stargate-Redial\update-state.json`). *Mettre à jour* télécharge le nouveau zip, son `.sha256` et
sa signature dans `%LOCALAPPDATA%\Stargate-Redial\updates`, vérifie que c'est bien le fichier signé par le projet
(signature Ed25519 vérifiée avec la clé intégrée à l'installeur ; un fichier qui ne la vérifie pas est supprimé
et rien n'est installé), puis ouvre l'installeur de la nouvelle version, qui met le jeu à jour avec vos options
actuelles et propose *Jouer* à la fin. La mise à jour a de nouveau besoin des fichiers du jeu : le dossier de
travail les garde, sauf si vous l'avez supprimé ; sinon la fenêtre demande le `.7z` (trouvé dans Téléchargements
comme la première fois).

Pour couper cette vérification, décochez *Vérifier les mises à jour au lancement du jeu* dans la fenêtre de
l'installeur (ou installez avec `--no-update-check`) : le raccourci lance alors directement le jeu.
`Stargate Redial - The Alliance.cmd` dans `<UT2004>\SGAlliance` ne vérifie jamais.

**À la main.** À la sortie d'une nouvelle version, téléchargez son zip, décompressez-le (dans un nouveau dossier
ou par-dessus l'ancien) et relancez **Stargate Redial Setup.exe** : la fenêtre affiche *Mettre à jour v0.1 →
v0.2* et reprend vos choix précédents (raccourci bureau, vérification des mises à jour, clavier, manette). Ne
désinstallez pas avant. Le zip et le dossier de la version précédente peuvent être supprimés.

- L'installeur lit la version installée et l'annonce (*Mettre à jour v0.1 → v0.2* ; en ligne de commande
  `updating 0.1 -> 0.2`). Installer une version plus ancienne par-dessus une plus récente demande confirmation
  (`--force` en ligne de commande).
- **Vos données ne sont jamais remplacées** : touches, réglages vidéo, audio et manette, vos autres modifications
  des fichiers de réglages du mod, sauvegardes et points de contrôle, captures, journaux. Les fichiers de
  réglages sont fusionnés : un réglage que vous avez modifié garde votre valeur, sauf si la nouvelle version
  change ce réglage par défaut précis (l'installeur le signale) ; les nouveaux réglages sont ajoutés. Avant toute
  modification, vos réglages et sauvegardes sont copiés dans `SGAlliance\.redial\backups` (les 5 dernières mises
  à jour sont conservées).
- Les fichiers de l'ancienne version absents de la nouvelle sont supprimés (seulement si vous ne les avez pas
  modifiés) ; les fichiers que l'installeur n'a pas écrits ne sont jamais touchés.
- Seul ce qui a changé est reconstruit. Relancer l'installeur sur une version à jour ne fait qu'une vérification
  des fichiers : quelques secondes.
- Si une mise à jour est interrompue (coupure de courant, fenêtre fermée), relancez-la : une copie interrompue
  dans le dossier du mod est d'abord annulée, vous avez donc toujours l'ancienne ou la nouvelle version complète,
  jamais un mélange.
- Les sauvegardes sont conservées telles quelles, et les versions suivantes continuent de lire celles des
  anciennes. Avant une mise à jour, l'installeur liste vos sauvegardes par format et signale toute sauvegarde
  qu'une nouvelle version ne saurait pas charger (elle est conservée et copiée, jamais supprimée). Tout ce qu'il
  faut savoir sur une version est dans [CHANGELOG.md](../CHANGELOG.md).

#### Désinstallation en détail

Lancez **Stargate Redial Setup.exe**, allez à la dernière étape et cliquez sur *Désinstaller…* ; cochez *Supprimer
aussi mes sauvegardes, mes réglages et mes statistiques* seulement si vous le souhaitez. Depuis une invite de
commandes : `app\tools\sgredial.exe --uninstall` (ajoutez `--dry-run` pour voir d'abord chaque fichier,
`--purge-saves` pour supprimer aussi les sauvegardes).

- Il supprime exactement les fichiers listés dans le manifeste (`SGAlliance\.redial\manifest.json`), où qu'ils
  soient, ainsi que les enregistrements de l'installeur. Dans `<UT2004>\System`, il supprime aussi le fichier de
  réglages du jeu `SGSpeech.ini` (et un `SGAlliance.ini` s'il y en a un, créé par le jeu) quand toutes ses
  sections appartiennent à ce mod. Il ne supprime jamais d'après un motif de nom de fichier.
- Les fichiers que l'installeur n'a pas écrits restent, avec les dossiers qui les contiennent : captures
  d'écran, journaux, vos propres fichiers. Le dossier `SGAlliance` n'est supprimé que s'il ne contient plus rien
  d'autre.
- **Les sauvegardes sont conservées** : `SGAlliance\Saves`, `SGASaves.ini`, `PlayerProfile.ini`, `Stats.ini` et
  les copies de secours des mises à jour (`SGAlliance\.redial\backups`) restent. Ajoutez `--purge-saves` pour les
  supprimer aussi.

### Premier lancement

1. Lancez **Stargate Redial - The Alliance**. Le jeu s'ouvre en plein écran à la résolution du bureau, affiche
   l'écran des logos d'origine, puis le menu principal devant une scène de la Porte des étoiles. Le menu
   principal affiche « Stargate Redial V0.1 » dans son coin en bas à droite. L'installeur a déjà préparé la liste
   des cartes du mod ; si UT2004 lui-même n'a jamais été lancé, son premier lancement liste encore une fois ses
   propres cartes, et l'écran des logos reste alors un peu plus longtemps.
2. **Rien à configurer.** Le jeu garde lui-même vos sauvegardes, votre progression, la difficulté, les volumes, les
   touches, les réglages de souris et vos nom, tenue et paquetages en multijoueur ; il n'y a aucun profil à créer ni
   à choisir. (Une installation qui avait déjà des profils continue avec le dernier utilisé ; les autres restent sur
   le disque.)
3. Les menus se pilotent à la souris, au clavier (flèches, Entrée = valider, Échap ou Retour arrière = retour,
   Suppr et Inser pour les autres boutons) et à la manette (croix ou stick gauche, A valider, B retour). Un seul
   élément est en surbrillance : celui sous la souris quand vous la bougez, sinon celui où les touches ou la manette
   l'ont amené ; Entrée agit sur lui. Les boutons en bas d'une page se cliquent et indiquent leur touche :
   **Back (Esc)** à gauche, l'action de la page à droite (**Select (Enter)**, **Load (Enter)**, **Start (Enter)**...).
   Quand vous utilisez une manette, ils montrent ses boutons à la place.

### Les menus

#### Menu principal

- **Continue** charge le checkpoint ou la sauvegarde rapide la plus récente, comme le
  dit son texte d'aide de 2005. Il reste grisé tant qu'il n'y a pas de sauvegarde. (Dans la version de 2005,
  il ouvrait une liste provisoire de toutes les cartes.) Pour lancer n'importe quelle partie de mission, passez par
  Single Player → Chapter Selection. La version n'a pas les missions 1, 3, 5, 6, 8, 9 et 11.
- **Exit Game** quitte le jeu après confirmation, comme Échap.
- **Single Player** :
  - **Continue** fait comme le Continue du menu principal (grisé tant qu'il n'y a pas de sauvegarde).
  - **New Game** demande si vous voulez jouer le didacticiel : *Yes* lance le didacticiel (M00), *No* lance la
    mission 2.
  - **Chapter Selection** liste les 61 parties de l'histoire, sans image de chapitre (les données de 2005 n'en
    ont pas). À gauche, il affiche le briefing de mission de 2005 du chapitre choisi (lieu, heure locale et texte,
    comme l'onglet BRIEFING en jeu) au-dessus de son nom ; M02A-D, M14A-C et M15A n'en ont pas dans les données de
    2005 et n'affichent que leur nom. Les chapitres terminés ont une coche et un nom vert, le chapitre en cours (le plus
    avancé que vous ayez atteint) une flèche dorée et un nom doré, ceux pas encore atteints un nom gris. La liste s'ouvre sur le chapitre en cours ; vous pouvez toujours lancer n'importe lequel. Un clic ne fait que sélectionner un chapitre (son briefing s'affiche à gauche) ; un double-clic, Entrée ou le bouton **Start** le lance. Le menu Single Player
    affiche votre progression, par exemple « Progress: 21 % - chapter 14/61 ».
  - **Load Game** liste vos points de contrôle et la sauvegarde rapide ([Sauvegardes](#sauvegardes)) pour les
    charger.
  - **Tutorial** lance M00.
- **Multi-Player** : voir [Multijoueur](#multijoueur).
- **Options** : Controls, Multiplayer (votre personnage en multijoueur), Video, Audio, Difficulty. Voir
  [Les options](#les-options).
- Le bouton **Extras** de 2005 est masqué : sa page était vide, laissée en attente.
- **Échap** sur le menu principal propose de quitter.

Une mission de l'histoire est une suite de parties (M02A, M02B…) : atteindre la fin d'une partie charge la
suivante. M21D, la dernière, ramène au menu principal.

#### Pendant une mission

- **Échap** (Start à la manette) : le menu pause, avec *Resume Game*, *Restart*, *Options* et *Return to Main
  Menu*.
- **Tab** (Back) : *Mission Information*, avec les onglets *OBJECTIVES* et *BRIEFING* (Page préc. / Page
  suiv., ou la croix ou LB / RB, changent d'onglet).
- **« Press [E] to Skip »** termine aussitôt une cinématique ; le niveau continue comme si vous l'aviez regardée.
- À votre mort, **MISSION FAILED** propose *Retry* (depuis le dernier point de contrôle, si la partie en a un),
  *Restart Chapter* (depuis le début de la partie) et *Load Game*. **F9** y charge aussi votre sauvegarde rapide.
- Les conseils du didacticiel mettent le jeu en pause et nomment vos propres touches.

### Commandes

Les touches se changent dans **Options → Controls**. La colonne manette est la disposition Xbox
d'origine de 2005 (les boutons blanc et noir de la Xbox sont LB et RB, comme sur la Xbox 360).

| Action | Clavier AZERTY | QWERTY | Manette |
|---|---|---|---|
| Se déplacer | Z Q S D, flèches | W A S D, flèches | stick gauche |
| Regarder | souris | souris | stick droit |
| Sprinter | Maj, ou deux appuis rapides sur avancer | pareil | pousser deux fois le stick gauche vers l'avant |
| Sauter | Espace | Espace | A |
| S'accroupir (maintenu / bascule) | Ctrl / C | pareil | — / clic du stick gauche |
| Marcher | Verr. Maj | Verr. Maj | — |
| Tir / tir secondaire | bouton gauche / droit de la souris | pareil | RT / LT |
| Zoom (armes à lunette) | bouton du milieu de la souris | pareil | clic du stick droit |
| Utiliser, ramasser, passer une cinématique | E, Entrée | E, Entrée | X |
| Recharger | R | R | X |
| Arme précédente | A | Q | Y |
| Choix de l'arme | molette, 1 à 0 | pareil | croix haut / bas |
| Lancer une grenade | 4 (grenades), puis tir | pareil | croix jusqu'aux grenades, puis RT |
| Jumelles | B | B | croix gauche |
| Camouflage (il faut une ceinture de bouclier) | F | F | B |
| Tir concentré (maintenu : choisir un équipier) | X | X | RB |
| Se mettre à couvert | W | Z | LB |
| Équipe : tenir la position | H | H | — |
| Équipe : me suivre | G | G | — |
| Informations de mission | Tab | Tab | Back |
| Scores (multijoueur) | F1 | F1 | — |
| Sauvegarde rapide / chargement rapide | F5 / F9 | F5 / F9 | — |
| Discussion / discussion d'équipe (multijoueur) | T / Y | T / Y | — |
| Lampe torche on/off (P90 avec lampe ; tous les P90 de la campagne) | L | L | — |
| Menu vocal rapide (multijoueur) | V | V | — |
| Menu pause | Échap | Échap | Start |
| Console | `²` ou `ù` | `` ` `` (à gauche de 1) | — |
| Capture d'écran | F12 | F12 | — |

Bon à savoir :

- **Capture d'écran : F12** (ligne *Screenshot* de la page Controls, pour changer la touche). Les images sont
  enregistrées dans le dossier `ScreenShots` de votre installation d'UT2004 (`<UT2004>\ScreenShots`).
- Objets, armes et munitions se ramassent avec **Utiliser**, pas en passant dessus. Utiliser ouvre aussi les
  portes, actionne les consoles et ranime un équipier à terre (« administer first aid »).
- **Sprinter** vide la barre d'endurance, qui se recharge à l'arrêt. Le double appui sur avancer, la méthode de
  2005, fonctionne toujours.
- **Ordres à l'équipe** (solo). Tant qu'un ordre est en cours, la plaque de l'équipier, à gauche de l'écran,
  affiche une lettre : **F** = ordre de tir, **C** = ordre de mise à couvert (un repère, pas une touche).
  - **Tir concentré, appui bref sur X** avec un ennemi sous le réticule : toute l'équipe tire dessus. Chaque
    équipier affiche **F** et un repère reste sur la cible jusqu'à sa mort. Un appui sans ennemi visé annule
    l'ordre de tir.
  - **Tir concentré, X maintenu** : le menu de l'équipe s'ouvre (CLEAR ORDER et les noms des équipiers). La
    molette (manette : croix haut / bas) choisit un équipier. Relâchez X sur un ennemi : seul cet équipier
    l'attaque, avec son attaque spéciale ou une grenade. Relâchez X sans ennemi visé : l'équipier attend jusqu'à
    45 secondes votre prochain appui sur X visant un ennemi. Relâchez X sur **CLEAR ORDER** : tous les
    ordres de tir sont annulés. Autre façon de choisir un équipier (celle du tutoriel) : visez-le et appuyez sur X,
    puis appuyez sur X en visant l'ennemi.
  - **Se mettre à couvert** (W, QWERTY Z) : toute l'équipe cherche un abri et affiche **C** ; un nouvel appui
    la fait sortir de couverture. Avec le réticule sur un équipier, lui seul se met à couvert.
  - **Tenir la position** (H) : chaque équipier reste où il est (une flèche jaune marque chaque place) et combat
    de là pendant que vous avancez. **Me suivre** (G) l'annule et l'équipe revient vers vous. L'ordre de tenir la
    position est gardé par les sauvegardes et sauvegardes rapides ; la mission suivante commence avec l'équipe qui
    vous suit. Ces deux ordres n'avaient pas de touche en 2005 (seulement des commandes de console) ; la manette n'a
    pas de bouton pour eux, on peut en donner un sur la page Controls (la croix droite est libre).
  - **Premiers soins** : un équipier à terre appelle à l'aide ; approchez-vous et appuyez sur **E** (Utiliser)
    quand « administer first aid » s'affiche (environ 2 secondes).
- Le **camouflage** demande une ceinture de bouclier ; il ne marche pas en sprintant, et l'équipe se camoufle
  avec vous.
- Les **grenades** n'ont pas de touche à elles (comme en 2005) : choisissez-les avec 4 (ou la molette), puis tirez
  pour lancer.
- Le **zat** et le **ribbon device** tirent environ deux coups avec une charge pleine, puis se rechargent (pleine en
  6 secondes) ; la charge s'affiche en haut à droite, en barre et en pourcentage. La **lance Goa'uld** se charge tant
  que vous maintenez le tir.
- Les armes à chargeur affichent **chargeur / réserve** sous le nom de l'arme, en haut à droite (par exemple
  `50 / 250` : 50 cartouches dans le chargeur, 250 en réserve) ; la barre est aussi le chargeur. Les grenades et le
  C4 affichent leur nombre.

#### Changer les touches

Sur la page Controls, *Keyboard Layout* passe d'un préréglage à l'autre : QWERTY (WASD) ou AZERTY (ZQSD). Dans
la liste des actions : Entrée ou un double-clic, puis appuyez sur la nouvelle touche ou le bouton de souris
(Échap annule) ; Suppr retire les touches d'une action ; Inser rétablit les touches par défaut de la disposition.
Une touche prise à une autre action lui est retirée, et la page le signale. Échap ouvre toujours le menu pause,
on ne peut donc pas le perdre. Les changements s'appliquent aussitôt.

#### Manette

Une manette de type Xbox (Xbox 360, One ou Series) utilise la disposition de 2005 ci-dessus.

- Le jeu active la manette tout seul au démarrage quand il en trouve une. Une manette allumée après le lancement
  n'est pas vue : utilisez Options → Controls → Controller → **Detect (restart)**, qui relance le jeu pour la trouver.
- Options → Controls, colonne de droite : **Controller** Off / On / Detect (restart), **Pad Look Speed** (1.0 = le jeu d'origine) et
  **Invert Pad Look**.
- Tous les menus marchent à la manette, et les invites et conseils nomment les boutons de la manette pendant que
  vous l'utilisez.
- Limites (le jeu lit les manettes par DirectInput) : **LT et RT pressées ensemble s'annulent**, il n'y a **pas
  de vibrations**, et seule la première manette listée par Windows est lue.
- Si les gâchettes sont inversées, ajoutez `bSwapTriggers=True` sous `[SGShim.SGPadInfo]` dans
  `<UT2004>\SGAlliance\System\SGAllianceUser.ini` (jeu fermé).

### Les options

**Options** (menu principal), aussi accessible depuis le menu pause. Les changements Video et Audio
s'appliquent avec *Save* (Entrée).

#### Vidéo

| Ligne | Valeurs | Remarques |
|---|---|---|
| View Point | First Person, Third Person | conservé d'un niveau à l'autre |
| Resolution | les modes de votre écran | tout format d'image : la mise en page 4:3 d'origine est mise à l'échelle, pas étirée |
| Display | Windowed, Full Screen | le plein écran est sans bordure et suit la fréquence du bureau |
| Frame Rate Limit | 30 à 240, Unlimited | voir [Performances](#performances) |
| Vertical Sync | Off, On | |
| Field of View | 80 à 120 | 90 est la valeur du jeu |
| Widescreen FOV | Hor+, Off | Hor+ : un écran large voit davantage sur les côtés |
| Texture Detail | UltraLow à UltraHigh | |
| Brightness | 10 à 100 | 50 (défaut) = l'image telle quelle ; avec Direct3D 9, seulement en plein écran |
| Renderer | Direct3D 9, OpenGL, Direct3D 11 | Direct3D 9 (défaut) est le moteur d'origine ; Direct3D 11 est expérimental : anticrénelage avec le bloom, mais défauts connus ([problèmes connus](KNOWN_ISSUES.md)) ; au prochain démarrage (l'enregistrement propose *Restart now* ou *Later*) |
| Anti-Aliasing | Off, 2x, 4x, 8x | Direct3D 11 ou OpenGL seulement ; avec Direct3D 11, le bloom reste actif ; au prochain démarrage (l'enregistrement propose *Restart now* ou *Later*) |
| Texture Filtering | Bilinear, Trilinear, Anisotropic 2x à 16x | |
| Shadows | On, Off | ombres des personnages, des arbres et du décor (impacts, traces de brûlure et lampe torche restent) ; s'applique tout de suite, ou au prochain chargement de niveau si le niveau a démarré avec Off |
| World Detail | High, Low | lumières dynamiques, halos, impacts, végétation, textures de détail ; au prochain chargement de niveau |
| Bloom | On, Off | le halo lumineux de la version de 2005 et le flou derrière le menu pause, plus la lueur douce des lampes et consoles des dernières missions (effet émissif de la version PC de Perception) ; immédiat. Direct3D 9 et Direct3D 11 : avec OpenGL, la ligne affiche Off |
| Scope Depth of Field | Off, On | dans la lunette du fusil de précision et les jumelles, ce que vise le réticule reste net, l'avant-plan et l'arrière-plan sont légèrement flous (effet de la version PC de Perception) ; désactivé par défaut ; immédiat. Direct3D 9 et Direct3D 11 |

#### Audio

| Ligne | Valeurs | Remarques |
|---|---|---|
| Music Volume, Voice Volume, FX Volume | 0 à 1 | conservés d'un lancement à l'autre |
| 3D Audio (HRTF) | Auto, Off, On | son 3D au casque ; au prochain démarrage (l'enregistrement propose *Restart now* ou *Later*) |
| Sound Channels | 32, 64, 128 | au prochain démarrage (l'enregistrement propose *Restart now* ou *Later*) |

#### Contrôles

Keyboard Layout, la liste des actions ([Changer les touches](#changer-les-touches)), Mouse Sensitivity, Invert
Mouse, Mouse Smoothing (Off = mouvement brut de la souris), et les lignes de la manette ([Manette](#manette)).

### Difficulté

**Options → Difficulty** : Easy, Medium, Hard ou Insane. Par défaut **Hard**, la valeur par défaut
de 2005. Les menus de 2005 ne permettaient pas de la changer ; les quatre niveaux sont complets dans les données
du jeu. Le choix est conservé et s'applique au prochain début de niveau, redémarrage ou
chargement. Comme dans le jeu d'origine, il change aussi la résistance de vos alliés.

### Sauvegardes

Comme en 2005, le jeu sauvegarde **aux points de contrôle**. Sur PC, vous pouvez aussi faire une **sauvegarde
rapide** à tout moment (il n'y a toujours pas de menu de sauvegarde).

- « Checkpoint reached » s'affiche quand le jeu sauvegarde. Une sauvegarde est aussi faite au début de chaque
  partie.
- **Sauvegarde rapide : F5**, **chargement rapide : F9** (Options → Controls pour changer les
  touches). « Quick Saving » s'affiche quand le jeu sauvegarde. Le chargement rapide vous remet où vous aviez
  sauvegardé, avec votre santé, vos armes et vos munitions, les ennemis abattus toujours morts, les portes comme
  vous les aviez laissées et les événements scriptés du niveau repris là où ils en étaient. La sauvegarde rapide
  précédente est gardée en secours.
- F9 marche aussi sur le menu pause et sur la page MISSION FAILED.
- Pas de sauvegarde rapide pendant une cinématique ou une scène scriptée qui vous immobilise (« Cannot quick save
  now »), ni en multijoueur.
- Pour revenir à un point de contrôle : *Retry* sur la page MISSION FAILED, ou **Single Player → Load Game**, qui
  liste aussi la sauvegarde rapide (« Quicksave: Current ») et sa copie de secours (« Quicksave: Backup »).
- *Restart* (menu pause) et *Restart Chapter* recommencent la partie en cours depuis son début.
- Les mises à jour et la désinstallation conservent les sauvegardes (voir
  [Désinstallation en détail](#désinstallation-en-détail)).
- Les fichiers de points de contrôle de la version Xbox (`.sgs`) ne peuvent pas être chargés.

### Multijoueur

**Multi-Player** propose **LAN** et **Internet** (les pages System Link et Xbox Live
de 2005). Les boutons *Split-Screen* et *Edit Game Modes* de 2005 sont masqués : aucun des deux n'a de page dans la
version de 2005.

- **LAN → Host Game** : mode de jeu, équipe (modes en équipe), personnage, carte, bots. La partie reste sur votre
  réseau local.
- **LAN → Join Game** : la liste des parties de votre réseau (elle se met à jour toute seule tant qu'elle est
  ouverte), puis équipe et personnage.
- **Internet** : *Create Match* héberge une partie listée sur les serveurs maîtres d'OldUnreal ; *Find Match* y
  cherche des parties. Les deux listes de serveurs (LAN et Internet) affichent pour chaque partie le nom du serveur,
  la carte, le mode de jeu et les joueurs.
- **Options → Multiplayer** : votre personnage, votre nom en multijoueur (**Name** : *Player*
  sauf si vous en tapez un autre ; *Player Name (Ins)* ou Y à la manette ouvre le clavier à l'écran) et une tenue
  (**Outfit**) : uniforme standard, désert ou noir pour O'Neill, Carter, Jackson, Teal'c et Graham Coulder (les
  bots en portent une au hasard). Les mêmes lignes *Outfit* et *Name* figurent sur la page du personnage quand vous
  créez ou rejoignez une partie ; ce que vous y changez est gardé. Sur cette page, un clic
  sélectionne un personnage ; **Start** en bas à droite (**Next** quand vous hébergez), Entrée ou un double-clic
  valide.
- **Pack** (mêmes pages, sous *Outfit*) : les armes avec lesquelles vous commencez. Son contenu s'affiche dans le
  cadre sous les lignes (icônes et noms) ; chaque camp garde son propre pack. Les personnages Tau'ri (SG-1, Walter,
  Coulder, Tok'ra) gardent le pistolet de 2005 et ajoutent : *Assault* = P90 + grenades à fragmentation, *Close
  Quarters* = fusil à pompe + C4, *Marksman* = fusil de précision + grenades à fragmentation, *Zat* = zat + grenades
  à fragmentation, *Staff* = lance Goa'uld + grenades à fragmentation. Les personnages Goa'uld (Jaffa, Goa'uld ; en
  équipe, c'est votre équipe qui décide) n'ont pas de pistolet : *Warrior* = lance Goa'uld + grenades paralysantes,
  *Zat* = zat + grenades paralysantes, *Lord* = ribbon device + bouclier personnel + zat (sans grenades). Le Stinger
  et le bouclier se trouvent aussi sur les cartes. Les bots prennent un pack au hasard de leur camp ; un serveur peut
  garder le départ de 2005, le pistolet seul pour tous.
- **Change Character** (Échap pendant une partie multijoueur) : la même page, pour changer de personnage, de tenue,
  de nom et de pack (en équipe, parmi les personnages de votre équipe). **Apply** vous remet aussitôt sur un point
  d'apparition avec le nouveau choix, sans mort, score ni vie comptés. Si vous avez été touché dans les 5 dernières
  secondes, portez un drapeau, conduisez un véhicule ou êtes mort, le changement s'applique à votre prochaine
  réapparition (un message le dit).

Modes et cartes (dix cartes : sept de match à mort, trois de capture du drapeau) :

| Mode | Cartes | Victoire |
|---|---|---|
| DeathMatch | cartes DM | 30 frags |
| Team DeathMatch | cartes DM | la limite de frags (les frags comptent pour l'équipe) |
| Capture the Flag | CTF-Abydos, CTF-LostCity, SGCTF-AbydosVsSGC | 5 captures |
| Last Man Standing | cartes DM | cinq vies chacun : le dernier joueur à qui il reste des vies gagne |

Onze personnages sont jouables (SG-1, le SGC, la Tok'ra, un Goa'uld et trois Jaffa). Les équipes sont la
Stargate Team et la Jaffa Team. *System Lord*, listé en 2005, est masqué : son code n'est pas dans la version.

Déroulement d'un match (règles de 2005) :

- Un match commence quand **au moins deux joueurs** sont là (les bots comptent) ; chacun appuie sur **Tir** pour
  être prêt. Un hôte seul sans bots attend.
- Armes, santé et boucliers se ramassent avec **Utiliser**.
- Après un match en équipe, une manche de plus est jouée, puis la carte suivante se charge.
- Maintenez **Tab** (Back à la manette) pour voir les joueurs et les scores ; F1 les affiche aussi.
- **Discussion** : appuyez sur **T** pour parler à tout le monde, **Y** pour parler à votre équipe (Options →
  Controls change les touches). Une ligne de saisie s'ouvre en bas à gauche : **Entrée** envoie,
  **Échap** annule. Les messages s'affichent sous votre portrait pendant 10 secondes, le nom de l'auteur dans la
  couleur de son équipe, les messages d'équipe marqués *(Team)* ; pendant la saisie, les derniers messages
  réapparaissent. Les joueurs morts et les spectateurs peuvent aussi discuter. Sans équipes (Deathmatch, Last Man
  Standing), la discussion d'équipe va à tout le monde, comme dans UT2004. `say` / `teamsay` dans la console
  marchent toujours.
- Sur un serveur qui a un fil Discord (c'est le cas de nos serveurs publics), les messages à tout le monde sont
  aussi publiés dans le salon Discord de ce serveur avec votre nom de joueur ; la discussion d'équipe, jamais.
- **Menu vocal rapide : V** (ligne *Voice Menu* de la page Controls). Votre personnage dit la réplique avec sa
  propre voix de 2005, entendue par les joueurs proches, et son texte s'affiche dans la discussion (à votre équipe
  dans les modes en équipe, sauf les provocations). Choisissez avec les touches numériques ou un clic (bougez la
  souris pour faire apparaître le curseur) ; Échap ou V ferme ; vous pouvez continuer à bouger. Le menu ne propose
  que les répliques que votre personnage a dans le jeu de 2005 : Taunt, Affirmative, Negative, Take cover,
  Concentrate fire, Ready pour SG-1 (Jackson n'a ni Affirmative ni Negative, Teal'c pas de Ready), Taunt, Attack! et Enemy spotted
  pour les Jaffa (leurs propres cris de combat) ; Coulder, Walter, le Tok'ra et le Goa'uld n'ont pas de répliques. Une réplique toutes les 3 s,
  une provocation toutes les 6 s ; pas une fois mort.

Pour jouer ensemble, tout le monde doit avoir **la même version de Redial et le même build OldUnreal** ; sinon,
la connexion échoue (les listes de serveurs grisent un serveur d'une autre version). Pour héberger sur Internet derrière une box, redirigez les ports habituels d'UT2004 (UDP
7777 et 7778) vers votre PC et autorisez UT2004 dans le pare-feu Windows. Pour faire tourner un serveur dédié
(Windows ou Linux), voir [SERVER.md](SERVER.md#français).

#### Jouer avec des bots, héberger une partie

Les bots sont des joueurs contrôlés par l'ordinateur. Ils ne sont pas dans la version de 2005 ; le portage les
ajoute en DeathMatch, Last Man Standing, Team DeathMatch et Capture the Flag (SG-1 contre les Jaffa dans les deux modes
en équipe). En Capture the Flag, ils attaquent le drapeau adverse, défendent leur base, rapportent leur drapeau et
escortent leur porteur.

- **Seul avec des bots** : Multi-Player → LAN → Host Game, puis choisissez un mode, une équipe (modes en équipe), un
  personnage et une carte. Sous la liste des cartes, réglez **Bots** (de None à 15) et **Bot Skill** (de 0 Very Easy
  à 7 Elite ; 6 Expert par défaut), puis cliquez sur la carte ou appuyez sur Entrée (A à la manette). Une fois le
  niveau chargé, appuyez sur **Tir** : le match commence avec les bots, sans attendre un autre joueur.
- Votre dernier choix est mémorisé : la fois suivante, choisissez simplement la carte.
- **Entre amis sur votre réseau** : le même Host Game. Vos amis choisissent LAN → Join Game. Quand un joueur
  arrive, un bot s'en va (à sa mort suivante) : le nombre de joueurs reste le même ; quand un joueur part, un bot
  revient.
- **Sur Internet** : Multi-Player → Internet → *Create Match*, puis les mêmes pages. Votre partie est listée sur
  les serveurs maîtres d'OldUnreal (ouvrez les ports comme indiqué plus haut). Pour rejoindre une partie :
  *Find Match*, puis choisissez un serveur dans la liste. Si aucune partie n'est trouvée, le message de 2005
  « No matching games were found » vous ramène en arrière.
- **Pendant le match**, l'hôte peut taper dans la console : `AddBots 2` (deux bots de plus), `KillBots 1` (un bot de
  moins ; `KillBots` seul les retire tous), `SetBotSkill 4` (le niveau de tous les bots).

### Mise à jour et désinstallation

- **Mise à jour au lancement du jeu** : le raccourci **Stargate Redial - The Alliance** demande d'abord à
  GitHub s'il existe une version plus récente (2 secondes au plus ; rien sur vous n'est envoyé). Pour jouer en
  ligne, il faut la même version des deux côtés : s'il y en a une, une fenêtre propose *Mettre à jour*, *Plus
  tard* ou *Ignorer cette version*. *Mettre à jour* la télécharge, vérifie sa signature (un fichier qui ne la
  vérifie pas est supprimé et rien n'est installé) et ouvre le nouvel installeur, qui met le jeu à jour avec vos
  options et propose *Jouer*. Si vous avez supprimé le dossier de travail, la fenêtre redemande le `.7z`. Pour
  couper la vérification, décochez *Vérifier les mises à jour au lancement du jeu* dans l'installeur (ou
  installez avec `--no-update-check`).
- **Mise à jour à la main** : téléchargez le nouveau zip de l'installeur, décompressez-le et relancez
  **Stargate Redial Setup.exe** : il affiche *Mettre à jour v0.1 → v0.2*. Ne désinstallez pas avant. Vos
  touches, réglages et sauvegardes sont conservés, et seul ce qui a changé est reconstruit. Détails :
  [Mise à jour en détail](#mise-à-jour-en-détail).
- **Désinstallation** : lancez **Stargate Redial Setup.exe** et cliquez sur *Désinstaller…* à sa dernière
  étape. Il supprime exactement les fichiers écrits par l'installeur ; sauvegardes, captures, journaux et vos
  propres fichiers restent (cochez *Supprimer aussi mes sauvegardes…* pour les supprimer aussi).
- Le dossier de travail de l'installeur `%LOCALAPPDATA%\SGAlliance-build` (plusieurs Go, gardé pour accélérer
  les mises à jour) et son cache de téléchargement `%LOCALAPPDATA%\Stargate-Redial\downloads` ne sont pas
  supprimés par la désinstallation : effacez-les à la main si vous n'en avez plus besoin.

### Dépannage

#### Installeur

| Message ou problème | Que faire |
|---|---|
| « install the latest OldUnreal patch », « this 3374 build is too old » | Installez la dernière version du patch OldUnreal par-dessus UT2004 (lien plus haut), puis relancez l'installeur. |
| « UT2004 est introuvable » | À l'étape *Dossier UT2004*, cliquez sur *Parcourir…* et choisissez le dossier qui contient `System\UT2004.exe`. Pas encore UT2004 : la fenêtre renvoie vers les installeurs complets d'OldUnreal, puis vers le patch. |
| Le `.7z` est introuvable, « not the archive.org release », « SHA-256 mismatch » | Retéléchargez l'archive sur archive.org : le fichier doit faire exactement 1 015 500 550 octets. Ne la recompressez pas. |
| « the release files do not match the 2005-12-15 release » | Votre dossier décompressé a été modifié ou est incomplet : donnez plutôt le `.7z` à l'installeur. |
| « close … first » | Quittez le jeu, UCC ou UnrealEd lancés depuis le dossier UT2004 que le message indique, puis relancez l'installeur. Les copies lancées depuis d'autres dossiers ne comptent pas. |
| « not enough space » | Libérez de la place, ou choisissez un autre dossier de travail sous *Plus d'options* (`--workdir <dossier>` en ligne de commande). |
| « could not fetch a third-party program » | Vérifiez la connexion Internet ou le pare-feu. |
| « Accès refusé » ou erreur de permission | UT2004 est dans un dossier protégé (comme Program Files) : installez UT2004 dans un dossier où votre utilisateur peut écrire. |
| L'installeur s'est arrêté ou le PC s'est éteint | Relancez-le : il reprend, et le dossier du mod n'est jamais laissé à moitié installé. *Annuler* dans la fenêtre est sans risque à tout moment. |
| « La mise à jour n'a pas été installée » (au lancement du jeu) | Le jeu démarre avec votre version. Un fichier sans signature valide n'est jamais installé : prenez le zip à la main sur la page Releases. Journal : `%LOCALAPPDATA%\Stargate-Redial\logs\update.log`. |

Les journaux de l'installeur sont dans `%LOCALAPPDATA%\SGAlliance-build\logs` (le bouton *Ouvrir le dossier des
journaux* de la fenêtre l'ouvre ; `installer-window.log` y contient tout ce que la fenêtre a affiché). Le journal
du jeu est
`<UT2004>\System\UT2004.log`.

#### Jeu

- **Écran noir, image incorrecte, ou le jeu ne démarre plus après un changement vidéo** : relancez l'installeur
  avec `--reset-video` (réglages vidéo par défaut : Direct3D 9).
- **Écran noir ou erreur au démarrage après avoir choisi Direct3D 11** : sur un PC sans Direct3D 11,
  l'installeur et le raccourci du jeu reviennent à Direct3D 9 d'eux-mêmes, et après un démarrage raté en
  Direct3D 11 le raccourci lance le suivant en Direct3D 9. Si l'écran reste noir malgré tout, fermez le jeu
  (Alt+F4), ouvrez `<UT2004>\SGAlliance\System\SGAlliance.ini` avec le Bloc-notes et, sous `[Engine.Engine]`,
  remplacez `RenderDevice=D3D11Drv.D3D11RenderDevice` par `RenderDevice=D3D9Drv.D3D9RenderDevice`.
- **Fenêtre ou plein écran** : Video → Display. Pour démarrer en fenêtre, fermez le jeu et mettez
  `StartupFullscreen=False` sous `[WinDrv.WindowsClient]` dans `<UT2004>\SGAlliance\System\SGAlliance.ini`.
- **Les touches de déplacement ne sont pas au bon endroit** : Options → Controls → Keyboard Layout, ou relancez
  l'installeur avec `--keyboard azerty` (ou `qwerty`) et `--reset-keys`.
- **La manette ne fait rien** : Options → Controls → Controller On, ou Detect (restart) si elle a été allumée après le
  lancement du jeu. Les manettes qui ne sont pas de type Xbox peuvent demander Steam Input ou un outil semblable.
- **Trop sombre** : Brightness sur la page Video. Avec Direct3D 9, seulement en plein écran ; OpenGL et
  Direct3D 11 l'appliquent aussi en fenêtre.
- **Une mission semble bloquée** : un équipier est peut-être coincé, ou un événement scripté n'a pas démarré.
  Reprenez au dernier point de contrôle (menu pause → Restart, ou Load Game). La commande console
  `assemblemembers` ramène votre équipe près de vous ([triche](CHEATS.md#français)). Voir aussi les
  [problèmes connus](KNOWN_ISSUES.md#français).
- **Multijoueur : la partie n'est pas listée** : autorisez UT2004 dans le pare-feu Windows (réseaux privés pour
  le LAN), et vérifiez que tous les joueurs ont la même version.
- **Multijoueur : un serveur est grisé et marqué « v0.1.1 required » (ou « Other version »)**, ou la connexion
  affiche « This server runs Stargate Redial v... You have v... » : vous et le serveur n'avez pas la même version
  de Redial. Les serveurs n'envoient jamais les fichiers du jeu. Si le serveur est plus récent, relancez le jeu
  avec son raccourci (il propose la version la plus récente) ; s'il est plus ancien, attendez sa mise à jour.
  « Downloading package '...' failed: Server refused to send '...' » d'UT2004 a la même cause (ou un build
  OldUnreal différent).

#### Performances

- **Frame Rate Limit** : 144 ou 240 plutôt qu'*Unlimited*. La physique des véhicules perd un peu de vitesse à
  très haute fréquence d'images. *Vertical Sync* supprime les déchirures d'image.
- **Renderer** : Direct3D 9 (par défaut) et Direct3D 11 dessinent le bloom, le flou du menu pause et la lentille
  de la lunette du fusil de précision ; ils coûtent un peu (environ une demi-milliseconde par image en 1080p sur
  un PC récent). Direct3D 11 (expérimental) ajoute l'anticrénelage, à peu près à la même fréquence d'images sur
  un PC récent. OpenGL a aussi l'anticrénelage, mais pas de bloom.
- **Scope Depth of Field** coûte environ 1,5 ms par image, seulement quand vous regardez dans la lunette ou les jumelles.
- Sur un PC lent : *World Detail* Low, *Shadows* Off, une résolution ou un *Texture Detail* plus bas.
- Sur un portable, vérifiez que Windows lance UT2004 sur la carte graphique dédiée.

#### Signaler un problème

Ouvrez une issue sur le [dépôt GitHub](https://github.com/Stargate-Redial/alliance-redial/issues) avec la version
(V0.1), ce que vous avez fait, ce que vous avez vu, et `<UT2004>\System\UT2004.log` (plus les journaux de
l'installeur pour un problème d'installation). Consultez d'abord [KNOWN_ISSUES.md](KNOWN_ISSUES.md#français).
