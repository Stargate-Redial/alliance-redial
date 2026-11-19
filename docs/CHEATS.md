# Cheats and console commands

**English** · [Français](#français)

The December 2005 build still contains the cheat codes its developers used for testing. The Xbox had no keyboard
and no console, so nobody could type them; on PC you can.

- **Single player only.** Cheats work in a game you play alone. Any network game refuses them, LAN or online,
  even on the PC that hosts it (UT2004's rule).
- They change nothing until you type them, and they are not saved: after a level change or after loading a
  checkpoint or a quick save, type them again.
- They can break a mission: read [Before you cheat](#before-you-cheat).

See also the [player guide](GUIDE.md) and the [known issues](KNOWN_ISSUES.md).

## Opening the console

| Keyboard | Console key |
|---|---|
| US QWERTY | `` ` `` / `~`, left of `1` |
| French AZERTY | `²` (left of `1`) or `ù` (right of `M`) |

On other layouts it is the key Windows calls `VK_OEM_3` (the `` ` `` key of a US keyboard). To use another key,
close the game and add a line such as `F8=ConsoleToggle` under `[Engine.Input]` in
`<UT2004>\SGAlliance\System\SGAllianceUser.ini`.

Type a command and press Enter; press the console key again to close the console. Commands are not
case-sensitive. Replies appear in the console; a few commands only write to the log (`<UT2004>\System\UT2004.log`).

## Cheats

### Health

| Command | Effect |
|---|---|
| `god` | You take no damage from enemies. Type it again to turn it off. As in 2005, damage without an attacker (falls, drowning, hazards) still hurts. |
| `phil` | Same as `god`. |
| `sg1god` | `god` for you and for your SG-1 squad mates. Type it again to turn it off for everyone. |

### Weapons

| Command | Effect |
|---|---|
| `loaded` | Every weapon of the game, with full ammunition. |
| `allweapons` | Every weapon of the game (18, including some that no mission hands out). |
| `allammo` | Full ammunition (999) for the weapons you carry. |
| `resetweapon` | Puts a stuck weapon back in its idle state. |

### Moving

| Command | Effect |
|---|---|
| `fly` | Fly where you look. |
| `ghost` | Fly through walls. |
| `walk` | Back to normal after `fly`, `ghost` or `teleportto`. |
| `teleport` | Jump to the spot you are looking at. |
| `teleportloc (X=0,Y=0,Z=0)` | Jump to these coordinates. |
| `teleportto <ActorName>` | Jump to a named object of the level (turns `ghost` on: type `walk` afterwards). |
| `setspeed 2` | Run, swim and fly twice as fast (`setspeed 1`: normal). |
| `setjumpz <value>` | Jump height: a higher value jumps higher. |
| `setgravity <value>` | Gravity of the area you are in (negative; closer to 0 = lighter). |
| `amphibious` | Breathe under water. |
| `changesize <factor>` | Your size times the factor (`changesize 1`: normal). |
| `invisible 1` / `invisible 0` | Enemies cannot see you / back to normal. |
| `unstick` | Back to the level's player start. |
| `assemblemembers` | Your squad mates teleport to you (useful when one of them is stuck). |
| `toggleteleport` | Turns off (or on again) the squad's automatic catch-up teleport. |

### The world

| Command | Effect |
|---|---|
| `slomo <speed>` | Game speed: `slomo 0.5` half speed, `slomo 1` normal. |
| `setserverslomo <speed>` | The same, with the game's own command. |
| `killtarget <Tag>` | Kills the characters that carry this Tag (a level-design name). |
| `takedamage <Tag> <amount>` | Damages them. |
| `killpawns` | Kills every other character of the level, your squad included (most missions cannot go on). |
| `killall <Package.Class>` | Kills every actor of a class, e.g. `killall StargateContent.JaffaGrunt`. A UT2004 command: also allowed to the host of a network game. |
| `summon <Package.Class>` | Creates an object in front of you, e.g. `summon StargateContent.P90Pickup`. |
| `playersonly` | Freezes everything except you; again to resume. |
| `freezeall` | The same, physics included. |
| `causeevent <Event>` | Fires a level event (for testing level scripts). |
| `showtriggers` | Unhides the level's trigger objects (for level-design debugging). |
| `end` | Ends the game at once, as a level's end trigger would (a developer test): the action stops; load a checkpoint or restart the chapter from the menus. |

### View and screen

| Command | Effect |
|---|---|
| `togglehud` | Hides the HUD (portrait, bars, weapon panel, crosshair), or shows it again. |
| `sethud 0` / `sethud 1` | Hides / shows the HUD. |
| `toggleweapon` | Hides or shows your first-person weapon. |
| `astral` | Jackson's astral sight screen effect, on or off (see [Not available](#not-available)). |
| `puss` | Scarab slime over the screen, for 10 seconds. |
| `behindview 1` / `behindview 0` | Third-person / first-person view. |
| `viewclass Pawn` | Look through the next character's eyes (repeat to go on); `viewself` to come back. |
| `freecamera 1` / `freecamera 0` | Third-person camera that turns freely around you / normal. |
| `setcameradist <distance>` | Distance of the third-person camera when you drive a vehicle (in hundreds of units; 2 at least). |

## Starting any mission

- **Main menu → Continue** opens the list of every map of the build.
- Or type `open <map>` in the console, e.g. `open SGA-M02A`. Story missions are named `SGA-M<number><part>`, from
  `SGA-M00` to `SGA-M21D` (the build has no M01, M03, M05, M06, M08, M09 or M11). Multiplayer maps are
  `SGA-DM-*`, `SGA-CTF-*` and `SGA-SGCTF-*`.
- The part starts from its beginning, with the equipment the level gives. Checkpoints work as usual.

## Before you cheat

- Missions are driven by scripts that wait for you to reach a place, use a device, or for a character to arrive.
  Flying, ghosting or teleporting past a trigger, or killing a character the story needs (`killpawns`,
  `killtarget`, `killall`), can leave a mission impossible to finish. If that happens: pause menu → Restart
  Chapter, or Continue from the last checkpoint.
- `god` only stops damage from attackers: watch out for falls.
- What a cheat gave you is part of your inventory, so a checkpoint reached afterwards may keep it.

## Not available

- **Astral sight**: `astral` shows its screen effect, but the 2005 engine also drew living beings through walls
  with code UT2004 does not have.
- **Log filters** (`DisplayLogFilters`, `AddLogFilter`, `RemoveLogFilter`, `ClearAllLogFilters`) and
  `LogTimeInfo`: engine features UT2004 does not have.
- **Movie tests** (`PlayM`, `PauseM`, `StopM`, `ShowMovie`): the build has neither the movie player nor movie files.
- `ShowDebugIcons` / `HideDebugIcons` are accepted but show nothing: their display was already switched off in
  the 2005 build. `ViewActor <name>` works, without the 2005 build's extra Tag/Event filters.
- The debug menu (Escape) and the F1–F4 debug keys of the earlier PC prototype's readme are not in this build.
  Closest commands: `viewclass Pawn` (F1), `viewself` (F2), `ghost` + `invisible 1` (F3), `walk` + `invisible 0` (F4).
- UT2004's tournament cheats (`skipmatch`, `jumpmatch`, `winmatch`, `weakobjectives`, `disablenextobjective`) do
  nothing in this game.

## Français

La version de décembre 2005 contient encore les codes de triche que ses développeurs utilisaient pour leurs
tests. La Xbox n'avait ni clavier ni console, donc personne ne pouvait les taper ; sur PC, c'est possible.

- **Solo uniquement.** Les codes fonctionnent dans une partie jouée seul. Toute partie en réseau les refuse,
  en LAN comme en ligne, même sur le PC qui l'héberge (règle d'UT2004).
- Ils ne changent rien tant qu'on ne les tape pas, et ils ne sont pas sauvegardés : après un changement de
  niveau ou le chargement d'un point de contrôle ou d'une sauvegarde rapide, retapez-les.
- Ils peuvent bloquer une mission : lisez [Avant de tricher](#avant-de-tricher).

Voir aussi le [guide du joueur](GUIDE.md#français) et les [problèmes connus](KNOWN_ISSUES.md#français).

### Ouvrir la console

| Clavier | Touche de la console |
|---|---|
| AZERTY français | `²` (à gauche de `1`) ou `ù` (à droite de `M`) |
| QWERTY américain | `` ` `` / `~`, à gauche de `1` |

Sur les autres dispositions, c'est la touche que Windows appelle `VK_OEM_3` (la touche `` ` `` d'un clavier
américain). Pour utiliser une autre touche, fermez le jeu et ajoutez une ligne comme `F8=ConsoleToggle` sous
`[Engine.Input]` dans `<UT2004>\SGAlliance\System\SGAllianceUser.ini`.

Tapez une commande puis Entrée ; appuyez de nouveau sur la touche de la console pour la fermer. Majuscules et
minuscules sont équivalentes. Les réponses s'affichent dans la console ; quelques commandes écrivent seulement
dans le journal (`<UT2004>\System\UT2004.log`).

### Codes de triche

#### Santé

| Commande | Effet |
|---|---|
| `god` | Vous ne subissez plus de dégâts de la part des ennemis. Retapez-la pour l'arrêter. Comme en 2005, les dégâts sans attaquant (chutes, noyade, pièges) font toujours mal. |
| `phil` | Identique à `god`. |
| `sg1god` | `god` pour vous et pour vos coéquipiers de SG-1. Retapez-la pour l'arrêter pour tous. |

#### Armes

| Commande | Effet |
|---|---|
| `loaded` | Toutes les armes du jeu, munitions au maximum. |
| `allweapons` | Toutes les armes du jeu (18, dont certaines qu'aucune mission ne donne). |
| `allammo` | Munitions au maximum (999) pour les armes que vous portez. |
| `resetweapon` | Remet une arme bloquée au repos. |

#### Déplacements

| Commande | Effet |
|---|---|
| `fly` | Voler dans la direction du regard. |
| `ghost` | Voler à travers les murs. |
| `walk` | Retour à la normale après `fly`, `ghost` ou `teleportto`. |
| `teleport` | Se téléporter à l'endroit visé. |
| `teleportloc (X=0,Y=0,Z=0)` | Se téléporter à ces coordonnées. |
| `teleportto <NomDObjet>` | Se téléporter sur un objet nommé du niveau (active `ghost` : tapez `walk` ensuite). |
| `setspeed 2` | Courir, nager et voler deux fois plus vite (`setspeed 1` : normal). |
| `setjumpz <valeur>` | Hauteur de saut : plus la valeur est grande, plus le saut est haut. |
| `setgravity <valeur>` | Gravité de la zone où vous êtes (négative ; plus proche de 0 = plus légère). |
| `amphibious` | Respirer sous l'eau. |
| `changesize <facteur>` | Votre taille multipliée par le facteur (`changesize 1` : normal). |
| `invisible 1` / `invisible 0` | Les ennemis ne vous voient plus / retour à la normale. |
| `unstick` | Retour au point de départ du joueur dans le niveau. |
| `assemblemembers` | Vos coéquipiers se téléportent près de vous (utile si l'un d'eux est coincé). |
| `toggleteleport` | Coupe (ou rétablit) la téléportation automatique qui ramène l'équipe près de vous. |

#### Le monde

| Commande | Effet |
|---|---|
| `slomo <vitesse>` | Vitesse du jeu : `slomo 0.5` moitié moins vite, `slomo 1` normal. |
| `setserverslomo <vitesse>` | La même chose, avec la commande propre au jeu. |
| `killtarget <Tag>` | Tue les personnages qui portent ce Tag (un nom de conception du niveau). |
| `takedamage <Tag> <quantité>` | Leur inflige des dégâts. |
| `killpawns` | Tue tous les autres personnages du niveau, votre équipe comprise (la plupart des missions ne peuvent plus continuer). |
| `killall <Paquet.Classe>` | Tue tous les acteurs d'une classe, par ex. `killall StargateContent.JaffaGrunt`. Commande d'UT2004 : également permise à l'hôte d'une partie en réseau. |
| `summon <Paquet.Classe>` | Fait apparaître un objet devant vous, par ex. `summon StargateContent.P90Pickup`. |
| `playersonly` | Fige tout sauf vous ; retapez-la pour reprendre. |
| `freezeall` | Pareil, physique comprise. |
| `causeevent <Événement>` | Déclenche un événement du niveau (pour tester ses scripts). |
| `showtriggers` | Rend visibles les déclencheurs du niveau (pour déboguer la conception des niveaux). |
| `end` | Termine la partie immédiatement, comme le ferait le déclencheur de fin d'un niveau (test des développeurs) : l'action s'arrête ; chargez un point de contrôle ou recommencez le chapitre depuis les menus. |

#### Vue et écran

| Commande | Effet |
|---|---|
| `togglehud` | Masque l'interface (portrait, barres, panneau de l'arme, réticule), ou la réaffiche. |
| `sethud 0` / `sethud 1` | Masque / affiche l'interface. |
| `toggleweapon` | Masque ou affiche votre arme en vue subjective. |
| `astral` | L'effet d'écran de la vision astrale de Jackson, activé ou non (voir [Non disponible](#non-disponible)). |
| `puss` | De la bave de Scarabée sur l'écran, pendant 10 secondes. |
| `behindview 1` / `behindview 0` | Vue à la troisième / à la première personne. |
| `viewclass Pawn` | Voir par les yeux du personnage suivant (répétez pour continuer) ; `viewself` pour revenir. |
| `freecamera 1` / `freecamera 0` | Caméra à la troisième personne qui tourne librement autour de vous / normale. |
| `setcameradist <distance>` | Distance de la caméra à la troisième personne quand vous conduisez un véhicule (en centaines d'unités ; 2 au minimum). |

### Lancer n'importe quelle mission

- **Menu principal → Continue** ouvre la liste de toutes les cartes de la version.
- Ou tapez `open <carte>` dans la console, par ex. `open SGA-M02A`. Les missions de l'histoire s'appellent
  `SGA-M<numéro><partie>`, de `SGA-M00` à `SGA-M21D` (la version n'a pas de M01, M03, M05, M06, M08, M09 ni M11).
  Les cartes multijoueur sont `SGA-DM-*`, `SGA-CTF-*` et `SGA-SGCTF-*`.
- La partie commence à son début, avec l'équipement que donne le niveau. Les points de contrôle fonctionnent
  normalement.

### Avant de tricher

- Les missions sont pilotées par des scripts qui attendent que vous atteigniez un endroit, que vous utilisiez un
  appareil ou qu'un personnage arrive. Voler, traverser les murs ou se téléporter au-delà d'un déclencheur, ou
  tuer un personnage dont l'histoire a besoin (`killpawns`, `killtarget`, `killall`), peut rendre une mission
  impossible à terminer. Dans ce cas : menu pause → Restart Chapter, ou Continue depuis le dernier point de
  contrôle.
- `god` n'arrête que les dégâts infligés par un attaquant : attention aux chutes.
- Ce qu'un code vous a donné fait partie de votre inventaire : un point de contrôle atteint ensuite peut le
  conserver.

### Non disponible

- **Vision astrale** : `astral` affiche son effet d'écran, mais le moteur de 2005 dessinait aussi les êtres
  vivants à travers les murs, avec du code qu'UT2004 n'a pas.
- **Filtres du journal** (`DisplayLogFilters`, `AddLogFilter`, `RemoveLogFilter`, `ClearAllLogFilters`) et
  `LogTimeInfo` : fonctions du moteur absentes d'UT2004.
- **Tests de vidéo** (`PlayM`, `PauseM`, `StopM`, `ShowMovie`) : la version n'a ni lecteur vidéo ni fichiers vidéo.
- `ShowDebugIcons` / `HideDebugIcons` sont acceptées mais n'affichent rien : leur affichage était déjà coupé dans
  la version de 2005. `ViewActor <nom>` fonctionne, sans les filtres Tag/Event supplémentaires de la version 2005.
- Le menu de débogage (Échap) et les touches de débogage F1 à F4 du readme du prototype PC antérieur ne sont pas
  dans cette version. Commandes les plus proches : `viewclass Pawn` (F1), `viewself` (F2), `ghost` +
  `invisible 1` (F3), `walk` + `invisible 0` (F4).
- Les codes de tournoi d'UT2004 (`skipmatch`, `jumpmatch`, `winmatch`, `weakobjectives`, `disablenextobjective`)
  n'ont aucun effet dans ce jeu.
