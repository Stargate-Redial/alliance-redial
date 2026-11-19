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
   - **Install**: tick *Put a shortcut on the desktop* if you want one, keep *Check for updates when the game
     starts* ticked (see [Updating](#updating-and-uninstalling)), then click *Install*.
3. Wait. The window shows each step with a tick, the overall progress and the time left: about 3 minutes on an
   8-core PC, 5 to 6 minutes on a 4-core one, plus the extraction of the archive. *Cancel* stops safely.
4. Click **Play**. Later, start **Play Stargate SG-1 The Alliance** in `<UT2004>\SGAlliance` (or the desktop
   shortcut).

The game is installed as a UT2004 mod: your UT2004 itself is not changed. Your keyboard layout (QWERTY or
AZERTY) is detected, and an Xbox-style controller connected during the installation is switched on.

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
| `--desktop-shortcut` | also puts the launcher on your desktop |
| `--no-update-check` | the Play shortcut starts the game directly, without checking for a new version |
| `--keyboard qwerty\|azerty` | key preset (default: from your Windows keyboard layout; the game's Options > Controls page can switch it later) |
| `--gamepad on\|off` | an Xbox-compatible pad connected during the install is switched on with the 2005 layout; this forces it |
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
`SGAMusic.ini`, `SGSpeechData.ini`, `SGLipSyncData.ini` and `SGMeshMaterials.ini`. The game itself later writes
`SGSpeech.ini` (settings) and `SGASaves.ini`, `PlayerProfile.ini`, `Stats.ini` (saves, profile, statistics)
there. No UT2004 file is replaced. Every file the installer wrote, in the mod folder and in
`<UT2004>\System`, is listed with its SHA-256 in `SGAlliance\.redial\manifest.json` (the ones in
`<UT2004>\System` also in `SGAlliance\installed-outside-mod.txt`). With the update check (the default),
`SGAlliance\Launcher` holds a copy of the installer program (about 40 MB) that the Play shortcut starts.

The mod is built in the work folder first and copied into `<UT2004>\SGAlliance` only at the very end, in one step
that is undone if it is interrupted: a failed or stopped install never leaves a half-installed mod, and running
the installer again resumes where it stopped. The work folder keeps the extracted release and the build, so that
a second run or an update only redoes what changed; you can delete it once the game works (the next update then
rebuilds everything, which takes a few minutes longer).

### Updating in detail

**When the game starts.** Online games need the same version on both sides, so the **Play Stargate SG-1 The
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
`--no-update-check`): the shortcut then starts the game directly. `Play Stargate SG-1 The Alliance.cmd` in
`<UT2004>\SGAlliance` never checks.

**By hand.** When a new version is released, download its zip, extract it (into a new folder, or over the old one)
and run **Stargate Redial Setup.exe** again: the window shows *Update v0.1 → v0.2* and reuses the options you
chose before (desktop shortcut, update check, keyboard, controller). Do not uninstall first. The previous
version's zip and folder can be deleted.

- The installer reads the installed version and says what it does (*Update v0.1 → v0.2*; on the command line
  `updating 0.1 -> 0.2`). Installing an older version over a newer one asks for confirmation (`--force` on the
  command line).
- **Your data is never replaced**: key bindings, video, audio and controller settings, your other changes to the
  mod's settings files, profiles, saved games and checkpoints, screenshots and logs. Settings files are merged: a
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
profile and statistics* only if you want that. From a command prompt: `app\tools\sgredial.exe --uninstall`
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

1. Start **Play Stargate SG-1 The Alliance**. The game opens in full screen at your desktop resolution, shows
   the original logo screen, then the main menu over a Stargate scene. The main menu shows "Stargate Redial
   V0.1" in its bottom-right corner.
2. **Create a profile.** At the first launch the game opens *Create Profile*: type a name with the keyboard
   (Backspace deletes) or the on-screen keys, choose *Done* (Enter), then *Save* (Ins, or click the prompt, or Y on a
   controller). This profile is now the active one: the game remembers it at the next launch, and Continue, Single
   Player, Multi-Player and Options use it. The main menu's **Profile** button selects another profile (Enter or a
   click), creates one (Ins) or deletes one (Delete). A profile keeps its difficulty, volumes, keys, mouse settings,
   multiplayer name and outfit, and saves.
3. Menus work with the mouse, the keyboard (arrows, Enter = select, Escape or Backspace = back, Delete and Insert
   for the other prompts) and a controller (d-pad or left stick, A select, B back). One item is highlighted at a
   time: the one under the mouse when you move it, else the one the keys or the pad moved to; Enter acts on it. The
   prompt bar at the bottom names the keys of the device you use last.

## Menus

### Main menu

- **Continue** loads the most recent checkpoint or quick save of the profile used last, as its 2005 hint text
  says. It is greyed until the profile has a save. (In the 2005 build it opened a temporary list of every map.)
  To start any mission part, use Single Player → Chapter Selection. The build has no missions 1, 3, 5, 6, 8, 9
  and 11.
- **Exit Game** quits the game after a confirmation, like Escape.
- **Single Player**:
  - **New Game** asks whether you want to play the tutorial: *Yes* starts the tutorial (M00), *No* starts
    Mission 2.
  - **Chapter Selection** lists the 61 parts of the story; it shows no chapter pictures (the 2005 data has none).
  - **Load Game** lists the profile's checkpoints and its quick save ([Saves](#saves)): load or delete them.
  - **Tutorial** starts M00.
- **Multi-Player**: see [Multiplayer](#multiplayer).
- **Options** → **Edit Profile** of the active profile: Controls, Multiplayer (your multiplayer character), Video,
  Audio, Name, Difficulty. See [Options](#options).
- **Profile**: select the active profile, create one or delete one (see [First launch](#first-launch)).
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

Keys can be changed in **Options → Edit Profile → Controls**. The controller column is the original 2005 Xbox
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
| Mission information | Tab | Tab | Back |
| Scores (multiplayer) | F1 | F1 | — |
| Quick save / quick load | F5 / F9 | F5 / F9 | — |
| Pause menu | Escape | Escape | Start |
| Console | `` ` `` (left of 1) | `²` or `ù` | — |
| Screenshot | F12 | F12 | — |

Good to know:

- Items, weapons and ammunition are picked up with **Use**, not by walking over them. Use also opens doors,
  works consoles and revives a downed teammate ("administer first aid").
- **Sprint** drains the stamina bar; it refills when you stop. The double-tap of forward, the 2005 way, still
  works.
- **Concentrate fire**: tap it to make the squad fire at what you aim at; hold it to pick one squad member to
  command. **Take cover** sends the squad to cover.
- The **cloak** needs a shield belt; it does not work while sprinting, and the squad cloaks with you.
- **Grenades** have no key of their own (as in 2005): select them with 4 (or the wheel), then fire to throw.
- The **Zat gun** and the **ribbon device** fire about two shots on a full charge, then recharge (full in 6 seconds);
  the charge shows at the top right as a bar and a percentage. The **staff weapon** charges while you hold fire.

### Changing keys

On the Controls page, *Keyboard Layout* switches between the QWERTY (WASD) and AZERTY (ZQSD) presets. In the
action list: Enter or a double click, then press the new key or mouse button (Escape cancels); Delete removes an
action's keys; Insert restores the layout's defaults. A key taken from another action is moved, and the page says
so. Escape always opens the pause menu, so it cannot be lost. Changes apply at once.

### Controller

An Xbox-style controller (Xbox 360, One or Series) uses the 2005 layout above.

- **Connect it before starting the game**: the game reads the controller it finds at start-up. If you plug it in
  later, restart the game.
- Options → Controls, right-hand column: **Controller** On/Off, **Pad Look Speed** (1.0 = the original
  game) and **Invert Pad Look**.
- All menus work with the controller, and prompts and hints name the controller buttons while you use it.
- Limits (the game reads controllers through DirectInput): pressing **LT and RT together cancels both**, there
  is **no rumble**, and only the first game controller Windows lists is read.
- If the triggers are swapped, add `bSwapTriggers=True` under `[SGShim.SGPadInfo]` in
  `<UT2004>\SGAlliance\System\SGAllianceUser.ini` (game closed).

## Options

**Options → (profile) → Edit Profile**, also reachable from the pause menu. Video and Audio changes are applied
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
| Brightness | 10 to 100 | with Direct3D 9, only in full screen |
| Renderer | Direct3D 9, OpenGL, Direct3D 11 | Direct3D 9 is the original look; applies at the next start |
| Anti-Aliasing | Off, 2x, 4x, 8x | OpenGL or Direct3D 11 only; applies at the next start |
| Texture Filtering | Bilinear, Trilinear, Anisotropic 2x to 16x | |
| Shadows | On, Off | character shadows only (bullet and scorch marks and the torch light stay); applies at once, or from the next level load if the level started with Off |
| World Detail | High, Low | dynamic lights, light coronas, decals, foliage, detail textures; from the next level load |
| Bloom | On, Off | the 2005 build's glow around bright lights and the blur behind the pause menu; applies at once. Direct3D 9 only: with OpenGL or Direct3D 11 the row shows Off |

### Audio

| Row | Values | Notes |
|---|---|---|
| Music Volume, Voice Volume, FX Volume | 0 to 1 | stored in the profile |
| 3D Audio (HRTF) | Auto, Off, On | headphone 3D sound; applies at the next start |
| Sound Channels | 32, 64, 128 | applies at the next start |

### Controls

Keyboard Layout, the action list ([Changing keys](#changing-keys)), Mouse Sensitivity, Invert Mouse, Mouse
Smoothing (Off = raw mouse movement), and the controller rows ([Controller](#controller)).

## Difficulty

**Options → Edit Profile → Difficulty**: Easy, Medium, Hard or Insane. The default is **Hard**, the 2005
default. The 2005 menus had no way to change it; the four levels are complete in the game's data. The choice is
stored in the profile and applies from the next level start, restart or load. As in the original game, it also
changes the strength of your allies.

## Saves

As in 2005, the game saves **at checkpoints**. On PC you can also **quick save** at any time (there is still no
save menu).

- "Checkpoint reached" appears when the game saves. A save is also made when a new part starts.
- **Quick save: F5**, **quick load: F9** (Options → Edit Profile → Controls changes the keys). "Quick Saving"
  appears when the game saves. A quick load puts you back where you saved, with your health, weapons and
  ammunition, the enemies you had killed still dead, the doors as you left them and the level's scripted events
  carrying on from where they were. The previous quick save is kept as a backup.
- F9 also works on the pause menu and on the MISSION FAILED page.
- No quick save during a cutscene or a scripted scene that holds you in place ("Cannot quick save now"), and none
  in multiplayer.
- To go back to a checkpoint: *Retry* on the MISSION FAILED page, or **Single Player → Load Game**, which also
  lists the quick save ("Quicksave: Current") and its backup ("Quicksave: Backup").
- *Restart* (pause menu) and *Restart Chapter* start the current part from its beginning.
- Saves belong to the profile. They are kept by updates and by the uninstaller (see [Uninstall in detail](#uninstall-in-detail)).
- The checkpoint files of the Xbox build (`.sgs`) cannot be loaded.

## Multiplayer

**Multi-Player** offers **LAN** and **Internet** (the 2005 System Link and Xbox Live
pages). *Edit Game Modes* and *Split-Screen* are greyed out: neither has a page in the 2005 build.

- **LAN → Host Game**: game mode, team (team modes), character, map, bots. The game stays on your local network.
- **LAN → Join Game**: the list of games on your network (it updates itself while it is open), then team and
  character.
- **Internet**: *Create Match* hosts a game listed on OldUnreal's master servers; *Find Match* looks for games there.
  Both server lists (LAN and Internet) show each game's server name, map, game type and players.
- **Options → Edit Profile → Multiplayer**: your character, your **Name** in multiplayer games (the profile name
  unless you type another; [Ins] or pad Y opens the on-screen keyboard) and an **Outfit**: standard, desert or
  black uniform for O'Neill, Carter, Jackson, Teal'c and Graham Coulder (bots wear a random one). The same *Outfit*
  and *Name* rows are on the character page when you host or join a game; changes there are kept in the profile.
- **Pack** (same pages, under *Outfit*): the weapons you start with, besides the pistol. Its contents show at the top
  left (icons and names). Tau'ri characters (SG-1, Walter, Coulder, Tok'ra): *Assault* = P90 + frag grenades, *Close
  Quarters* = Shotgun + C4, *Marksman* = Sniper rifle + shock grenades. Goa'uld characters (Jaffa, Goa'uld;
  in team games your team decides): *Warrior* = Staff weapon + frag grenades, *Zat* = Zat gun + shock grenades,
  *Lord* = Ribbon device + frag grenades. The Stinger and the shield are only found on the maps. Bots take a random
  pack; a server can keep the 2005 start, the pistol only.

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
- Hold **Tab** (Back on the controller) to see the players and scores; F1 also shows them. To chat, open the
  console and type `say` followed by your message (`teamsay` for your team).

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

- **Update when the game starts**: the **Play Stargate SG-1 The Alliance** shortcut first asks GitHub whether a
  newer version exists (2 seconds at most; nothing about you is sent). Online games need the same version on
  both sides, so when there is one a window offers *Update*, *Later* or *Skip this version*. *Update* downloads
  it, checks its signature (a file that does not verify is deleted and nothing is installed) and opens the new
  installer, which updates the game with your options and offers *Play*. If you deleted the work folder, the
  window asks for the `.7z` again. To turn the check off, untick *Check for updates when the game starts* in the
  installer (or install with `--no-update-check`).
- **Update by hand**: download the new installer zip, extract it and run **Stargate Redial Setup.exe** again: it
  shows *Update v0.1 → v0.2*. Do not uninstall first. Your keys, settings, profiles and saves are kept, and only
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
| "close … first" | Quit the game (and anything using UT2004's files), then run the installer again. |
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
  installer again with `--reset-video` (back to the default video settings). If you switched the renderer, the
  default is Direct3D 9.
- **Window or full screen**: Video → Display. To start in a window, close the game and set
  `StartupFullscreen=False` under `[WinDrv.WindowsClient]` in `<UT2004>\SGAlliance\System\SGAlliance.ini`.
- **The movement keys are in the wrong place**: Options → Controls → Keyboard Layout, or run the installer with
  `--keyboard azerty` (or `qwerty`) and `--reset-keys`.
- **The controller does nothing**: Options → Controls → Controller On, and make sure it was connected before the
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
- **Renderer**: Direct3D 9 is the tested one and the only one that draws the bloom, the pause blur and the
  sniper scope's lens; they cost a little (about half a millisecond per frame at 1080p on a recent PC). OpenGL
  and Direct3D 11 add anti-aliasing, which costs more.
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
   - **Installation** : cochez *Mettre un raccourci sur le bureau* si vous le souhaitez, laissez cochée
     *Vérifier les mises à jour au lancement du jeu* (voir *Mise à jour et désinstallation*), puis cliquez sur
     *Installer*.
3. Patientez. La fenêtre coche chaque étape et montre l'avancement et le temps restant : environ 3 minutes sur
   un PC à 8 cœurs, 5 à 6 minutes avec 4 cœurs, plus l'extraction de l'archive. *Annuler* arrête proprement.
4. Cliquez sur **Jouer**. Plus tard, lancez **Play Stargate SG-1 The Alliance** dans `<UT2004>\SGAlliance` (ou
   le raccourci du bureau).

Le jeu est installé comme un mod d'UT2004 : votre UT2004 lui-même n'est pas modifié. La disposition de votre
clavier (QWERTY ou AZERTY) est détectée, et une manette de type Xbox branchée pendant l'installation est activée.

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
| `--desktop-shortcut` | place aussi le lanceur sur votre bureau |
| `--no-update-check` | le raccourci Jouer lance directement le jeu, sans chercher de nouvelle version |
| `--keyboard qwerty\|azerty` | disposition des touches (par défaut d'après le clavier Windows ; la page Options > Controls du jeu peut la changer ensuite) |
| `--gamepad on\|off` | une manette compatible Xbox branchée pendant l'installation est activée avec la disposition de 2005 ; ceci le force |
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
fichiers), `SGAMusic.ini`, `SGSpeechData.ini`, `SGLipSyncData.ini` et `SGMeshMaterials.ini`. Le jeu y écrit
ensuite lui-même `SGSpeech.ini` (réglages) et `SGASaves.ini`, `PlayerProfile.ini`, `Stats.ini` (sauvegardes,
profil, statistiques). Aucun fichier d'UT2004 n'est remplacé. Chaque fichier écrit par l'installeur, dans le
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
`Play Stargate SG-1 The Alliance.cmd` dans `<UT2004>\SGAlliance` ne vérifie jamais.

**À la main.** À la sortie d'une nouvelle version, téléchargez son zip, décompressez-le (dans un nouveau dossier
ou par-dessus l'ancien) et relancez **Stargate Redial Setup.exe** : la fenêtre affiche *Mettre à jour v0.1 →
v0.2* et reprend vos choix précédents (raccourci bureau, vérification des mises à jour, clavier, manette). Ne
désinstallez pas avant. Le zip et le dossier de la version précédente peuvent être supprimés.

- L'installeur lit la version installée et l'annonce (*Mettre à jour v0.1 → v0.2* ; en ligne de commande
  `updating 0.1 -> 0.2`). Installer une version plus ancienne par-dessus une plus récente demande confirmation
  (`--force` en ligne de commande).
- **Vos données ne sont jamais remplacées** : touches, réglages vidéo, audio et manette, vos autres modifications
  des fichiers de réglages du mod, profils, sauvegardes et points de contrôle, captures, journaux. Les fichiers de
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
aussi mes sauvegardes, mon profil et mes statistiques* seulement si vous le souhaitez. Depuis une invite de
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

1. Lancez **Play Stargate SG-1 The Alliance**. Le jeu s'ouvre en plein écran à la résolution du bureau, affiche
   l'écran des logos d'origine, puis le menu principal devant une scène de la Porte des étoiles. Le menu
   principal affiche « Stargate Redial V0.1 » dans son coin en bas à droite.
2. **Créez un profil.** Au premier lancement, le jeu ouvre *Create Profile* : tapez un nom au clavier (Retour
   arrière efface) ou avec les touches à l'écran, choisissez *Done* (Entrée), puis *Save* (Inser, ou un clic sur
   l'invite, ou Y à la manette). Ce profil devient le profil actif : le jeu s'en souvient au lancement suivant, et
   Continue, Single Player, Multi-Player et Options l'utilisent. Le bouton **Profile** du menu principal choisit un
   autre profil (Entrée ou un clic), en crée un (Inser) ou en supprime un (Suppr). Un profil garde sa difficulté, ses
   volumes, ses touches, ses réglages de souris, son nom et sa tenue en multijoueur, et ses sauvegardes.
3. Les menus se pilotent à la souris, au clavier (flèches, Entrée = valider, Échap ou Retour arrière = retour,
   Suppr et Inser pour les autres invites) et à la manette (croix ou stick gauche, A valider, B retour). Un seul
   élément est en surbrillance : celui sous la souris quand vous la bougez, sinon celui où les touches ou la manette
   l'ont amené ; Entrée agit sur lui. La barre d'invites en bas indique les touches du dernier périphérique utilisé.

### Les menus

#### Menu principal

- **Continue** charge le checkpoint ou la sauvegarde rapide la plus récente du dernier profil utilisé, comme le
  dit son texte d'aide de 2005. Il reste grisé tant que le profil n'a pas de sauvegarde. (Dans la version de 2005,
  il ouvrait une liste provisoire de toutes les cartes.) Pour lancer n'importe quelle partie de mission, passez par
  Single Player → Chapter Selection. La version n'a pas les missions 1, 3, 5, 6, 8, 9 et 11.
- **Exit Game** quitte le jeu après confirmation, comme Échap.
- **Single Player** :
  - **New Game** demande si vous voulez jouer le didacticiel : *Yes* lance le didacticiel (M00), *No* lance la
    mission 2.
  - **Chapter Selection** liste les 61 parties de l'histoire, sans image de chapitre (les données de 2005 n'en
    ont pas).
  - **Load Game** liste les points de contrôle et la sauvegarde rapide du profil ([Sauvegardes](#sauvegardes)) :
    chargez-les ou supprimez-les.
  - **Tutorial** lance M00.
- **Multi-Player** : voir [Multijoueur](#multijoueur).
- **Options** → **Edit Profile** du profil actif : Controls, Multiplayer (votre personnage en multijoueur), Video,
  Audio, Name, Difficulty. Voir [Les options](#les-options).
- **Profile** : choisir le profil actif, en créer un ou en supprimer un (voir [Premier lancement](#premier-lancement)).
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

Les touches se changent dans **Options → Edit Profile → Controls**. La colonne manette est la disposition Xbox
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
| Informations de mission | Tab | Tab | Back |
| Scores (multijoueur) | F1 | F1 | — |
| Sauvegarde rapide / chargement rapide | F5 / F9 | F5 / F9 | — |
| Menu pause | Échap | Échap | Start |
| Console | `²` ou `ù` | `` ` `` (à gauche de 1) | — |
| Capture d'écran | F12 | F12 | — |

Bon à savoir :

- Objets, armes et munitions se ramassent avec **Utiliser**, pas en passant dessus. Utiliser ouvre aussi les
  portes, actionne les consoles et ranime un équipier à terre (« administer first aid »).
- **Sprinter** vide la barre d'endurance, qui se recharge à l'arrêt. Le double appui sur avancer, la méthode de
  2005, fonctionne toujours.
- **Tir concentré** : un appui fait tirer l'équipe sur ce que vous visez ; maintenu, il permet de choisir un
  équipier à commander. **Se mettre à couvert** envoie l'équipe à couvert.
- Le **camouflage** demande une ceinture de bouclier ; il ne marche pas en sprintant, et l'équipe se camoufle
  avec vous.
- Les **grenades** n'ont pas de touche à elles (comme en 2005) : choisissez-les avec 4 (ou la molette), puis tirez
  pour lancer.
- Le **zat** et le **ribbon device** tirent environ deux coups avec une charge pleine, puis se rechargent (pleine en
  6 secondes) ; la charge s'affiche en haut à droite, en barre et en pourcentage. La **lance Goa'uld** se charge tant
  que vous maintenez le tir.

#### Changer les touches

Sur la page Controls, *Keyboard Layout* passe d'un préréglage à l'autre : QWERTY (WASD) ou AZERTY (ZQSD). Dans
la liste des actions : Entrée ou un double-clic, puis appuyez sur la nouvelle touche ou le bouton de souris
(Échap annule) ; Suppr retire les touches d'une action ; Inser rétablit les touches par défaut de la disposition.
Une touche prise à une autre action lui est retirée, et la page le signale. Échap ouvre toujours le menu pause,
on ne peut donc pas le perdre. Les changements s'appliquent aussitôt.

#### Manette

Une manette de type Xbox (Xbox 360, One ou Series) utilise la disposition de 2005 ci-dessus.

- **Branchez-la avant de lancer le jeu** : le jeu lit la manette trouvée au démarrage. Branchée plus tard, il
  faut relancer le jeu.
- Options → Controls, colonne de droite : **Controller** On/Off, **Pad Look Speed** (1.0 = le jeu d'origine) et
  **Invert Pad Look**.
- Tous les menus marchent à la manette, et les invites et conseils nomment les boutons de la manette pendant que
  vous l'utilisez.
- Limites (le jeu lit les manettes par DirectInput) : **LT et RT pressées ensemble s'annulent**, il n'y a **pas
  de vibrations**, et seule la première manette listée par Windows est lue.
- Si les gâchettes sont inversées, ajoutez `bSwapTriggers=True` sous `[SGShim.SGPadInfo]` dans
  `<UT2004>\SGAlliance\System\SGAllianceUser.ini` (jeu fermé).

### Les options

**Options → (profil) → Edit Profile**, aussi accessible depuis le menu pause. Les changements Video et Audio
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
| Brightness | 10 à 100 | avec Direct3D 9, seulement en plein écran |
| Renderer | Direct3D 9, OpenGL, Direct3D 11 | Direct3D 9 donne l'aspect d'origine ; au prochain démarrage |
| Anti-Aliasing | Off, 2x, 4x, 8x | OpenGL ou Direct3D 11 seulement ; au prochain démarrage |
| Texture Filtering | Bilinear, Trilinear, Anisotropic 2x à 16x | |
| Shadows | On, Off | ombres des personnages uniquement (impacts, traces de brûlure et lampe torche restent) ; s'applique tout de suite, ou au prochain chargement de niveau si le niveau a démarré avec Off |
| World Detail | High, Low | lumières dynamiques, halos, impacts, végétation, textures de détail ; au prochain chargement de niveau |
| Bloom | On, Off | le halo lumineux de la version de 2005 et le flou derrière le menu pause ; immédiat. Direct3D 9 seulement : avec OpenGL ou Direct3D 11, la ligne affiche Off |

#### Audio

| Ligne | Valeurs | Remarques |
|---|---|---|
| Music Volume, Voice Volume, FX Volume | 0 à 1 | enregistrés dans le profil |
| 3D Audio (HRTF) | Auto, Off, On | son 3D au casque ; au prochain démarrage |
| Sound Channels | 32, 64, 128 | au prochain démarrage |

#### Contrôles

Keyboard Layout, la liste des actions ([Changer les touches](#changer-les-touches)), Mouse Sensitivity, Invert
Mouse, Mouse Smoothing (Off = mouvement brut de la souris), et les lignes de la manette ([Manette](#manette)).

### Difficulté

**Options → Edit Profile → Difficulty** : Easy, Medium, Hard ou Insane. Par défaut **Hard**, la valeur par défaut
de 2005. Les menus de 2005 ne permettaient pas de la changer ; les quatre niveaux sont complets dans les données
du jeu. Le choix est enregistré dans le profil et s'applique au prochain début de niveau, redémarrage ou
chargement. Comme dans le jeu d'origine, il change aussi la résistance de vos alliés.

### Sauvegardes

Comme en 2005, le jeu sauvegarde **aux points de contrôle**. Sur PC, vous pouvez aussi faire une **sauvegarde
rapide** à tout moment (il n'y a toujours pas de menu de sauvegarde).

- « Checkpoint reached » s'affiche quand le jeu sauvegarde. Une sauvegarde est aussi faite au début de chaque
  partie.
- **Sauvegarde rapide : F5**, **chargement rapide : F9** (Options → Edit Profile → Controls pour changer les
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
- Les sauvegardes appartiennent au profil. Les mises à jour et la désinstallation les conservent (voir
  [Désinstallation en détail](#désinstallation-en-détail)).
- Les fichiers de points de contrôle de la version Xbox (`.sgs`) ne peuvent pas être chargés.

### Multijoueur

**Multi-Player** propose **LAN** et **Internet** (les pages System Link et Xbox Live
de 2005). *Edit Game Modes* et *Split-Screen* sont grisés : aucun des deux n'a de page dans la version de 2005.

- **LAN → Host Game** : mode de jeu, équipe (modes en équipe), personnage, carte, bots. La partie reste sur votre
  réseau local.
- **LAN → Join Game** : la liste des parties de votre réseau (elle se met à jour toute seule tant qu'elle est
  ouverte), puis équipe et personnage.
- **Internet** : *Create Match* héberge une partie listée sur les serveurs maîtres d'OldUnreal ; *Find Match* y
  cherche des parties. Les deux listes de serveurs (LAN et Internet) affichent pour chaque partie le nom du serveur,
  la carte, le mode de jeu et les joueurs.
- **Options → Edit Profile → Multiplayer** : votre personnage, votre nom en multijoueur (**Name** : le nom du
  profil sauf si vous en tapez un autre ; [Ins] ou Y à la manette ouvre le clavier à l'écran) et une tenue
  (**Outfit**) : uniforme standard, désert ou noir pour O'Neill, Carter, Jackson, Teal'c et Graham Coulder (les
  bots en portent une au hasard). Les mêmes lignes *Outfit* et *Name* figurent sur la page du personnage quand vous
  créez ou rejoignez une partie ; ce que vous y changez est gardé dans le profil.
- **Pack** (mêmes pages, sous *Outfit*) : les armes avec lesquelles vous commencez, en plus du pistolet. Son contenu
  s'affiche en haut à gauche (icônes et noms). Personnages Tau'ri (SG-1, Walter, Coulder, Tok'ra) : *Assault* = P90 + grenades
  à fragmentation, *Close Quarters* = fusil à pompe + C4, *Marksman* = fusil de précision + grenades paralysantes.
  Personnages Goa'uld (Jaffa, Goa'uld ; en équipe, c'est votre équipe qui décide) : *Warrior* = lance Goa'uld +
  grenades à fragmentation, *Zat* = zat + grenades paralysantes, *Lord* = ribbon device + grenades à fragmentation. Le
  Stinger et le bouclier ne se trouvent que sur les cartes. Les bots prennent un pack au hasard ; un serveur peut
  garder le départ de 2005, le pistolet seul.

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
- Maintenez **Tab** (Back à la manette) pour voir les joueurs et les scores ; F1 les affiche aussi. Pour
  discuter, ouvrez la console et tapez `say` suivi du message (`teamsay` pour votre équipe).

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

- **Mise à jour au lancement du jeu** : le raccourci **Play Stargate SG-1 The Alliance** demande d'abord à
  GitHub s'il existe une version plus récente (2 secondes au plus ; rien sur vous n'est envoyé). Pour jouer en
  ligne, il faut la même version des deux côtés : s'il y en a une, une fenêtre propose *Mettre à jour*, *Plus
  tard* ou *Ignorer cette version*. *Mettre à jour* la télécharge, vérifie sa signature (un fichier qui ne la
  vérifie pas est supprimé et rien n'est installé) et ouvre le nouvel installeur, qui met le jeu à jour avec vos
  options et propose *Jouer*. Si vous avez supprimé le dossier de travail, la fenêtre redemande le `.7z`. Pour
  couper la vérification, décochez *Vérifier les mises à jour au lancement du jeu* dans l'installeur (ou
  installez avec `--no-update-check`).
- **Mise à jour à la main** : téléchargez le nouveau zip de l'installeur, décompressez-le et relancez
  **Stargate Redial Setup.exe** : il affiche *Mettre à jour v0.1 → v0.2*. Ne désinstallez pas avant. Vos
  touches, réglages, profils et sauvegardes sont conservés, et seul ce qui a changé est reconstruit. Détails :
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
| « close … first » | Quittez le jeu (et tout ce qui utilise les fichiers d'UT2004), puis relancez l'installeur. |
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
  avec `--reset-video` (réglages vidéo par défaut). Si vous avez changé de moteur de rendu, le défaut est
  Direct3D 9.
- **Fenêtre ou plein écran** : Video → Display. Pour démarrer en fenêtre, fermez le jeu et mettez
  `StartupFullscreen=False` sous `[WinDrv.WindowsClient]` dans `<UT2004>\SGAlliance\System\SGAlliance.ini`.
- **Les touches de déplacement ne sont pas au bon endroit** : Options → Controls → Keyboard Layout, ou relancez
  l'installeur avec `--keyboard azerty` (ou `qwerty`) et `--reset-keys`.
- **La manette ne fait rien** : Options → Controls → Controller On, et vérifiez qu'elle était branchée avant le
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
- **Renderer** : Direct3D 9 est le moteur testé et le seul qui dessine le bloom, le flou du menu pause et la
  lentille de la lunette du fusil de précision ; ils coûtent un peu (environ une demi-milliseconde par image en
  1080p sur un PC récent). OpenGL et Direct3D 11 ajoutent l'anticrénelage, qui coûte davantage.
- Sur un PC lent : *World Detail* Low, *Shadows* Off, une résolution ou un *Texture Detail* plus bas.
- Sur un portable, vérifiez que Windows lance UT2004 sur la carte graphique dédiée.

#### Signaler un problème

Ouvrez une issue sur le [dépôt GitHub](https://github.com/Stargate-Redial/alliance-redial/issues) avec la version
(V0.1), ce que vous avez fait, ce que vous avez vu, et `<UT2004>\System\UT2004.log` (plus les journaux de
l'installeur pour un problème d'installation). Consultez d'abord [KNOWN_ISSUES.md](KNOWN_ISSUES.md#français).
