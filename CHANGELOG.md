# Changelog — differences from the December 2005 Xbox build

This port aims to reproduce the 2005 prototype exactly. Everything below is a deliberate, documented difference.
Each entry says why it exists. No game data is in this repository; all fixes are applied locally by the installer.

## Fixes to bugs present in the 2005 build (approved by the project lead)

- **Characters no longer slide upright for up to 2 seconds before their walk starts.** After a small drop (a step,
  a ledge, a bump in the ground) the engine holds the character's base animation for its landing, and the 2005
  scripts put the standing idle there at that moment (written for Perception's engine, which did not hold it): squad
  members and other characters then glided along in the idle pose until its 2-second cycle ended. A character that
  moves now gets its walk or run animation back at once.
- **Characters hold each weapon in its own pose again.** Perception's engine blended a second layer of animation
  over every character's upper body: the pose of the weapon in hand (staff, Zat, pistol, sniper rifle...), the
  idle fidgets, the crouch and sniper transitions and the alert gestures. The port's engine has no such layer, so
  none of it showed: everyone held every weapon in the P90 pose (Teal'c's staff stuck out sideways; online, staffs
  were carried upright like walking sticks). The layer works again as in 2005, for every character, on every PC
  of an online game; as in 2005 it steps aside in scripted scenes, vehicles and seats, and for the dead.
- **Characters standing still no longer make footstep sounds.** The upper-body layer above kept playing the run
  animation, unseen, on characters standing still, and its footstep marks went on sounding: every standing
  character made a step noise about every half second (earlier Redial releases only). Enemies heard those steps
  through walls and stayed suspicious instead of carrying on with their script: in M13C (*Attack on the Tok'ra Base
  III*) the Jaffa never blew the crystal wall open after Carter's "Incoming", so the passage stayed shut. Standing
  characters are silent again and the explosion comes; walking and running characters keep their 2005 footsteps.
- **First-aid prompt**: it names the teammate as the squad menu does ("Press [E] to administer first aid to
  CARTER") instead of the object name the 2005 code printed ("... first aid to Carter0"). Characters without a squad
  name show their class name without the number (JONAS).
- **2005 tuning values inherited again.** Perception's engine gave a class the values of its parent class's section
  of the game's tuning files (`Tweak_*.ini`) for every key its own section left out. The port's engine did that only
  when the parent class happened to be loaded first, so some values depended on the order the game loaded things
  in. Each class's tuning section now carries the keys it inherited in 2005, so it gets the 2005 values every time.
  The most visible case: the Assault pack's P90 (the P90 with torch) online was drawn below the screen, so you saw no
  gun in your hands, and it fired no tracers; it is now in your hands with its tracers, like the standard P90.
- **Characters leaving a vehicle walk off normally**: they no longer keep the seated pose until something else
  changes their stance (Perception's engine reset the animations when a character left a seat).
- **Characters jump and land with their 2005 animations again.** Perception's engine played a character's take-off
  animation when it jumped, kept it in the jump pose in the air and played its landing animation when it touched
  down standing still. The port's engine did none of it: squad members, enemies and, online, other players walked
  or ran in the air and ran on the spot for a moment after landing. They now take off, hang in the jump pose and
  land as in 2005.
- **Crouching characters crouch on their legs too.** A character crouching in place (the player seen by others
  online or in third person, squad members, enemies) stood on straight legs, crouch-walked in the standing run and
  kept the crouch set after standing up: the port's engine played the standing idle and walk there. Crouching
  and standing up now set the 2005 crouch animations (kneeling idle, crouch walk) and the 2005 crouch and stand-up
  transitions play, on every PC of an online game.
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
- **Mission 10 (mines, M10D)**: the SuperSoldier now follows Teal'c onto the bait ledge; it stood still after the
  dialogue and the level could not be finished (an enemy-tracking flag left set by a scripted state, apparently
  already in the 2005 build).
- **Two cutscenes at once no longer leave you without control.** The 2005 cutscene code kept one saved character
  per player for all cutscenes: when a second cutscene started while one was playing, both ended without giving the
  player their character back (black screen, the level could not go on). This happened in M12D when the Jaffa
  captain's cutscene was still playing as the outpost blew up. The player now gets control back when the last
  cutscene ends.
- **M17D: planting the C4 on the fake artifact early no longer blocks the level.** The C4 can be planted as soon as
  you reach the artifact, but the level only listened for it after Carter and Teal'c's lines: a C4 planted earlier
  went unheard and the level never ended. The level now remembers that the C4 was planted (and went off), with the
  2005 designers' own setting for such waits.
- **M13C: killing the last Jaffa captain before Jacob gets there no longer blocks the end.** Jacob is meant to
  remember that the captain is already dead, but the game only kept the last 64 events and the level's constant
  tremors used them up within minutes: Jacob then waited for good and the final scene never started. The game now
  keeps the last 1,024.
- **M07D**: the third Jaffa wave of the priests' puzzle comes when the team returns to the alcove after deciphering (its
  trigger was never switched on; it now arms together with the alcove trigger next to it).
- **M02A**: after the intro, Major Gray finishes his animation and walks off instead of standing frozen (he waited for
  a dialogue line that was cut from the game; he now waits for the line before it).
- **The "PLACE-HOLDER" banner is gone from story cutscenes.** Perception marked its unfinished cutscenes with a
  full-screen "PLACE-HOLDER" picture over the scene (M07, M10, M12, M13, M17, M18, M19, M21: 72 cutscene parts
  in 28 maps). The cutscenes now play without it; nothing else in them changes.
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
- **On-screen keyboard** (player name): the Space key types a space and no longer presses the selected on-screen
  key (with *Done* selected it closed the keyboard).
- **`togglehud`** (console) also hides the shield, stamina and ammunition bars; in 2005 they stayed on screen.
- **Multiplayer Internet list**: servers returned by the master servers now appear in the list. In 2005 each new
  game-type query cancelled the previous server-detail requests, so late replies were dropped and the page showed
  "No matching games were found".
- **Ribbon device and frag grenade pickups** (multiplayer maps) no longer look like a P90: the 2005 build used P90
  meshes as placeholders for them. The ribbon device lies as the Goa'uld device the 2005 DM-Ha'tak ribbon pickup shows,
  frag grenade pickups show the frag grenade itself.
- **Ribbon device icon**: the Goa'uld ribbon device (and the Hand of Light, which shares its icon) showed a magenta
  placeholder in the HUD weapon box, the weapon list and the multiplayer pack contents; the same silhouette is now light
  grey, like the other weapon icons.
- **Pickups riding a moving object in network games**: on DM-Langara the missile launcher rides the train, but
  players saw it where it first was, even with no train there, and pressing Use on it did nothing. It now moves with
  the train on every screen and is picked up from the carriage.
- **Multiplayer: the Mission Information page can always be closed.** In 2005, dying with it open brought up the
  scoreboard over it and left the menus without input, so the page stayed on screen for the rest of the game. The
  scoreboard now waits until the page is closed.
- **Key rebinding** (Options → Controls) no longer binds the Enter that starts the change, and the new key replaces
  the chosen key instead of being added to it. Each action has two keys (Key 1 / Key 2, as the 2005 PC profile stored
  them), picked with Left/Right or a click; Delete clears the chosen key.
- **Chapter Selection**: every chapter name fits its row (the list draws them a little smaller), so the chapters of
  one mission can be told apart.
- **Solo progress at a glance (addition, PC convenience).** The Single Player menu shows "Progress: N % - chapter X/Y"
  and Chapter Selection marks each chapter: done chapters have a check mark and a green name, the current one (the
  furthest reached) a gold arrow and a gold name, chapters not reached yet a grey name (the icons are the 2005 GUI
  textures' check box mark and arrow); it opens on the current chapter, selected (2005: on the first). The progress
  line sits inside the menu panel, under the buttons. The furthest chapter is derived from the story progress record and
  checkpoint saves, the same data as Continue. Every chapter can still be picked, as in 2005.
- **First chapter renamed "Training (Tutorial)".** The 2005 chapter list names its first entry "Mission 1 Replicator
  Attack" and points it to a map that is not in the build (m01a); the port starts the tutorial (M00) from it, so it is
  shown under the name of what it starts (a localized string).
- **Mission briefings in Chapter Selection (addition, project lead's decision).** The left side of the page shows the
  selected chapter's 2005 mission briefing (Location, Local time, then the briefing text, as the in-game Mission Info
  BRIEFING tab shows it) above the chapter's name, in the 2005 briefing box, font and colour; it follows the selection
  like the name. The text is each map's own briefing, read from your copy of the game by the installer: 53 of the 61
  chapters have one (M17B and M17D keep theirs in another field of the map, used as is); M02A-D, M14A-C and M15A have
  none in the 2005 data and show only their name, as before.
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
- **Multi-Player → Split-Screen and Edit Game Modes are hidden**: two 2005 Xbox leftovers with no page behind them
  (Split-Screen was local play on one console, never built; UT2004 has no split screen). As with Extras, no gap is left.
- **Hosted games are named after the host's multiplayer name** (2005 named LAN games "Unnamed" and Internet games
  after the profile).
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
- **Characters no longer sink into some static-mesh floors.** A few collision models of the 2005 meshes are not
  solid under the floor their mesh shows, so characters stood or walked in it up to the waist: the grated walkway
  where the squad starts M20A, ground pieces of the M02A/M02B jungle and of the M13D caves, the M02B bridge, a log
  bridge and a watchtower floor in M14C. Shots and the camera already used the visible surface. When a level
  loads, the map's own paths are checked; a mesh with such a hole on a path now uses its visible surface for
  characters too (28 meshes in 14 missions; none in the multiplayer maps).
- **Headshot deaths**: a character killed by a headshot whose model has no headshot animation (SG-1, Goa'uld, NPCs,
  soldiers; only the Jaffa have one) stayed standing, frozen, forever. It now falls like any other death.
- **Stargate iris with an open wormhole** (main menu background, end of M17D): the scripts close the iris and then shut
  the wormhole down, but the 2005 gate ignored that second order. The event horizon stayed on in front of most of
  the closed iris, and the menu's gate never dialled again. A gate whose iris is closed now shuts down when its
  script asks; gates without an iris behave as in 2005.
- **Long "New Objective" notifications** shrink to fit their one-line frame (down to half size) instead of wrapping
  below it: 47 of the 228 objective names were too wide for the 2005 frame.
- **Long weapon names** (Ribbon Device, Missile Launcher, Shock Grenade) stay inside the HUD's weapon box: smaller
  text, cut with "..." when still too long.
- **Ammunition readout "clip / reserve"** (a PC convenience, not 2005): weapons with a magazine (P90, pistol,
  shotgun, sniper rifle) show the rounds in the clip and the spare rounds, for example `50 / 250`, under the
  weapon name. 2005 showed only the spare rounds (the clip was the bar, which stays). The Zat gun, ribbon device
  and staff weapon still show their charge in percent; grenades and C4 still show their count.
- **Select Team** shows which team is selected (2005 left the selection box to a list drawing UT2004 does not have).
- **Weapon effects in network games** (client of a server): the staff weapon's blasts are visible (2005 built their
  glow, impact and sound only where the shot was spawned, the server); bullet tracers show (online they start in the
  shooter's eye and destroyed themselves on the shooter at once; your own now leave your gun's muzzle as in single
  player); the other players see a human player's muzzle flash (2005 only counted the bots' shots); your own muzzle
  flash shows at the gun (it was spawned at the map's origin).
- **More weapon effects in network games**: the P90 with torch shows its tracers (its own torch light destroyed
  them at the muzzle); the staff weapon's charge counts (online every blast left with the smallest charge, glow and
  damage) and your own blast leaves the staff's tip; a staff blast or frag grenade that explodes close by shows its
  explosion to every player (it was removed on the server before anyone saw it); the P90 torch goes off when you
  switch weapons.
- **Staff weapon blasts in flight online**: your own blast leaves the staff's tip the moment you fire and flies all
  the way to its target, as in single player (online it appeared only after a round trip to the server, already
  about 350 units out, so close and medium shots showed little more than the impact); the other players' and the
  bots' blasts also fly from their weapon over their whole path. Damage, speed, charge and timing are unchanged.
- **Zat gun pulses in flight online**: the same for the Zat gun: your own pulse leaves at once as in single player,
  and the other players' and the bots' pulses fly over their whole path, close shots included (a pulse that hit
  within the server's first moment was never seen online). Damage and timing are unchanged.
- **Charge of the Zat gun, ribbon device and staff weapon in network games**: the HUD showed 0 and an empty bar on a
  client; it shows the charge. The 2005 charge itself is kept: about two Zat or ribbon shots on a full charge, full
  again in 6 seconds.
- **Staff weapon charge in network games**: the HUD's charge percentage goes back to 0 % after each shot, as in
  single player (online it kept the last charge until the next one). Damage, charge time and blasts are unchanged.
- **Sniper rifle and binoculars in network games**: after leaving the scope the weapon stayed raised to the eye until
  the next shot, and the scope toggle right after a shot was ignored. With the mouse scope, a right button still held
  when the scope animation ends no longer strikes with the weapon (single player too).
- **Weapon menu in network games**: each weapon you selected was greyed out a moment later (UT2004 reported it out of
  ammunition), until the mouse wheel and the number keys only opened the menu without switching.
- **Weapon menu in network games after a respawn**: two weapons of the same slot (the pistol and the Zat gun, the C4
  and the frag grenade) shared one menu entry, so one of them, often the Zat, could no longer be chosen from the
  menu while the HUD showed it in hand. Each weapon has its own entry again (single player was not affected).
- **Mouse wheel in network games with a weapon pack**: the weapons the server gives at spawn reached your game
  after the weapon menu was built, so no weapon was highlighted: the wheel could not leave the first weapon and the
  HUD showed no weapon (the number keys worked). The menu now follows the weapons you really hold (spawn, respawn,
  Change Character, pick-ups, weapons replaced or used up), and after your last grenade online the empty grenade
  leaves the menu and you switch to your best weapon, as in single player.
- **Weapon packs at the respawn in network games**: you could appear with a grenade (or the C4) in hand that was then
  swapped for your main weapon, the Marksman pack started on the pistol, and pack weapons could take a few seconds to
  appear in the weapon menu. You now appear holding the pack's main weapon (P90, shotgun, sniper rifle, Zat gun or staff
  weapon for the Tau'ri; staff weapon, Zat gun or ribbon device for the Goa'uld), every pack weapon already in the menu.
- **C4 in network games**: after the first charge the C4 stayed in its firing pose (it has no firing animation): no
  detonation and no weapon change until you died, and the detonator started a melee strike on the server. Placing
  and detonating now play as in single player; with every charge placed the C4 stays in hand until you detonate,
  then you switch to your best weapon.
- **C4 in first person**: two large dark sleeve pieces no longer cover the left and right edges of the screen.
  They were the upper arms of the first-person arms, which the 2005 C4 animations hang right in front of the eye.
  The upper arms are now kept out of view; the hands, forearms, charge and detonator move exactly as in 2005, in
  single player and online, at every screen shape.
- **Reload key (R)**: it did nothing, in single player and online (UT2004's own reload command is empty; Perception's
  engine passed it to the weapon). It reloads the weapon in hand again, with its reload animation, on a server too
  (P90, pistol, shotgun shell by shell, sniper rifle). An empty clip still reloads by itself.
- **Cloak and weapon change**: a weapon taken out while cloaked was fully visible, and the weapon put away came
  back see-through after the cloak ended. The cloak now passes to the weapon you take out, as in 2005.
- **Last weapon key (Q)** no longer takes the binoculars out again after you used them (2005 rule, lost in the
  port: the key only switches between real weapons).
- **Idle animations in single player**: characters standing still play their weapon's idle fidgets again (none
  ever played in the port), and Jaffa snipers keep walking while they aim, as in 2005.
- **One weapon per slot in the campaign**, as in 2005: the pistol and the Zat, the P90 and the shotgun, the sniper
  rifle, the staff weapon and the Stinger share a slot, and picking one up drops the one you carry there, as the
  prompt says ("Press [E] to drop P90 and pick up SHOTGUN"; the port kept every weapon). Binoculars, grenades, C4 and
  the Goa'uld devices have no slot. Multiplayer keeps every weapon (the packs give the pistol and the Zat together).
- **Pausing pauses the sounds**: the pause menu, Mission Info and hint pages pause the sounds, the dialogue and the
  music, which resume where they stopped, as in 2005 (in the port, dialogue and sounds went on under the pause).
- **Cloak online** (project lead's decision; it did not work in 2005 network games either): the cloak key works for
  a player connected to a server, not only for the host. As in single player it drains the shield, ends when you
  fire, and your weapon cloaks with you; other players see the cloak, the weapon in hand included.
- **Electric arcs on Zat, Kull disruptor and electrified-fence victims**: the thin cyan-to-magenta arcs that crawl
  from the hit point over the victim's whole body for about a second and a half never appeared in the port (their
  2005 code was part of the engine, which the build does not include). They are back as the 2005 code drew them, in
  single player and online, where every player who can see the victim sees them.
- **Chapter Selection no longer starts a chapter on one click.** In the PC port a single click on a chapter started it at
  once, so the 2005 briefing on the left could not be read. A click (or the arrow keys) now only selects the chapter and
  shows its briefing; the mouse over a row only lights it. A chapter starts with a double click, Enter (pad A) or the
  **Start** button at the bottom right.

- **Four small screen fixes.** The "Progress" line of the Single Player menu is drawn only once the panel has slid into
  place (it flashed in the middle of the screen). A long "Objective Complete" or "New Objective" notification stays on
  one line inside its box in a small window instead of wrapping under the frame. The text the server shows when you join
  (its message of the day) is wrapped to the window width instead of being cut at the left in a small window. In Team
  DeathMatch the in-game scoreboard shows the names in the team colours of the 2005 team scoreboard (red for team 0, blue
  for team 1).
- **Bullet tracers fired at you online**: in a network game the tracers of the P90, pistol and sniper rifle fired by
  other players and bots now leave the shooter's gun and fly their whole path, as in single player. Online they started
  at the shooter's eye and the server moved them before sending them, so a tracer fired at you arrived beside your face
  and showed for one frame at most, or never when the shot hit you at once (measured through our server: 0 of 36 P90
  shots at 600 units showed a tracer). Shots, damage and timing are unchanged. The shotgun has no tracers, as in 2005.
- **Goa'uld shock grenade flash through walls**: its white flash is drawn only while you can see the blast. Its large
  white sprites and rings face the camera at the blast's distance, so a grenade going off behind a wall at your side
  washed your whole room white, in single player and online. A blast in view looks as in 2005; the stun is unchanged.
- **Other players' poses online**: on a client of a server, the other players and bots playing an SG-1 character kept
  their character's default relaxed pose: a walking cycle at full running speed and the weapon held low, a staff
  upright at the side like a walking stick. They now move and stand as on the server and in single player, in the
  combat stance 2005 gives every character in multiplayer.
- **Tok'ra weapons**: the Tok'ra (multiplayer character; Jacob/Selmak and the armed Tok'ra of the campaign) aimed and
  fired with empty hands, because their skeleton has no weapon bone. Their weapon is now held in the right hand, where
  the other characters' weapon bone sits.
- **C4 in the hand**: a player holding C4 showed a P90 to the other players (2005 gave the C4 the P90's third-person
  model). The game's own C4 pickup model is now held instead, and it is gone from the hand once the last charge is placed.

## Additions for PC playability and modern standards

- **Online, other players now visibly react to hits** (purely visual): in 2005 the hit reactions (the flinch when
  shot) played on the server only, so a network client saw the other characters stay upright. The server now tells the other
  machines about each hit and they play the same 2005 animations (at most one flinch every 0.3 s, so a burst of
  P90 fire does not make a character shiver). No change to damage, timing or the single-player campaign.
- **P90 torch: soft light and an on/off key** (deviation, project lead's decision): the torch projects the
  soft `Torch_Blob` of the same 2005 package instead of the lens photo the 2005 code named (rings and a seam).
  **L** (Controls row *Torch (P90)*) switches it off and on, online too; lit when raised, as in 2005, and off
  stays off while you keep that gun.
- **A torch on every P90 in the campaign** (project lead's decision): in the story missions the standard P90 has
  the same light as the P90 with torch on **L**; it stays off until you press the key. Multiplayer P90s are
  unchanged.
- **Real cinematic skip.** "Press [E] to Skip" ends the scene at once, using Perception's own hard-skip code, which no
  button reached in 2005 (only the cinematic's own scripts are fast-forwarded; the level ends up as after a full
  viewing). The original soft skip stays available: `[SGBase.SGSceneManagerBase] bHardSkip=False`.
- **Skip with your own Use key**: the prompt names the Use key ("Press [U] to Skip"), but a key bound to Use alone
  did not skip. Use now skips a cutscene whatever its binding, and Options → Controls lists such a key on the
  *Use / Skip Cutscene* row again.
- **Difficulty selector** on Options (Easy / Medium / Hard / Insane; default Hard, the 2005 default).
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
  bloom on/off (Direct3D 9 / Direct3D 11), scope depth of field (off by default), 3D audio (HRTF), sound channels, mouse smoothing. A new install starts with every graphics
  setting at its highest (UltraHigh textures, 16x anisotropic filtering, shadows, world detail, bloom), with only the 2005
  build's effects; an update keeps your own settings.
- **Bloom together with anti-aliasing**: the bloom, the pause-menu blur and the sniper scope's live lens now also
  work on the Direct3D 11 renderer, so its 2x–8x anti-aliasing no longer costs the 2005 glow. The glow now sits on
  its light and is blurred smoothly: before, it was pulled toward the middle of wide screens (a ceiling light's
  halo lay on the wall below it), too weak, and small lights left ghost copies around them.
- **Emissive glow** (Perception's PC effect; the Xbox build switched it off): lights, consoles, crystals and force
  fields of missions 15, 19, 20 and 21 glow softly, on top of the bloom; on with the Video page's Bloom row. The
  glowing materials are listed from your own copy of the game at install.
- **Scope depth of field** (Video row *Scope Depth of Field*, off by default; Perception's PC effect, absent from the
  Xbox build): in the sniper scope and the binoculars, what the crosshair points at stays sharp and nearer and
  farther things are softly blurred (Perception's code focused at a fixed distance per zoom step). Direct3D 9 and
  Direct3D 11; about 1.5 ms per frame while you look through the scope.
- **Restart prompt for settings that apply at the next start**: when you save the Video or Audio page after changing the
  Renderer, Anti-Aliasing, 3D Audio (HRTF) or Sound Channels row, a message offers *Restart now* or *Later* (also from the
  pause menu). *Restart now* starts the game again with the same shortcut options (the main menu opens again; a game in
  progress is not kept); *Later* keeps playing and the setting applies the next time you start. Nothing is shown when no
  such row changed.
- **Direct3D 11 safety net**: Direct3D 11 (an experimental choice on the Video page; Direct3D 9 stays the
  default) needs a Direct3D 11 graphics card (feature level 11_0). When it cannot start, the installer and the
  game's shortcut use Direct3D 9 (UT2004 would stop with an error), and a start that failed on Direct3D 11 makes
  the next one use Direct3D 9.
- **Sharper character and vehicle shadows**: the shadow texture is 512 x 512 instead of the engine's 128 x 128, so a
  shadow shows the outline of the body instead of a blurred blob. Same size, direction and darkness on the ground
  (Perception's own code listed 512 as the "High" shadow setting of a never-finished option).
- **Tree shadows** (addition; the 2005 build had none): trees cast a shadow on the ground, shaped like the
  tree and falling away from the sun (or the moon in the night jungle). In 2005 the jungle palms were left
  out of the maps' lighting, and terrain lighting is far too coarse to show a tree's shadow, so trees stood
  on evenly lit ground. The twelve nearest trees get a shadow (about 1 ms per frame); the *Shadows* row of
  the Video page turns them off together with the character shadows.
- **Shadows for every character** (addition): the SGC staff, the Tok'ra, Jacob and the other non-combat characters
  had no shadow in 2005 (their classes never asked for one), unlike SG-1 and the enemies. They now get the same
  shadow, switched by the *Shadows* row of the Video page. The invisible Reetou stays without one.
- **Shadows for rocks, statues, walls and other outdoor scenery** (addition): big rocks, statues, wall pieces,
  ruins, houses, tents, crates and similar scenery standing on open ground now cast a shadow on it too, like
  the trees (the six nearest pieces within about 130 metres), in the campaign and in multiplayer. In 2005
  their shadow was baked into the map lighting, which on open ground is stored far too coarsely to show it.
  Same *Shadows* row of the Video page.
- **Smoother skies**: the 2005 skies are small compressed textures stretched over the whole sky, so their
  4x4 compression blocks showed as square steps. On your PC the installer decodes the 29 sky textures (domes,
  bands, clouds, mist), smooths the block steps while keeping stars and outlines sharp, and stores them
  uncompressed (8.5 MB more on disk). Star fields, planets and world textures stay as they are;
  `--skies keep` keeps the 2005 textures.
- **Scenery no longer blinks in and out**: with the static-mesh batching of OldUnreal's UT2004 engine, lamps, pipes,
  crates and desk objects of the 2005 maps disappeared and reappeared every few frames, even standing still (seen
  in the SGC levels). The batching is switched off for every install, including existing ones; the cost is a few
  percent of frame rate.
- **More resolutions** in Options > Video: 2880x1620, 3200x1800 and 5760x3240, the sizes NVIDIA DSR and AMD
  VSR offer, listed when the display driver supports them.
- **Readable drop-down lists** on the Options pages: an open list (Texture Filtering, Resolution, Sound Channels,
  Pad Look Speed, Outfit...) shows its items in the same font and size as its closed box. In small windows the
  items were tiny capitals about 6 pixels high, and one size smaller than the box at higher resolutions.
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
  Bots are hurt by the Zat gun, the shock grenade and the ribbon device as players are (all three slow, and the Zat
  and the shock grenade then kill, by the rule below; before, these three weapons did nothing to a bot, whoever fired
  them), and they use the Zat's and the ribbon device's 2005 charge as players do (about two
  shots, then another weapon, or a grenade, while it refills). Bots fire the pistol, the P90, the shotgun and the
  sniper rifle at a player's rate (they fired two shots per firing animation).
  Bots play with UT2004's bot AI on a navigation network the
  game builds when the map loads (the 2005 multiplayer maps have none), and they use the Stargates, rings and
  ladders. Servers: `?MinPlayers=N` / `?BotSkill=0-7`, and the console commands AddBots, KillBots and SetBotSkill.
  Players joining need nothing.
  In Last Man Standing a bot that sees nobody goes looking for the other players instead of waiting or
  wandering: it heads for roughly where one of them is (the nearest, players before bots; it still has to see him
  to shoot), never more than one bot after the same player while six or more are left, two with four or five, and
  everyone once three are left. A bot backs off only when badly hurt and only for a few seconds (two bots could
  keep backing away from each other for the rest of a round), and it charges an enemy it sees out of its weapon's
  reach. On DM-Langara bots step off the train track when a train comes and wait at the side until it has passed.
  On DM-KelownanTrain bots no longer jump or step off the cars into the void (no jump or drop whose arc comes
  down out of the world, the edges of the cars avoided when they can); in every mode they charge an enemy they see
  out of their weapon's reach and, when they and the enemy they were after have just swapped places through the
  rings or a Stargate, wait there a few seconds (Last Man Standing only before: two bots could swap places through
  Ha'tak's rings or shoot at each other from deck to deck for minutes); they throw no grenade that would come down
  next to them (thrown at cover a few steps away) and run from their own grenade, they let go of a staff charge
  when the blast would reach them, and on DM-Langara they no longer run from a grenade onto the track in front of
  a train.
- **Project label on the main menu**: "Stargate Redial V0.1" and "by the Stargate Database team - stargatedatabase.link"
  in the bottom-right corner of the screen (outside the original 4:3 art on wide screens). Not in the 2005 build.

- **Installer**: every tool it runs is the project's own code (no third-party decompilation tools are downloaded),
  and the game files are checked against the project's own hash list.
- **Faster first start**: at its first start UT2004 lists the maps of the mod by loading each one's summary, which
  kept the logo screen up for minutes on a slow disk. The installer now has UT2004's own tool write that list
  (`<UT2004>\System\<map>.ucl`, the same files the game writes) after each install or update, in a few seconds, so
  the first launch reaches the main menu about as fast as the next ones. A UT2004 never started before still lists
  its own maps once. Uninstalling removes these files.
- **Installer: a game running from another folder no longer blocks the install.** The installer refused to run
  ("close UT2004.exe, UCC.exe first") whenever any UT2004, UCC or UnrealEd ran on the PC, even from another UT2004
  folder. It now counts only the ones started from the UT2004 folder it installs into (and names that folder).
- **Updates replace the update-check launcher**: an updated install kept the `SGAlliance\Launcher\Stargate
  Redial.exe` of its first version (the installer took it for unchanged: same size and same file date in every
  release zip). It is now compared by content and replaced when it changed.
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
- **Window title and taskbar**: the game window is titled "Stargate Redial: The Alliance" instead of "Unreal
  Tournament 2004". Started from the Play shortcut, it also shows the Redial icon (title bar, Alt+Tab, taskbar) and
  gets its own taskbar button named "Stargate Redial: The Alliance", apart from any plain UT2004 window; pinning that
  button pins the Play shortcut.
- **Shortcuts**: the game's shortcut is named "Stargate Redial - The Alliance" (was "Play Stargate SG-1 The
  Alliance"). The installer always adds it to the Start menu, and puts it on the desktop unless the box is unticked
  (ticked for a new install; an update keeps the previous choice). An update removes the old-named shortcuts.
- **Sharper HUD text at high resolutions**: subtitles and HUD labels use a larger size of the same 2005 font (the game
  font up to its Huge size, Tahoma up to 36 px) instead of magnifying the small one; same size and layout.
  `[SGBase.SGHudScale] bSharpFonts=False` restores plain magnification.
- **Sharper loading picture**: the 2005 loading picture is a small 512x512 compressed texture stretched across the
  whole screen (5 screen pixels for each of its pixels at 2560x1440), so it looked blocky in full screen. The
  installer now makes a 2048x2048 copy of the same picture on your PC (the compression blocks smoothed, then
  enlarged 4 times; no new art) and the loading screen draws it, framed exactly as before. An empty
  `HDBackgrounds=` under `[StargateGame.SGServerLoading]` in SGAllianceUser.ini brings back the 2005 texture.
- **Menus work with the mouse**: one click chooses a map, chapter, team, game mode or server (as Enter); on the
  multiplayer character pages a click only selects the character (picture, Outfit and Pack rows follow), and the
  *Start* button at the bottom right (*Next* when hosting, Enter or a double-click) confirms;
  in the saved game and Controls lists a click selects the row and a second click or a double-click
  chooses it. One item is highlighted at a time, as usual on PC: the button, option or list row under the mouse
  takes the highlight (and the focus Enter acts on), and the arrow keys, Tab and the pad still move it; a list's
  selected row stays framed, dimmed, while another control has the focus. Up/Down also move between buttons, like
  the pad's d-pad.
- **Exit Game button** on the main menu, from Perception's earlier main menu in the 2005 data; it asks for
  confirmation, like Escape.
- **Console**: the key that opens it (² on AZERTY keyboards) closes it again, and one Escape closes it. Tab also
  closes the Mission Information page (Escape only before).
- **Multiplayer outfits**: Options → Multiplayer has an *Outfit* row (Standard / Desert / Black)
  that dresses O'Neill, Carter, Jackson, Teal'c and Graham Coulder in the 2005 build's unused desert and black
  SG-1 uniform textures; every player sees it, bots pick one at random. Team games stay readable (SG-1 against
  Jaffa).
- **Multiplayer player name**: the same page has a *Name* box (on-screen keyboard with Ins or pad Y) for the
  name other players and the game list see; the default is *Player*.
- **Outfit and Name when hosting or joining**: the character page of the host and join flows has the same *Outfit*
  and *Name* rows as Options → Multiplayer (and its *Player Name (Ins)* button); what is set there is kept for the next games.
- **Multiplayer weapon packs** (project lead's decision, a deliberate change of the 2005 balance): every player gets
  the pack chosen under *Outfit* on the character pages and Options → Multiplayer (its contents shown with their icons
  in a box under the rows; one pack is remembered per side). Tau'ri, who keep the 2005 pistol: Assault = P90 + frag
  grenades, Close Quarters = Shotgun + C4, Marksman = Sniper rifle + frag grenades, Zat = Zat gun + frag grenades,
  Staff = Staff weapon + frag grenades. Goa'uld, who start without the pistol: Warrior = Staff weapon + shock grenades,
  Zat = Zat gun + shock grenades, Lord = Ribbon device + personal shield (the shield belt of the map pickup) + Zat gun,
  no grenades. Grenades and C4 come in the amount of their 2005 map pickups. The side is the team in team games, else
  the character (Jaffa and Goa'uld are Goa'uld; the Tok'ra, allies of Earth, are Tau'ri). Bots take a random pack of
  their side. The Stinger and the shield stay map pickups. A server keeps the 2005 pistol-only start for everyone with
  `?SGPacks=0` or `[SGBase.SGPacks] bPacks=False` (see SERVER.md).
- **Joining a Last Man Standing round already under way** (project lead's decision): if no other player is in the
  round (bots only), the round starts again at once, lives and scores back to the start, so you play it whole against
  every bot; if other players are in it, you watch with the spectator camera and play the next round.
- **A Last Man Standing round ends when one player is left**, also when the second-to-last player dies without a
  killer (his own grenade, a fall, a train); before, the round went on with a single player until the time limit.
- **Zat'nik'tel and shock grenade in multiplayer: the first hit slows, the second kills** (project lead's decision,
  a deliberate change of the 2005 balance, where one hit killed a player at once): in every multiplayer game the
  first Zat hit or shock grenade blast that reaches a player slows them to half speed for 5 seconds. They can still
  fire, aim, jump and change weapons, and Zat arcs crawl over them so everyone sees who is slowed. A second hit, Zat
  or shock grenade, from anyone, within those 5 seconds kills, credited to whoever fired it; once the 5 seconds are
  over, the next hit slows again. Nobody is knocked down any more (earlier Redial releases knocked the player down
  at the first hit). A charged personal shield still absorbs the hit first and prevents the slow; a teammate's Zat or
  shock grenade does nothing while friendly fire is off (in 2005 both killed teammates, and the shock grenade its thrower too); your
  own grenade follows the same rule; the shock blast reaches only the players in its line of sight (in 2005 it went
  through walls and floors). Bots are slowed and killed the same way and follow a slow up with a second Zat shot.
  Servers can tune the slow under `[StargateGame.StargateDeathMatch]`: `ZatSlowPct=0.5` (speed factor) and
  `ZatSlowTime=5.0` (seconds). The single player game keeps the 2005 rule.
- **Ribbon device in multiplayer: it slows instead of throwing back** (project lead's decision, as for the Zat and
  the shock grenade): its ball still does its 150 damage at once, then slows the player hit to half speed for 5
  seconds, with the Zat arcs, instead of throwing them back and keeping them down for 2 to 3 seconds. Every ball
  starts the 5 seconds again; the ribbon device never kills by the two-hit rule itself, but a Zat hit or shock
  grenade blast on a player it slowed kills. A charged personal shield (any charge left) prevents the slow and still
  absorbs the damage. Bots are slowed the same way and follow the slow up with the Zat. The single player game keeps
  the 2005 knock-back.
- **No knock-back in multiplayer** (project lead's decision): in every multiplayer game nothing throws a player or a
  bot back, knocks them down or makes them stagger any more. The frag grenade, the C4, the Stinger, the staff
  weapon's strikes and the other 2005 knock-backs only deal their damage, unchanged (a C4 charge or a melee strike
  deals it at once instead of when the victim lands). Blasts still push you as in UT2004, but you keep control. The
  Zat gun, the shock grenade and the ribbon device slow, as above. The single player game keeps the 2005
  knock-backs.
- **Change Character in game** (PC convenience): Escape → *Change Character* opens the character page (character,
  outfit, name, pack; in team games your team's characters only); *Apply* respawns you at once at a spawn point with
  the new character and pack, with no death, score or life counted. If you were hit in the last 5 seconds, carry a
  flag, drive a vehicle or are dead, the change waits for your next respawn, and a message says so.
- **No visible profiles: the game uses one automatic profile** (project lead's decision; 2005's profiles were for
  several players sharing one console, and 2005 asked for one on the Single Player, Multi-Player and Options paths).
  It is made without any page at the first launch (named *Player*, also the default multiplayer name) and holds the
  saves, checkpoints, quick saves, story progress, settings, keys and the multiplayer name, outfit and packs. No
  button or page selects, creates or deletes profiles, and Options opens straight on its options (2005: "Edit
  Profile", with a Name box for the profile). An install that already had profiles uses the one played last (else
  the one with the most recent save); the others stay on disk, untouched.
- **Extras hidden**: the main menu's *Extras* opened an empty 2005 placeholder page ("Extras should go here"); the
  button is hidden and Exit Game takes its step.
- **Continue in the Single Player menu too** (project lead's decision): the Single Player menu's first button is the
  main menu's Continue, with the same action (the most recent checkpoint or quick save) and the same rule (greyed
  while there is no save, checked again each time the menu shows); the 2005 buttons move down one step.
- **Real buttons for the menu actions** (project lead's decision, PC convenience): the 2005 prompts at the bottom of the
  menu pages ("[Esc] Back", "[Enter] Select") are framed buttons in the frame of the main menu's buttons, with the
  action first and its key after it: **Back (Esc)** on the left, the page's action on the right (**Select (Enter)**,
  **Load (Enter)**, **Start (Enter)**, **Next (Enter)**...), the others between them (**Delete (Del)**, **Player Name
  (Ins)**...). The button under the mouse lights up and takes the highlight; a click or Enter presses it, and it acts
  on the row or item the page had selected. Keys and the pad work as before; while the pad is in use, the 2005 pad
  icons come back.
- **Internet page Back button**: the Internet page (Create Match / Find Match) has a Back button like the LAN page (on
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
- **Multiplayer text chat** (user request): **T** talks to everyone, **Y** to your team (UT2004's Talk / TeamTalk),
  new Controls rows *Chat* / *Team Chat* (and *Screenshot*, F12, so the screenshot key can be changed); new and
  existing players get T / Y where those keys are free. The 2005
  Xbox game used the headset; its PC code only sent the console's `say` lines to the dialogue box, one at a time for
  2 s. They are now a chat list under the portrait (names in team colour, fading after 10 s), and the typing line
  is drawn at the bottom left in the HUD's style.
- **Discord feed: public chat** (user request): dedicated servers with the Discord feed also post players' public
  chat in the server's channel (sanitised, rate-limited; never team chat, never bots); the event log keeps those
  lines.
- **Quick voice menu** (user decision): in multiplayer, **V** (Controls row *Voice Menu*) opens a short list of
  lines your character says in its own 2005 voice (Taunt, Affirmative, Negative, Enemy spotted, Take cover,
  Concentrate fire, Ready: only those its 2005 voice pack has), heard by nearby players; the text shows in the chat
  list (team lines to the team). The 2005 Xbox game had only the headset; these lines were the story squad's.
  Deviation: the Jaffa (Horus, Serpent, Jackal) have no Taunt or Attack line in 2005, so their Taunt and Attack!
  entries play their own 2005 combat shouts (their attack recordings). Walter and Coulder, and the Goa'uld and Tok'ra,
  stay without lines (the SGC soldiers' voice pack is empty in the 2005 build).

## Perception's own PC code used instead of the Xbox variant

The game's scripts contain both Xbox and PC variants of some passages; the port uses Perception's PC variants (project
decision), except where a PC line is broken. Visible differences from the 2005 Xbox build:

- The notification box (checkpoints, objectives) uses the PC version's default HUD font; the Xbox build used SmallFont.
- The binocular zoom shows the PC version's static fuzz, growing with the zoom step; the Xbox build had none.
- The loading screen (between levels and while joining a server) shows the game's own loading picture, a Horus
  guard in a Stargate with "LOADING . . .", across the whole screen width as Perception's PC build showed it, instead
  of the Xbox controller layout (user decision). The game type's line and the map name are written small under it.
- Debug messages the 2005 build showed on screen are not shown: a red chat line when a scripted sequence broke, and a
  placeholder text for an empty notification.

## Restored (present in the 2005 build but never wired)

- **Last Man Standing** (multiplayer): Perception's complete mode (five lives; the last player with lives left wins) was
  switched off in the 2005 game-mode list; it is listed again under Multiplayer → Host, plays on the seven deathmatch
  maps and appears in the Internet server list.
- **Build stamp**: the 2005 build date is no longer shown on the main menu; only the Stargate Redial label is (bottom right).
- **Original Xbox button icons in the menu prompt bar**, shown while the controller is in use.
- **Squad members crouch out of your line of fire** when you shoot past them (switched off for the May 2005 E3 demo).
- **P90 with torch**: Carter's and Daniel's P90 in M20C and the six SGCTF-AbydosVsSGC pickups shine their flashlight
  while raised (in 2005 they were a plain P90).
- **Bullet and grenade effects per material**: glass, metal, metal grates, sand, snow, carpet, ice, dirt and grass get
  their own marks, wood its wood chips, water its own splash.
- **Windows shatter**: a window that breaks (DM-WorstCaseScenario, SGCTF-AbydosVsSGC, mission 18) bursts into glass
  shards that fall, settle and vanish after 10 s; the 2005 effect was switched off and could not even be created.
  Online every player sees the shards (each PC draws them; nothing extra is sent), and the burst of any breakable
  object (the Lost City pots...) now shows for every player, not only for the host.
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
- **Continue** (main menu) loads the most recent checkpoint or quick save, as its 2005 hint says ("Load the
  most recent saved game or checkpoint"); it is greyed when there is no save. In 2005 it opened a temporary
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
- **Squad orders Hold position and Follow me have keys**: **H** and **G** (Controls rows *Hold Position* and
  *Follow Me*, same keys on AZERTY). Both orders are in the 2005 game but had no key or button there (console
  commands only). Hold keeps each squad member where he or she stands, with the 2005 yellow arrow over each spot
  and the 2005 message; Follow me brings them back. A hold order is kept by saves and quick saves, as the 2005
  saves did. Existing players get H and G only where those keys are free. The GUIDE explains every squad order.

## Unavoidable differences

- Effects that needed the Xbox's pixel shaders are approximated: the bloom, the pause-menu blur and the sniper scope's
  live lens are reproduced on the Direct3D 9 and Direct3D 11 renderers (on by default, as in 2005; off on OpenGL);
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
