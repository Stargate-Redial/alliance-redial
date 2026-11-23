# Known issues (V0.1)

**English** · [Français](#français)

An honest list for V0.1. It has three parts: what the 2005 build itself did and the port keeps on purpose, the
limits of the port on PC, and what no person has checked yet. Bugs of the 2005 build that the port fixes, and
features it restores, are in [CHANGELOG.md](../CHANGELOG.md). How to play: [GUIDE.md](GUIDE.md).

## Kept from the 2005 build

The port reproduces the December 2005 prototype. The items below are how that build is, not port bugs. Some may
change in a later version if the project decides so.

### An unfinished game

- Missions 1, 3, 5, 6, 8, 9 and 11 are not in the build: the story jumps between missions.
- Many recorded voice lines (mission interludes, briefings, an ending that was never built) are in the files,
  but no level plays them.
- Not in the build, or never finished: co-op, split-screen and the *Edit Game Modes* page (both buttons are hidden), the
  *System Lord*, *Jaffa! Kree!* and *Enslave* multiplayer modes (their code is missing; *System Lord*, listed in
  2005, is hidden), Thor and the Kull as multiplayer characters (no animations),
  the vehicles and creatures that no level uses, Jackson's astral sight (no level uses it), the credits.
- The *Extras* page is an empty placeholder. Chapter Selection has no chapter pictures.
- Some objects show a plain white or grey surface where the 2005 data has no texture and no close match: for
  example the shield-belt pickup, the Goa'uld drone, the staff cannon's screen and some lights and beams in the
  levels.
- A few sounds and HUD icons the game asks for are not in the 2019 release (for example a staff weapon sound
  and the shotgun's melee sound): they stay silent or empty.
- Mouths move only in some levels' dialogue, and not in the Mission 2 introduction, as in 2005.

### Single player

- Saves are checkpoints and quick saves (no save menu). A save does not record everything: corpses, dropped
  weapons and projectiles are not kept, and some characters restart what they were doing.
- When the story switches to another SG-1 member (end of M07E to M10A, and one of the two exits of M16G), the
  new character arrives with the previous one's weapons, for example Teal'c without his staff weapon. Kept as in
  2005 for now.
- The difficulty also changes the strength of your allies.
- Some scripted scenes that are not cutscenes lock your movement, view or weapon for a while; they cannot be
  skipped.
- M15A: skipping the opening cutscene takes two presses.
- Vehicles have no health bar on the HUD.
- Subtitles cannot be switched off.
- M19A says "You've found a secret place." without a secrets counter.
- In M21D the music stops before the end of the level (its last bars are not in the build).
- First person: the shock grenade and the Jaffa staff are shown without hands, the shotgun looks pale, and the zat
  and the Goa'uld hand device have no melee animation.
- Jaffa holding a pistol, a shotgun or a Stinger show no firing pose: the 2005 data has no such animations for them.

### Multiplayer

- In Capture the Flag, bots take, drop and return the flags often but seldom bring one home (a match between bots
  can end 0-0): the whole enemy team hunts the carrier, and on CTF-LostCity each team starts next to the other
  team's flag (2005 map), so both flags are nearly always away and every run home ends among the enemy's starts.
- A match waits for two players (bots count), and each must press Fire to be ready; a host alone without bots
  waits.
- After a team match one more round is played; in Capture the Flag the next capture ends it at once.
- The Last Man Standing scoreboard has no lives column: lives left = 5 minus deaths.
- The Stargate of DM-WorstCaseScenario is a decoration: it has no DHD (dialling device) and never opens.

## Limits of the port

- **Effects of the Xbox's pixel shaders** are approximated. The bloom and the blur behind the pause menu are
  drawn with the Direct3D 9 (default) and Direct3D 11 renderers, not with OpenGL (on by default; Options → Video
  → Bloom turns them off). The heat haze
  and distortion of fires, explosions and force fields is not reproduced, and the Reetou's invisibility shows as
  a see-through sheen.
- **The sniper scope's lens** shows the view with Direct3D 9 and Direct3D 11; with OpenGL it is black.
- **Brightness** applies only in full screen with Direct3D 9 (OldUnreal behaviour); Direct3D 11 applies it in a
  window too.
- **Direct3D 11 is experimental** (Options → Video → Renderer): with anti-aliasing, character shadows can show
  square blocks, and text is softer than with Direct3D 9.
- **Controller**: read through DirectInput. LT and RT pressed together cancel out, there is no rumble, the
  controller must be connected before the game starts, only the first game controller is read, and the layout
  assumes an Xbox-style controller.
- **Astral sight**: the `astral` cheat shows its screen effect only; drawing living beings through walls needed
  engine code UT2004 does not have. The developers' debug menu and some debug commands are not available
  ([CHEATS.md](CHEATS.md#not-available)).
- **Internet play** uses OldUnreal's master servers: the Xbox Live sign-in, friends and player lists are not
  available. Everyone must have the same Redial version and the same OldUnreal build.
- Only one copy of the game runs at a time on a PC (OldUnreal behaviour).
- Now and then a squad member still fails to board the Hummvee. The `assemblemembers` console command brings the
  squad back to you.
- Vehicle physics lose a little speed at very high frame rates (a few percent at 144 fps, about 10 % at 300 fps):
  prefer a frame rate limit of 144 or 240.
- The Xbox build's checkpoint files (`.sgs`) cannot be loaded.

## Not yet checked by a person

Automated tests played every story part to its end, and the menus, HUD and main features were checked on
screen. These have not yet been checked by a person playing V0.1:

- a real game controller (the layout was tested without a physical controller);
- Internet games through the master servers (LAN games were tested), several real players on one server, Team
  DeathMatch from a player's side, a dedicated server on a real Linux machine;
- brightness in full screen with Direct3D 9, 3D audio (HRTF) by ear, the reverb of caves and halls, the bloom on
  21:9 and 4K screens;
- moments that the automated tests had to help through: M10A (destroying the Al'Kesh with the staff cannon),
  M13C (the opening), M18D (the security doors that open when you walk into them), M19D (Carter walking to the
  generator room), M20D (the throne room and the Kull), M21C (the pod-room door);
- the Stinger's lock-on and multiple targets, the mind-control crystals (M21), the force-field puzzle (M19B),
  painting targets with the binoculars (M19D, M19E), the C4 objective (M17D), using the transport rings (M20),
  the staff cannon and M60 emplacements, the disguises (M21).

If something goes wrong, see [Troubleshooting](GUIDE.md#troubleshooting) and report it on the
[GitHub repository](https://github.com/Stargate-Redial/alliance-redial/issues) with `<UT2004>\System\UT2004.log`.

## Français

Une liste honnête pour la V0.1, en trois parties : ce que faisait la version de 2005 elle-même et que le portage
garde volontairement, les limites du portage sur PC, et ce que personne n'a encore vérifié. Les bugs de 2005
corrigés par le portage et les fonctions restaurées sont dans [CHANGELOG.md](../CHANGELOG.md) (en anglais).
Comment jouer : [GUIDE.md](GUIDE.md#français).

### Conservé de la version de 2005

Le portage reproduit le prototype de décembre 2005. Les points ci-dessous décrivent cette version, ce ne sont pas
des bugs du portage. Certains pourront changer dans une version future si le projet le décide.

#### Un jeu inachevé

- Les missions 1, 3, 5, 6, 8, 9 et 11 ne sont pas dans la version : l'histoire saute d'une mission à l'autre.
- Beaucoup de répliques enregistrées (interludes, briefings, une fin jamais construite) sont dans les fichiers,
  mais aucun niveau ne les joue.
- Absents ou jamais terminés : la coopération, l'écran partagé et la page *Edit Game Modes* (les deux boutons sont
  masqués),
  les modes multijoueur *System Lord*, *Jaffa! Kree!* et *Enslave* (leur code manque ; *System Lord*, listé en
  2005, est masqué), Thor et les Kull comme personnages multijoueur (pas
  d'animations), les véhicules et créatures qu'aucun niveau n'utilise, la vision astrale de Jackson (aucun niveau
  ne l'utilise), le générique.
- La page *Extras* est vide. Chapter Selection n'a pas d'images de chapitre.
- Certains objets ont une surface blanche ou grise unie là où les données de 2005 n'ont ni texture ni texture
  voisine : par exemple la ceinture de bouclier à ramasser, le drone Goa'uld, l'écran du canon à bâton et
  quelques lumières et poutres dans les niveaux.
- Quelques sons et icônes d'interface demandés par le jeu ne sont pas dans la publication de 2019 (par exemple un
  son de la lance Goa'uld et le coup de crosse du fusil à pompe) : ils restent muets ou vides.
- Les bouches ne bougent que dans les dialogues de certains niveaux, et pas dans l'introduction de la mission 2,
  comme en 2005.

#### Solo

- On sauvegarde aux points de contrôle et par sauvegarde rapide (pas de menu de sauvegarde). Une sauvegarde
  n'enregistre pas tout : cadavres, armes lâchées et projectiles ne sont pas gardés, et certains personnages
  reprennent ce qu'ils faisaient depuis le début.
- Quand l'histoire passe à un autre membre de SG-1 (fin de M07E vers M10A, et l'une des deux sorties de M16G), le
  nouveau personnage arrive avec les armes du précédent, par exemple Teal'c sans sa lance. Conservé comme en 2005
  pour l'instant.
- La difficulté change aussi la résistance de vos alliés.
- Certaines scènes scriptées qui ne sont pas des cinématiques bloquent un moment vos déplacements, la vue ou
  l'arme ; on ne peut pas les passer.
- M15A : passer la cinématique d'ouverture demande deux appuis.
- Les véhicules n'ont pas de barre de santé à l'écran.
- Les sous-titres ne peuvent pas être désactivés.
- M19A affiche « You've found a secret place. » sans compteur de secrets.
- Dans M21D, la musique s'arrête avant la fin du niveau (ses dernières mesures ne sont pas dans la version).
- En vue subjective : la grenade paralysante et le bâton Jaffa apparaissent sans mains, le fusil à pompe paraît
  pâle, et le zat et le bracelet Goa'uld n'ont pas d'animation de coup au corps à corps.
- Les Jaffa qui tiennent un pistolet, un fusil à pompe ou un Stinger n'ont pas de pose de tir : les données de
  2005 n'ont pas ces animations pour eux.

#### Multijoueur

- En capture du drapeau, les bots prennent, perdent et rapportent souvent les drapeaux mais en ramènent rarement un
  chez eux (un match entre bots peut finir à 0-0) : toute l'équipe adverse chasse le porteur, et sur CTF-LostCity
  chaque équipe commence à côté du drapeau de l'autre (carte de 2005), donc les deux drapeaux sont presque toujours
  sortis et chaque retour finit au milieu des départs adverses.
- Un match attend deux joueurs (les bots comptent), et chacun doit appuyer sur Tir pour être prêt ; un hôte seul
  sans bots attend.
- Après un match en équipe, une manche de plus est jouée ; en capture du drapeau, la capture suivante la termine
  aussitôt.
- Le tableau des scores de Last Man Standing n'a pas de colonne de vies : vies restantes = 5 moins les morts.
- La Porte des étoiles de DM-WorstCaseScenario est un décor : elle n'a pas de DHD et ne s'ouvre jamais.

### Limites du portage

- **Les effets des pixel shaders de la Xbox** sont approchés. Le bloom et le flou derrière le menu pause sont
  dessinés avec les moteurs de rendu Direct3D 9 (par défaut) et Direct3D 11, pas avec OpenGL (activés par
  défaut ; Options → Video → Bloom les désactive). La
  distorsion de chaleur des feux, explosions et champs de force n'est pas reproduite, et l'invisibilité
  des Reetou apparaît comme un reflet transparent.
- **La lentille de la lunette du fusil de précision** montre l'image avec Direct3D 9 et Direct3D 11 ; avec
  OpenGL, elle est noire.
- **La luminosité** ne s'applique qu'en plein écran avec Direct3D 9 (comportement d'OldUnreal) ; Direct3D 11
  l'applique aussi en fenêtre.
- **Direct3D 11 est expérimental** (Options → Video → Renderer) : avec l'anticrénelage, les ombres des
  personnages peuvent montrer des blocs carrés, et le texte est moins net qu'avec Direct3D 9.
- **Manette** : lue par DirectInput. LT et RT pressées ensemble s'annulent, il n'y a pas de vibrations, la manette
  doit être branchée avant le lancement du jeu, seule la première manette est lue, et la disposition suppose une
  manette de type Xbox.
- **Vision astrale** : le code `astral` n'affiche que son effet d'écran ; dessiner les êtres vivants à travers
  les murs demandait du code moteur qu'UT2004 n'a pas. Le menu de débogage des développeurs et certaines
  commandes de débogage ne sont pas disponibles ([CHEATS.md](CHEATS.md#non-disponible)).
- **Le jeu sur Internet** passe par les serveurs maîtres d'OldUnreal : la connexion Xbox Live, les amis et les
  listes de joueurs ne sont pas disponibles. Tout le monde doit avoir la même version de Redial et le même build
  OldUnreal.
- Une seule copie du jeu peut tourner à la fois sur un PC (comportement d'OldUnreal).
- Il arrive encore qu'un équipier ne monte pas dans le Hummvee. La commande console `assemblemembers` ramène
  l'équipe près de vous.
- La physique des véhicules perd un peu de vitesse à très haute fréquence d'images (quelques pour cent à
  144 images/s, environ 10 % à 300) : préférez une limite de 144 ou 240.
- Les fichiers de points de contrôle de la version Xbox (`.sgs`) ne peuvent pas être chargés.

### Pas encore vérifié par une personne

Des tests automatiques ont joué chaque partie de l'histoire jusqu'à sa fin, et les menus, l'interface et les
principales fonctions ont été vérifiés à l'écran. Personne n'a encore vérifié, en jouant à la V0.1 :

- une vraie manette (la disposition a été testée sans manette physique) ;
- les parties Internet par les serveurs maîtres (les parties en LAN ont été testées), plusieurs vrais joueurs sur
  un serveur, le Team DeathMatch du côté d'un joueur, un serveur dédié sur une vraie machine Linux ;
- la luminosité en plein écran avec Direct3D 9, le son 3D (HRTF) à l'oreille, la réverbération des grottes et des
  salles, le bloom sur écrans 21:9 et 4K ;
- les passages où les tests automatiques ont dû être aidés : M10A (détruire l'Al'Kesh avec le canon à bâton),
  M13C (l'ouverture), M18D (les portes de sécurité qui s'ouvrent quand on avance dedans), M19D (Carter qui va à
  la salle du générateur), M20D (la salle du trône et les Kull), M21C (la porte de la salle des capsules) ;
- le verrouillage et les cibles multiples du Stinger, les cristaux de contrôle mental (M21), l'énigme du champ de
  force (M19B), le marquage de cibles aux jumelles (M19D, M19E), l'objectif C4 (M17D), l'utilisation des anneaux
  de transport (M20), les canons à bâton et M60 en position fixe, les déguisements (M21).

En cas de problème, voir le [Dépannage](GUIDE.md#dépannage) et signalez-le sur le
[dépôt GitHub](https://github.com/Stargate-Redial/alliance-redial/issues) avec `<UT2004>\System\UT2004.log`.
