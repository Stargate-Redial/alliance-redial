# Changelog — differences from the December 2005 Xbox build

This port aims to reproduce the 2005 prototype exactly. Everything below is a deliberate, documented difference.
Each entry says why it exists. No game data is in this repository; all fixes are applied locally by the installer.

## Fixes to bugs present in the 2005 build (approved by the project lead)

- **Scripted dialogue no longer hangs a scene.** In the original code, a line that could not start (another line was
  still playing, or its sound file was missing) left the scene's script waiting forever, unless a timer happened to be
  running, in which case the line was skipped. A speaker removed mid-line also kept the dialogue channel busy for the
  rest of the level, so every later line failed the same way (seen in M07E, M10D, M18D, M19B). Such a line is now
  always skipped, and the channel is freed when the removed speaker's line ends. Nothing changes when dialogue plays
  normally.
- **M18D blast-door prompt** reads "Press [E] to use blastdoors" instead of the doubled "Press [E] Press [Fire] to use
  blastdoors".
- **A scripted teleport whose destination does not exist** (M12C after the hacking cinematic, M17D) no longer sends the
  character to the world origin; the character stays put and the script stops, as it did in 2005.
- **Scripts that wait in a loop without pausing** (M14A) no longer freeze the game: such a loop now checks its
  condition once per frame.
- **DM-KelownanTrain** no longer shows a debug "got it..." message to every player during the plane crash.
- **M19D**: the first Jaffa wave after the second wall now attacks (its two spawners carried a misspelled name the
  level's enemy script never called).
- **M07D**: the third Jaffa wave of the priests' puzzle comes when the team returns to the alcove after deciphering (its
  trigger was never switched on; it now arms together with the alcove trigger next to it).
- **M02A**: after the intro, Major Gray finishes his animation and walks off instead of standing frozen (he waited for
  a dialogue line that was cut from the game; he now waits for the line before it).
- **M17B**: the Jaffa squad north of the workshop advances once SG-1 has picked up the Kull disruptors (it waited for
  an event nothing fires; it now uses the workshop scene's go event).
- **Multiplayer Join with no server selected** no longer reloads the main menu.
- **HUD prompts**: the placeholder text "default" no longer shows under the crosshair after the M02A intro; a prompt
  hidden by a cinematic no longer comes back afterwards; prompts such as "Press [E] to start driving" are no longer
  drawn over the death camera and the MISSION FAILED page.
- **Menus that pointed to nothing**: Single Player → Load Game opens the saved-games page (2005 opened the chapter
  list); New Game → "Yes" and the Tutorial button start the tutorial (M00), "No" starts Mission 2 (both targets were
  missing from the build); Chapter Selection lists the 61 story maps of the build (its 2005 list named working copies
  and missing maps); Return to Main Menu returns to the menu (2005 quit the game); the Audio options page opens (a
  2005 typo) and its volumes are applied (a 2005 TODO).
- **MISSION FAILED**: Retry and Load Game are enabled when something can be loaded (2005 always disabled them).
- **Multiplayer "Instant Match" hint** no longer starts with a stray invisible character.
- **System Lord** is no longer listed among the multiplayer modes: its game code is not in the build, and choosing
  it loaded the map with the single-player rules.
- **Eight materials missing from the 2005 data** use the texture of the same name in the same package (Perception's
  `_S` / `_02` / `_PS2` variants): the Hummvee's camouflage net, the M60 tripod, the M13B ring platform and CTF
  bases, gun reflections and the M12 alarm panel (2005 drew the engine's default texture there).
- **Developer speed and teleport commands** (SetServerSloMo, AdjustSpeed, EditSpeed, SetWalkingPerc, UnStick) work only
  in single player; online, any client could have used them on a server (the Xbox had no console to type them).
- **Retrying from a checkpoint no longer replays the ambush or event laid over it.** Seven checkpoints sit inside a
  one-time trigger zone (M02B, M02C, M07D, M12C, M12F, M13D, M14B); in 2005 a Retry put the player back in the zone,
  which fired again: enemy waves were re-armed and M12C's command-centre doors closed again. A zone already used
  before the checkpoint now stays used; one whose sequence was still under way plays out as before.
- **The `ShadowLights` console command** no longer makes character shadows follow nearby lights, muzzle flashes or
  fill lights; as in 2005, character shadows always keep their fixed direction.
- **Menu lists** draw their text at the 2005 size (the list style's 85 % scale): long chapter names no longer run
  into the scroll bar.
- **On-screen keyboard** (profile name): the Space key types a space and no longer presses the selected on-screen
  key (with *Done* selected it closed the keyboard).
- **`togglehud`** (console) also hides the shield, stamina and ammunition bars; in 2005 they stayed on screen.
- **Multiplayer Internet list**: servers returned by the master servers now appear in the list. In 2005 each new
  game-type query cancelled the previous server-detail requests, so late replies were dropped and the page showed
  "No matching games were found".
- **Multiplayer: the Mission Information page can always be closed.** In 2005, dying with it open brought up the
  scoreboard over it and left the menus without input, so the page stayed on screen for the rest of the game. The
  scoreboard now waits until the page is closed.
- **Key rebinding** (Options → Controls) no longer binds the Enter that starts the change, and the new key replaces
  the chosen key instead of being added to it. Each action has two keys (Key 1 / Key 2, as the 2005 PC profile stored
  them), picked with Left/Right or a click; Delete clears the chosen key.
- **Create New Profile** opens on its first option, so Enter works there, and the prompt that creates the profile
  reads "[Ins] Save" (2005's own text for it) instead of "Create New".
- **No stray "DefaultProfile"**: creating a profile no longer also stores an empty profile named DefaultProfile (the
  2005 profile code saved the blank profile it replaced), and leaving Create Profile with Back no longer leaves a
  temporary profile in use.
- **Chapter Selection**: every chapter name fits its row (the list draws them a little smaller), so the chapters of
  one mission can be told apart.
- **Squad members no longer get stuck next to a parked Hummvee.** A team-mate left touching the Hummvee was nudged by
  the idling car without pause, hung in mid-step beside it, never got in and kept calling out friendly fire. A car
  moving too slowly to hurt anyone no longer pushes people; a real hit by a moving car works as before. A team-mate
  who was still crouching when you got in (for example after stepping out of your line of fire) could also stay wedged
  against the car body, unable to stand up; he or she now steps away from the car first.
- **Passengers of the Hummvee's back seats get out beside the car instead of inside it.** Their exit points were inside
  the car body, so they were left inside or under the car, sometimes falling through the ground. Those exit points are
  still tried first; when none is free, they use the car's side doors, like the driver (also the Semektet in M02D).
- **Team DeathMatch spawns**: on the six DeathMatch maps where one team has no start points of its own, that team now
  spawns at every start point, as in DeathMatch, instead of always at the same first one.
- **Multi-Player → Edit Game Modes** is greyed out like Split-Screen (it led nowhere).
- **Games hosted on the LAN are named after the host's profile** (2005 named them all "Unnamed"; the Internet path
  already used the profile).
- **M15E no longer blocks when Coulder arrives early**: if he reached O'Neill before Carter finished her line, the
  level waited forever (no talk with Coulder, no ring transport). His arrival is now remembered by that wait, with the
  designers' own flag already used on 207 other waits of the 2005 maps.
- **A new character starts the next mission with his or her own weapons.** Two level changes that switch the
  player's character kept the previous character's inventory, so the newcomer arrived with someone else's weapons:
  M07E → M10A (Teal'c arrived with Jackson's weapons and without his staff weapon) and M16G's second Hummvee exit
  → M17A (Carter with Jackson's). As at every other change of mission, the new character now arrives with that
  mission's own loadout.
- **Bodies no longer fall through floors made of static meshes** (the first mission's jungle ground pieces, stairs,
  stone blocks): the 2005 meshes have no simple physics shapes, so ragdolls sank through them standing upright.
  Static meshes that the maps leave blocking now use their triangles for physics; as a side effect, physics vehicles
  also collide with them.
- **Headshot deaths**: a character killed by a headshot whose model has no headshot animation (SG-1, Goa'uld, NPCs,
  soldiers; only the Jaffa have one) stayed standing, frozen, forever. It now falls like any other death.
- **Stargate iris with an open wormhole** (main menu background, end of M17D): the scripts close the iris and then shut
  the wormhole down, but the 2005 gate ignored that second order. The event horizon stayed on in front of most of
  the closed iris, and the menu's gate never dialled again. A gate whose iris is closed now shuts down when its
  script asks; gates without an iris behave as in 2005.
- **Long "New Objective" notifications** shrink to fit their one-line frame (down to half size) instead of wrapping
  below it: 47 of the 228 objective names were too wide for the 2005 frame.
- **Select Team** shows which team is selected (2005 left the selection box to a list drawing UT2004 does not have).
- **Weapon effects in network games** (client of a server): the staff weapon's blasts are visible (2005 built their
  glow, impact and sound only where the shot was spawned, the server); bullet tracers show (online they start in the
  shooter's eye and destroyed themselves on the shooter at once; your own now leave your gun's muzzle as in single
  player); the other players see a human player's muzzle flash (2005 only counted the bots' shots); your own muzzle
  flash shows at the gun (it was spawned at the map's origin).
- **Charge of the Zat gun, ribbon device and staff weapon in network games**: the HUD showed 0 and an empty bar on a
  client; it shows the charge. The 2005 charge itself is kept: about two Zat or ribbon shots on a full charge, full
  again in 6 seconds.
- **Sniper rifle and binoculars in network games**: after leaving the scope the weapon stayed raised to the eye until
  the next shot, and the scope toggle right after a shot was ignored. With the mouse scope, a right button still held
  when the scope animation ends no longer strikes with the weapon (single player too).
- **Weapon menu in network games**: each weapon you selected was greyed out a moment later (UT2004 reported it out of
  ammunition), until the mouse wheel and the number keys only opened the menu without switching.

## Additions for PC playability and modern standards

- **Real cinematic skip.** "Press [E] to Skip" ends the scene at once, using Perception's own hard-skip code, which no
  button reached in 2005 (only the cinematic's own scripts are fast-forwarded; the level ends up as after a full
  viewing). The original soft skip stays available: `[SGBase.SGSceneManagerBase] bHardSkip=False`.
- **Difficulty selector** on Options → Edit Profile (Easy / Medium / Hard / Insane; default Hard, the 2005 default).
  The four levels are complete in the data, but no 2005 menu set them. As in the original code, the level also scales
  allied soldiers.
- **PC key names in prompts and hints** ("Press [E]" instead of Xbox buttons), following the player's bindings.
- **Keyboard and mouse controls**: rebindable actions, QWERTY/AZERTY presets chosen from the Windows keyboard layout,
  a Sprint key (Shift) in addition to the original double-tap.
- **Options from the pause menu** (Perception's commented-out button restored).
- **Any resolution and aspect ratio** (16:9, 21:9, 4K): the menus keep the 2005 4:3 layout, scaled, not stretched,
  centred over the full-width scene (no black bars on wide screens); Hor+ field of view; frame-rate cap up to 240 or unlimited; VSync; FOV setting.
- **Online play through OldUnreal's master server and LAN** in place of Xbox Live / System Link: games hosted from the
  System Link pages stay on the local network; games hosted from the Xbox Live pages, and dedicated servers, are listed
  on OldUnreal's master servers. The installer's `--server` option sets up dedicated servers for Windows and Linux
  ([docs/SERVER.md](docs/SERVER.md)).
- **Discord activity feed for dedicated servers** (optional, off by default; not in the 2005 build): with
  `Discord=True`, a server-side package (never downloaded by players) sends the server's events to a small relay that
  posts players joining and leaving, kills, match results and map changes in a Discord channel, with the server
  owner's own bot ([docs/SERVER.md](docs/SERVER.md)).
- **Graphics, audio and mouse options** on the game's own Options pages: renderer (Direct3D 9 / OpenGL / Direct3D 11),
  anti-aliasing 2x–8x (OpenGL / Direct3D 11), texture filtering (bilinear to 16x anisotropic), character shadows, world detail,
  bloom on/off (Direct3D 9), 3D audio (HRTF), sound channels, mouse smoothing. A new install starts with every graphics
  setting at its highest (UltraHigh textures, 16x anisotropic filtering, shadows, world detail, bloom), with only the 2005
  build's effects; an update keeps your own settings.
- **Game controller** (Xbox 360/One/Series, XInput) with the original 2005 Xbox layout: A jump, B cloak, X use / skip /
  reload, Y last weapon, RB concentrate fire, LB take cover, RT fire, LT secondary fire, d-pad weapon selection /
  binoculars, Start pause, Back mission information, stick clicks crouch / zoom; the 2005 stick response is reproduced.
  Options → Controls: Controller On/Off (turned on at install if one is connected), Pad Look Speed, Invert Pad Look.
  All menus work with the pad; prompts and hints name pad buttons while the pad is in use.
- **Multiplayer pages use PC terms**: "System Link" is now "LAN" and "Xbox Live" is now "Internet" in titles, buttons,
  hints and status lines.
- **Multiplayer bots** (DeathMatch, Last Man Standing, Team DeathMatch and Capture the Flag; not in the 2005 build):
  the host's map page has *Bots* (none to 15) and *Bot Skill* (0 Very Easy to 7 Elite, default 6 Expert) rows,
  remembered for the next game; a game with bots starts at once, without waiting for a second player. In Team
  DeathMatch and Capture the Flag the teams are SG-1 (O'Neill, Carter, Jackson, Teal'c) against the Jaffa. In Capture
  the Flag (CTF-Abydos, CTF-LostCity, SGCTF-AbydosVsSGC) bots attack the enemy flag, defend their base, bring their
  dropped flag back, escort their flag carrier and hunt the enemy's.
  Bots playing O'Neill, Carter, Jackson or Teal'c sometimes say one of their character's own game lines (a taunt or
  an "enemy down" line) after a frag, at most once every 25 seconds; the Jaffa and the other characters stay silent.
  Bots play with UT2004's bot AI on a navigation network the
  game builds when the map loads (the 2005 multiplayer maps have none), and they use the Stargates, rings and
  ladders. Servers: `?MinPlayers=N` / `?BotSkill=0-7`, and the console commands AddBots, KillBots and SetBotSkill.
  Players joining need nothing.
- **Project label on the main menu**: "Stargate Redial V0.1" and `github.com/Stargate-Redial` in the bottom-right corner
  of the screen (outside the original 4:3 art on wide screens). Not in the 2005 build.

- **Installer**: every tool it runs is the project's own code (no third-party decompilation tools are downloaded),
  and the game files are checked against the project's own hash list.
- **Quick save and quick load** (F5 / F9; rows Quick Save and Quick Load on Options → Controls): Perception's own
  QuickSave/QuickLoad commands, which no key or menu reached in 2005, on the port's save system. A quick load puts you
  back where you saved, and the level's scripted events carry on from there. F9 also works on the pause menu and on
  the MISSION FAILED page, and Load Game lists the quick save and its backup. Refused during cutscenes and in
  multiplayer. Retry and checkpoint loads still restart the level's scripts, as in 2005. The screenshot key moves
  from F9 to F12.
- **Multiplayer scoreboard on Tab** (pad Back): hold it to show the game's own scoreboard page (players, ping, kills,
  deaths) instead of the empty Mission Information page, as in UT2004. In 2005 it appeared only after a death, at the
  end of a match, or on F1. Single player is unchanged.
- **The LAN server list updates itself** while it is open (in 2005 it asked the network once, when the page opened).
- **Server names in the server lists**: the LAN and Internet lists show each server's name in a first column, as
  UT2004's browser does (a long name ends with "..."); the column titles read Server, Map, Game Type, Players.
- **Version check in the server lists**: each server announces its Stargate Redial release; the LAN and Internet lists
  dim a server of another release and mark it "v0.1.1 required" (or "Other version"), and joining one anyway says
  "This server runs Stargate Redial v... You have v..." instead of UT2004's "Server refused to send" message.
- **Faster typed text**: tutorial hints and mission briefings type three times faster than in 2005
  (`[SGGUI.SGScrollText] TypeSpeed=1` restores the 2005 speed). As in 2005, Enter, pad A or a click shows the whole
  text at once, and a second press continues.
- **Sniper rifle and binoculars**: the right mouse button raises and lowers the scope (2005: the zoom key / middle
  button only); with the sniper scope up, the middle button steadies the aim (2005: the secondary fire). The pad keeps
  the 2005 buttons.
- **Shorter Internet menus**: Multi-Player → Internet opens the match menu at once (the Xbox Live sign-in page is
  skipped); it shows Create Match and Find Match, which opens the server list at once (Instant Match, which did the
  same, is hidden; the empty Match Filters page is skipped).
- **Window title**: the game window is titled "Stargate SG-1 The Alliance: Redial" instead of "Unreal Tournament 2004".
- **Sharper HUD text at high resolutions**: subtitles and HUD labels use a larger size of the same 2005 font (the game
  font up to its Huge size, Tahoma up to 36 px) instead of magnifying the small one; same size and layout.
  `[SGBase.SGHudScale] bSharpFonts=False` restores plain magnification.
- **Menus work with the mouse**: one click chooses a map, chapter, character, team, game mode or server (as Enter);
  in the profile, saved game and Controls lists a click selects the row and a second click or a double-click
  chooses it. One item is highlighted at a time, as usual on PC: the button, option or list row under the mouse
  takes the highlight (and the focus Enter acts on), and the arrow keys, Tab and the pad still move it; a list's
  selected row stays framed, dimmed, while another control has the focus. Up/Down also move between buttons, like
  the pad's d-pad.
- **Exit Game button** on the main menu, from Perception's earlier main menu in the 2005 data; it asks for
  confirmation, like Escape.
- **Console**: the key that opens it (² on AZERTY keyboards) closes it again, and one Escape closes it. Tab also
  closes the Mission Information page (Escape only before).
- **Multiplayer outfits**: Options → Edit Profile → Multiplayer has an *Outfit* row (Standard / Desert / Black)
  that dresses O'Neill, Carter, Jackson, Teal'c and Graham Coulder in the 2005 build's unused desert and black
  SG-1 uniform textures; every player sees it, bots pick one at random. Team games stay readable (SG-1 against
  Jaffa).
- **Multiplayer player name**: the same page has a *Name* box (on-screen keyboard with [Ins] or pad Y) for the
  name other players and the game list see; empty, it is the profile name as before.
- **Outfit and Name when hosting or joining**: the character page of the host and join flows has the same *Outfit*
  and *Name* rows as Options → Multiplayer (and its [Ins] Player Name prompt); what is set there is kept in the profile.
- **Multiplayer weapon packs** (project lead's decision, a deliberate change of the 2005 balance): every player still
  starts with the 2005 pistol and also gets the pack chosen under *Outfit* on the character pages and Options →
  Multiplayer (its weapons shown with their icons). Tau'ri: Assault = P90 + frag grenades, Close Quarters = Shotgun +
  C4, Marksman = Sniper rifle + shock grenades; Goa'uld: Warrior = Staff weapon + frag grenades, Zat = Zat gun + shock
  grenades, Lord = Ribbon device + frag grenades (grenades and C4 in the amount of their 2005 map pickups). The side
  is the team in team games, else the character (Jaffa and Goa'uld are Goa'uld; the Tok'ra, allies of Earth, are Tau'ri). Bots take a random pack of
  their side. The Stinger and the shield stay map pickups. A server keeps the 2005 pistol-only start with
  `?SGPacks=0` or `[SGBase.SGPacks] bPacks=False` (see SERVER.md).
- **One profile for the session** (project lead's decision): the main menu has a *Profile* button, two steps under
  Exit Game, to select, create or delete profiles. The chosen profile is the active one, remembered across launches,
  and Continue, Single Player, Multi-Player and Options use it (2005 asked for a profile on each of these paths). At
  the first launch, with no profile yet, the game opens Create Profile; a path that needs a profile when none is
  active opens the Profile page first.
- **Extras hidden**: the main menu's *Extras* opened an empty 2005 placeholder page ("Extras should go here"); the
  button is hidden and Exit Game takes its step.
- **Internet page Back prompt**: the Internet page (Create Match / Find Match) shows [Esc] Back like the LAN page (on
  PC it opens straight from Multi-Player; 2005 came back to it from a sign-in page with its own Back).
- **Kill messages name the weapon** (project lead's decision): "X was killed by Y (Ribbon Device)." and "You were
  killed by Y (Shotgun)!", from the weapon in the killer's hands. Kills that have their own 2005 wording (Zat, melee,
  explosions) are unchanged.
- **Multiplayer HUD portraits** (project lead's decision): the Jaffa, the Goa'uld, the Tok'ra and Walter, who have no
  HUD portrait in the 2005 data, and Graham Coulder, who showed O'Neill's, use their 2005 picture from the character
  selection menu.
- **Jaffa holding the pistol** (project lead's decision): the Jaffa animations have no pistol set, so 2005 showed them
  holding it in the staff pose; they now hold it with their Zat animations.
- **Charge percentage**: the HUD's charge number of the Zat gun, ribbon device and staff weapon reads as a
  percentage (70%).

## Perception's own PC code used instead of the Xbox variant

The game's scripts contain both Xbox and PC variants of some passages; the port uses Perception's PC variants (project
decision), except where a PC line is broken. Visible differences from the 2005 Xbox build:

- The notification box (checkpoints, objectives) uses the PC version's default HUD font; the Xbox build used SmallFont.
- The binocular zoom shows the PC version's static fuzz, growing with the zoom step; the Xbox build had none.
- Debug messages the 2005 build showed on screen are not shown: a red chat line when a scripted sequence broke, and a
  placeholder text for an empty notification.

## Restored (present in the 2005 build but never wired)

- **Last Man Standing** (multiplayer): Perception's complete mode (five lives; the last player with lives left wins) was
  switched off in the 2005 game-mode list; it is listed again under Multiplayer → Host, plays on the seven deathmatch
  maps and appears in the Internet server list.
- **Create Profile**: the 2005 page never showed its "Create New" button, so no profile could be created. The button is
  back (Ins or click), and on PC the name can also be typed on the keyboard (Backspace deletes).
- **Build stamp**: the 2005 build date is no longer shown on the main menu; only the Stargate Redial label is (bottom right).
- **Original Xbox button icons in the menu prompt bar**, shown while the controller is in use.
- **Squad members crouch out of your line of fire** when you shoot past them (switched off for the May 2005 E3 demo).
- **P90 with torch**: Carter's and Daniel's P90 in M20C and the six SGCTF-AbydosVsSGC pickups shine their flashlight
  while raised (in 2005 they were a plain P90).
- **Bullet and grenade effects per material**: glass, metal, metal grates, sand, snow, carpet, ice, dirt and grass get
  their own marks, wood its wood chips, water its own splash.
- **Hummvee door and ignition sounds** when you get in (the engine starts after it) and the door sound when you get out.
- **SGC card readers** buzz "access denied" with "This door has already been secured!".
- **M19 and M20 play their own music** (in 2005 they played M07B's and M01's).
- **Stinger launcher** can be raised, fired and switched away from: its own first-person animation set is linked when
  the mesh has none (in 2005 it was stuck and blocked weapon switching).
- **Team Deathmatch ends at its frag limit**: team kills count for the team, as in the UT2003/UT2004 TeamGame the mode
  was copied from (in 2005 it never ended). Capture the Flag is unchanged.
- **M02C**: the third positioning device plays its start sound and hum when Daniel activates it, like the first two
  (its sound script waited for an event nothing fires).
- **M07B**: after the palace talk, Carter walks to the last symbol and calls "Daniel, over here!" (her script waited
  for an end-of-talk event nothing fired).
- **M21D**: a picture-in-picture view shows the pod-room doors opening after the third crystal (the inset camera was
  placed, but no event matched its name).
- **M20A**: the air-filter door consoles beep when the doors are activated (their sound scripts waited for the wrong
  event names).
- **M16A**: SGC soldiers carry their P90 (six squad rosters misspelled the weapon class; in 2005 they were unarmed).
- **Map list filter**: the *Filter* box of the multiplayer host's map page is on screen, in the menus' own style, and
  keeps the maps whose name starts with what you type (2005: wired to nothing and placed below the screen).
- **Continue** (main menu) loads the profile's most recent checkpoint or quick save, as its 2005 hint says ("Load the
  most recent saved game or checkpoint"); it is greyed when the profile has no save. In 2005 it opened a temporary
  list of every map file, multiplayer maps included.
- **Multiplayer Options** shows the selected character's picture: the 2005 page had it but never updated it.
- **Binocular target read-out**: looking at a character through the binoculars shows its range, its health and the
  order prompt again (2005 had commented out the HUD reference the read-out needs).
- **"No matching games were found"**: when an Internet search finds no game, the 2005 message box appears again
  (2005's Instant Match opened it); OK goes back to the previous page.
- **Lip sync in every mission**: the SG-1 crew's lip-sync tracks now play wherever their line is spoken. The 2005
  build loaded them only in M00, M07, M10, M13, parts of M15, M20 and M21, so 283 dialogue lines in 34 other maps
  (the first mission M02A–D, M04, M12, M14, M15A/E, M16, M17, M18 and M19) played with a still face. Characters with
  no lip-sync data (the doctor, Jonas, other NPCs, Jaffa) still don't move their lips, as in 2005.
  `bAllTracks=False` under `[StargateGame.SGLipSync]` in SGSpeech.ini brings back the 2005 behaviour.
- **About 150 recorded voice lines no voice set used** (the 2005 voice sets kept only some takes of each line):
  more variety in the Jaffa's attack shouts, pain and death cries, the Jaffa captain's own attack shouts, more takes of
  the crew's orders and replies ("Wait for my order" when you hold a concentrate fire, which was silent; "Target the
  Jaffa vehicle"; "Move in formation"...), and three moments that were silent: a Jaffa knocked out by a shock grenade
  screams (squad mates hit by one complain again, as the 2005 code intended), a fleeing Jaffa shouts, and a Jaffa
  running to sound the alarm calls out. The other unused lines belong to orders and situations the game does not
  have (attack, retreat, hold fire... orders were cut before 2005) and stay unused.

## Unavoidable differences

- Effects that needed the Xbox's pixel shaders are approximated: the bloom, the pause-menu blur and the sniper scope's
  live lens are reproduced on the Direct3D 9 renderer (on by default, as in 2005; off on OpenGL/Direct3D 11);
  screen-space refraction is not.
- Saves use the port's own format: Xbox saves are not imported; when a save is loaded, a scripted character restarts
  its current scripted action from its beginning (the Xbox resumed mid-action); saves from a newer version of the port
  are refused with a message.
- The developers' debug menu and pad rumble are not included. Perception's cheat codes work from the console in single
  player ([docs/CHEATS.md](docs/CHEATS.md)); the few that needed engine code UT2004 lacks are unavailable (astral
  sight's see-through-walls view, log filters, movie tests).
- OldUnreal reads controllers through DirectInput: LT and RT pressed together cancel out, there is no rumble, and the
  controller must be connected before the game starts. The Xbox white/black buttons are LB/RB, as on the Xbox 360.

_Maintained by the port team: every new deviation from the 2005 build must be added here._
