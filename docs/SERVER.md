# Hosting a dedicated server · Héberger un serveur dédié

[English](#english) · [Français](#français)

---

## English

A dedicated server runs the multiplayer modes of the 2005 game (DeathMatch, Team DeathMatch, Capture the Flag,
Last Man Standing) on its 10 maps, without a player at the keyboard. Each mode runs as its own **instance** (its own
process, ports, settings and logs). Bots can fill DeathMatch and Last Man Standing games.

### What you need

- The installer, run on a Windows PC with your own copy of the game (the archive.org release), exactly as for
  playing. The server is built from that install: nothing of the game is ever downloaded from us.
- UT2004 with the **latest OldUnreal 3374 patch**, on the server and on every player's PC.
- **The server and the players must run the same release** of Stargate SG-1 The Alliance: Redial. The server
  announces its release by itself (rule `RedialVer`, read from the install; nothing to set): the players' server
  lists dim a server of another release and mark it "v<release> required", and a player who joins anyway is
  refused with "This server runs Stargate Redial v... You have v...". Update the server and announce the update to
  the players at the same time. The server name shows the release, e.g. `... [v0.1]`.
- For a Linux server: an x86-64 (or arm64) Linux machine with glibc 2.34 or newer (Debian 12+, Ubuntu 22.04+),
  `python3`, and about 3 GB of disk space.

### Windows server

1. Run the installer with `--server`, for example from a command prompt in the package folder:
   `"Install Stargate Redial.cmd" --server`. After the normal install it creates `<UT2004>\SGAlliance\Server\`.
2. Edit `<UT2004>\SGAlliance\Server\server-settings.ini` (see [Settings](#settings)), then run the installer with
   `--server` again (it takes a few seconds when the game is already installed).
3. Start an instance with `run-dm.cmd` (DeathMatch), `run-ctf.cmd`, ... or every instance listed in `Run=` with
   `run-all.cmd`. Each window restarts its server after a crash. To stop one for good, close its window, or create
   `dm.stop` next to the scripts and end the server.
4. Allow the UDP ports in the Windows firewall (see [Ports](#ports)), and forward them on your router if the server
   is behind one (then also set `ServerBehindNAT=True`).
5. Optional watchdog: schedule `powershell -NoProfile -ExecutionPolicy Bypass -File health.ps1 -Restart` every 2-5
   minutes (Task Scheduler). It ends a server that stopped answering; its window starts it again.

### Linux server (native, systemd)

The Linux server runs OldUnreal's native Linux binary (`ucc-bin-amd64`) with the files built by the installer on
your Windows PC (the installer itself runs on Windows only). These steps are tested on a real Linux server
(Debian 13, with the systemd units of this bundle).

1. **UT2004 on Linux.** Install the game files (OldUnreal's full-game installer, SteamCMD with the Windows platform,
   or a copy of a Windows install), then extract the **Linux** release of the OldUnreal 3374 patch over them. Folder
   names are case-sensitive on Linux. Create a user for the servers (here `ut`) that owns the folder, e.g.
   `/home/ut/ut2004`.
2. **On the Windows PC**, build the server bundle:
   `"Install Stargate Redial.cmd" --server --server-bundle D:\sga-server.tar.gz`
   The bundle (about 2 GB) contains files built from **your** copy of the game: copy it to your own server only and
   never share it.
3. **Copy it to the server** (e.g. `scp D:\sga-server.tar.gz ut@server:`), then, as the user `ut`:
   ```
   tar -xzf sga-server.tar.gz --occurrence=1 install-linux-server.sh
   bash install-linux-server.sh /home/ut/ut2004 sga-server.tar.gz
   ```
   It checks the bundle, that your UT2004 has the same OldUnreal packages as the PC that built it, installs the mod
   into `/home/ut/ut2004/SGAlliance`, and creates `SGAlliance/Server/server-settings.ini` on the first run.
4. **Edit** `/home/ut/ut2004/SGAlliance/Server/server-settings.ini` (server name, `Run=`, bots, and
   `Advertise=True` on the public server), then: `python3 /home/ut/ut2004/SGAlliance/Server/sgr-server.py configure`
5. **Start the servers** (as root):
   `sudo python3 /home/ut/ut2004/SGAlliance/Server/sgr-server.py install-units`
   It installs one systemd service per instance (`sgredial-server@dm`, `sgredial-server@ctf`, ...), enables and
   starts the instances listed in `Run=`, and starts a health check every minute that restarts a server that
   stopped answering.
6. **Open the ports** (see [Ports](#ports)), e.g. `sudo ufw allow 7777:7778/udp`.
7. Check: `systemctl status sgredial-server@dm`, `python3 .../sgr-server.py status` (asks every instance on its
   query port), logs in `SGAlliance/Server/logs/` and `journalctl -u sgredial-server@dm`.

Without systemd (or to watch the console), `SGAlliance/Server/run-server.sh dm` runs an instance in a restart loop
(for example inside `screen`); `touch SGAlliance/Server/dm.stop` ends the loop after the next exit.

**Updating**: install the new release on the Windows PC with `--server --server-bundle ...`, copy the new bundle,
run `install-linux-server.sh` again (it replaces only what changed, removes files the new release dropped, and keeps
your settings and logs), then `sudo systemctl restart 'sgredial-server@*'`. Players update at the same time.

### Settings

`server-settings.ini` holds the admin password: never share or publish it. Every key is optional.

| `[Server]` key | Default | Meaning |
|---|---|---|
| `ServerName`, `ShortName`, `MOTD` | | What players see; `VersionInName=True` appends ` [v<release>]`, and with several instances ` - <mode>` is added |
| `AdminPassword` | generated | In game: console `adminlogin <password>`, then `admin <command>` |
| `GamePassword` | empty | Password players need to join |
| `Advertise` | `False` | `True` lists the server on OldUnreal's master servers. **Only on your public server** |
| `ServerBehindNAT` | `False` | `True` behind a router with port forwarding |
| `IP` | empty | Public address on a host with several addresses (`-multihome`) |
| `Instances` | `dm,tdm,ctf,lms` | Instances generated (one mode each) |
| `Run` | `dm` | Instances started by `run-all.cmd` / enabled by `install-units` |
| `BasePort` | `7777` | Instance number k (0 = the first of `Instances`) uses `BasePort + 20*k` |
| `MaxPlayers`, `MaxSpectators` | `16`, `2` | |
| `MinPlayers`, `BotSkill` | `0`, empty | Bots (DM, TDM, CTF, LMS): fill each game up to `MinPlayers` players in total, bots leave as players join; skill 0-7, empty = the game's default (6) |
| `WebAdmin`, `WebAdminPort` | `False`, `8075` | UT2004's web admin, TCP port `WebAdminPort + k` *(to be confirmed with this game)* |
| `GamespyQuery` | `False` | Old GameSpy query port (game port + 10), for trackers that need it; needs `Advertise=True` |
| `LogsKept` | `10` | Server logs kept per instance (one per run) |
| `Discord`, `DiscordKills` | `False`, `humans` | Discord activity feed of each instance (see below); kills posted only when a player is the killer or the victim (`humans`), always (`all`) or never (`off`) |
| `User` | the current user | Linux: the user that runs the services |

A section per instance (`[dm]`, `[tdm]`, `[ctf]`, `[lms]`) overrides these keys and can set `Maps=` (the map
rotation, comma-separated), `Port=`, `GoalScore=`, `TimeLimit=` (minutes), `MaxLives=`, `MinPlayers=`, `BotSkill=`,
`Mutators=`, `ExtraURL=` (extra `?Key=Value` options), `Discord=`, `DiscordPort=`. Any `[Package.Class]` section is copied into every instance's
configuration (`[dm:Package.Class]` for one instance): `Key=` sets a key, `+Key=` adds a line, `-Key=` removes one.

Default rotations: DeathMatch, Team DeathMatch and Last Man Standing play the 7 DM maps (LostCity, Tomb, Hatak,
Langara, Subterranean, KelownanTrain, WorstCaseScenario); Capture the Flag plays CTF-LostCity, CTF-Abydos and
SGCTF-AbydosVsSGC, as in the game's host menu.

### Ports

Each instance uses a UDP **game port** and a UDP **query port** (server lists, `status`, the health check). With the
default `BasePort=7777`:

| Instance | Mode | Game (UDP) | Query (UDP) |
|---|---|---|---|
| `dm` | DeathMatch | 7777 | 7778 |
| `tdm` | Team DeathMatch | 7797 | 7798 |
| `ctf` | Capture the Flag | 7817 | 7818 |
| `lms` | Last Man Standing | 7837 | 7838 |

Open only those of the instances you run. With `GamespyQuery=True`, also game port + 10 (UDP); with `WebAdmin=True`,
the web admin port (TCP). The UT2004 LAN port 10777 needs no opening on an Internet server.

### Bots

`MinPlayers=N` fills each game with bots up to N players in total (players + bots, 0-16; bots come on top of
`MaxPlayers`, which counts players only). A bot leaves when a player joins (at its next death) and comes back when a
player leaves; 0 = no bots. Bots play in **DeathMatch**, **Last Man Standing**, **Team DeathMatch** and **Capture
the Flag** (SG-1 against the Jaffa in the two team modes), with the 11 multiplayer characters; in Last Man
Standing they have the same lives as everyone.

`BotSkill` goes from 0 (Very Easy) to 7 (Elite); left empty, the game's default **6** (Expert) applies. Both keys are passed
to the game as they are (`?MinPlayers=`, `?BotSkill=`). The bots run on the server only: players download nothing.
An empty server waits; the match starts when the first player joins and presses Fire.

For testing or stat collection, bots can also play on their own: `ExtraURL=?SGBBotsOnly=1` in an instance's section
(or `bStartWithBotsOnly=True` in a `[SGBots.SGBotSupport]` section), with `MinPlayers` above 0. With no player on
the server, each match then starts with the bots 10 s after the map loads, and the map rotation goes on after every
match. A player who joins enters the match in progress (a bot leaves at its next death); with a player on the
server at the map start, the usual start applies. These bots do not pause on the empty server (add
`?SGBEmptyPause=1` to pause them anyway). Off by default.
`?SGBBalanceLog=1` (off by default, for stats only) writes balance statistics to the server log (`SGBAL` lines).

### Weapon packs

Each player chooses a weapon pack with the character (Tau'ri: Assault = P90 + frag grenades, Close Quarters =
Shotgun + C4, Marksman = Sniper rifle + shock grenades; Goa'uld: Warrior = Staff weapon + frag grenades, Zat = Zat
gun + shock grenades, Lord = Ribbon device + frag grenades) and starts with it and the pistol. Bots take a random
pack of their side. To keep the 2005 start (the pistol only), add `ExtraURL=?SGPacks=0` to an instance's section, or
`bPacks=False` in a `[SGBase.SGPacks]` section (`[dm:SGBase.SGPacks]` for one instance). On by default.

### Discord activity feed (optional)

The server can post its activity in a channel of your Discord server: players joining (with their character) and
leaving, kills where a player is the killer or the victim (grouped in one message every 45 s), match start and results (winner,
scores), map changes, and a summary when the last player leaves. Bring your own bot: in the Discord Developer Portal
create an application, add a bot, copy its token, invite it to your server with the *View Channel* and *Send
Messages* permissions on the channel, and copy the channel's id (Discord settings: Developer Mode, then right-click the
channel → Copy Channel ID).

1. In `server-settings.ini`, `Discord=True` for the instances to follow (in `[Server]` or an instance section), then
   `configure`. Each such instance gets the server-side package `SGDiscordFeed` (a `ServerActors` line; it is never
   sent to players) and sends its events to the local UDP port game port + 6 (`DiscordPort=` to change it).
2. Put the token and the channel id in `Server/discord-<instance>.env`, which `configure` creates (mode 600 on Linux;
   it holds a secret: never share it): `SGR_DISCORD_TOKEN=...`, `SGR_DISCORD_CHANNEL=...`, optionally
   `SGR_DISCORD_BOT_ID=...` (then a token of another bot is refused).
3. Test: `python3 sgr-server.py discord dm --test` posts one test message.
4. Linux: `sudo python3 sgr-server.py install-units` starts the relay `sgredial-discord@<instance>` (logs:
   `journalctl -u sgredial-discord@dm`). Windows: run `python sgr-server.py discord dm` (Python 3.8+) next to the
   server.

The relay posts at most one message every 1.2 s and 120 per hour, never shows addresses, and shows player names
as code (no mentions). The bot's status shows the server's state once a minute, e.g. `DM-LostCity [1/16] +5 bots`
(map, players/places, bots), or "server not responding".

The relay also keeps every event (bot-against-bot kills included) in `Server/logs/<instance>-events.jsonl`: one JSON
line each, in-game names only (no address, no CD key), a new file every day or past 10 MB, 14 days kept.
`python3 sgr-server.py stats all --since 24h` (or an instance) summarises them: matches, kills and K/D per character
and weapon (bots and players apart), team wins, players seen, server restarts and crash markers, and what looks odd
(a weapon that dominates, a character that never wins).

### Server command line (advanced)

The scripts start `UCC server "<map>?game=<class>?<options>" -ini=<instance ini> -userini=<...> -nohomedir
-log=<...>` from UT2004's `System` folder. Game classes: `StargateGame.StargateDeathMatch`,
`StargateGame.TeamDeathMatch`, `StargateGame.SGxCTFGame`, `StargateGame.LastManStandingGame`. Options the game reads:
`MaxPlayers`, `MaxSpectators`, `MinPlayers`, `BotSkill`, `GoalScore`, `TimeLimit`, `MaxLives`, `Mutator`. Each
instance reads its own main ini, so `-mod=` is not used: with `-mod=` UT2004 ignores `-ini=`.

### Troubleshooting

- "This server runs Stargate Redial v... You have v..." (or UT2004's "Connection failed: Downloading package
  '...' failed: Server refused to send '...'") when joining: the player and the server run different releases (or
  different OldUnreal builds). The server never sends the game's packages: update both to the same release.
- `install-linux-server.sh` says the OldUnreal packages differ: install the latest OldUnreal 3374 patch on both PCs.
- A player cannot find the server in the Internet list: `Advertise=True`, the game and query ports open, and wait
  a few minutes. `sgr-server.py status` on the server must show the instance "up".

---

## Français

Un serveur dédié fait tourner les modes multijoueur du jeu de 2005 (DeathMatch, Team DeathMatch, Capture du drapeau,
Last Man Standing) sur ses 10 cartes, sans joueur devant l'écran. Chaque mode tourne dans sa propre **instance**
(son processus, ses ports, ses réglages et ses journaux). Des bots peuvent compléter les parties en DeathMatch et en
Last Man Standing.

### Ce qu'il faut

- L'installeur, lancé sur un PC Windows avec votre propre copie du jeu (la version archive.org), comme pour jouer. Le
  serveur est construit à partir de cette installation : rien du jeu n'est jamais téléchargé chez nous.
- UT2004 avec le **dernier patch OldUnreal 3374**, sur le serveur et chez chaque joueur.
- **Le serveur et les joueurs doivent avoir la même version** de Stargate SG-1 The Alliance: Redial. Le serveur
  annonce sa version tout seul (règle `RedialVer`, lue dans l'installation ; rien à régler) : les listes de
  serveurs des joueurs grisent un serveur d'une autre version et le marquent « v<version> required », et un joueur
  qui s'y connecte quand même est refusé avec « This server runs Stargate Redial v... You have v... ». Mettez le
  serveur à jour en même temps que vous annoncez la mise à jour aux joueurs. Le nom du serveur affiche la version,
  par exemple `... [v0.1]`.
- Pour un serveur Linux : une machine Linux x86-64 (ou arm64) avec glibc 2.34 ou plus récent (Debian 12+, Ubuntu
  22.04+), `python3`, et environ 3 Go d'espace disque.

### Serveur Windows

1. Lancez l'installeur avec `--server`, par exemple depuis une invite de commandes dans le dossier du paquet :
   `"Install Stargate Redial.cmd" --server`. Après l'installation normale, il crée `<UT2004>\SGAlliance\Server\`.
2. Modifiez `<UT2004>\SGAlliance\Server\server-settings.ini` (voir [Réglages](#réglages)), puis relancez
   l'installeur avec `--server` (quelques secondes quand le jeu est déjà installé).
3. Démarrez une instance avec `run-dm.cmd` (DeathMatch), `run-ctf.cmd`… ou toutes celles de `Run=` avec
   `run-all.cmd`. Chaque fenêtre relance son serveur après un plantage. Pour l'arrêter pour de bon, fermez sa
   fenêtre, ou créez `dm.stop` à côté des scripts puis arrêtez le serveur.
4. Autorisez les ports UDP dans le pare-feu Windows (voir [Ports](#ports-1)), et redirigez-les sur votre box si le
   serveur est derrière (mettez alors aussi `ServerBehindNAT=True`).
5. Surveillance facultative : planifiez
   `powershell -NoProfile -ExecutionPolicy Bypass -File health.ps1 -Restart` toutes les 2 à 5 minutes
   (Planificateur de tâches). Il arrête un serveur qui ne répond plus ; sa fenêtre le relance.

### Serveur Linux (natif, systemd)

Le serveur Linux utilise le binaire Linux natif d'OldUnreal (`ucc-bin-amd64`) avec les fichiers construits par
l'installeur sur votre PC Windows (l'installeur ne tourne que sous Windows). Ces étapes sont testées sur un vrai
serveur Linux (Debian 13, avec les unités systemd de ce paquet).

1. **UT2004 sous Linux.** Installez les fichiers du jeu (l'installeur complet d'OldUnreal, SteamCMD en plateforme
   Windows, ou une copie d'une installation Windows), puis extrayez par-dessus la version **Linux** du patch
   OldUnreal 3374. Sous Linux, les noms de dossiers respectent la casse. Créez un utilisateur pour les serveurs (ici
   `ut`), propriétaire du dossier, par exemple `/home/ut/ut2004`.
2. **Sur le PC Windows**, construisez le paquet serveur :
   `"Install Stargate Redial.cmd" --server --server-bundle D:\sga-server.tar.gz`
   Ce paquet (environ 2 Go) contient des fichiers construits à partir de **votre** copie du jeu : copiez-le
   uniquement sur votre propre serveur et ne le partagez jamais.
3. **Copiez-le sur le serveur** (par exemple `scp D:\sga-server.tar.gz ut@serveur:`), puis, en tant que `ut` :
   ```
   tar -xzf sga-server.tar.gz --occurrence=1 install-linux-server.sh
   bash install-linux-server.sh /home/ut/ut2004 sga-server.tar.gz
   ```
   Il vérifie le paquet, vérifie que votre UT2004 a les mêmes paquets OldUnreal que le PC qui l'a construit, installe
   le mod dans `/home/ut/ut2004/SGAlliance` et crée `SGAlliance/Server/server-settings.ini` au premier lancement.
4. **Modifiez** `/home/ut/ut2004/SGAlliance/Server/server-settings.ini` (nom du serveur, `Run=`, bots, et
   `Advertise=True` sur le serveur public), puis :
   `python3 /home/ut/ut2004/SGAlliance/Server/sgr-server.py configure`
5. **Démarrez les serveurs** (en root) :
   `sudo python3 /home/ut/ut2004/SGAlliance/Server/sgr-server.py install-units`
   Il installe un service systemd par instance (`sgredial-server@dm`, `sgredial-server@ctf`…), active et démarre
   les instances de `Run=`, et lance chaque minute une vérification qui relance un serveur qui ne répond plus.
6. **Ouvrez les ports** (voir [Ports](#ports-1)), par exemple `sudo ufw allow 7777:7778/udp`.
7. Vérifiez : `systemctl status sgredial-server@dm`, `python3 .../sgr-server.py status` (interroge chaque instance
   sur son port de requête), journaux dans `SGAlliance/Server/logs/` et `journalctl -u sgredial-server@dm`.

Sans systemd (ou pour voir la console), `SGAlliance/Server/run-server.sh dm` fait tourner une instance en boucle
(par exemple dans `screen`) ; `touch SGAlliance/Server/dm.stop` arrête la boucle à la sortie suivante.

**Mise à jour** : installez la nouvelle version sur le PC Windows avec `--server --server-bundle …`, copiez le
nouveau paquet, relancez `install-linux-server.sh` (il ne remplace que ce qui a changé, supprime les fichiers que la
nouvelle version n'a plus, et garde vos réglages et vos journaux), puis `sudo systemctl restart 'sgredial-server@*'`.
Les joueurs se mettent à jour en même temps.

### Réglages

`server-settings.ini` contient le mot de passe admin : ne le partagez et ne le publiez jamais. Toutes les clés sont
facultatives.

| Clé `[Server]` | Défaut | Rôle |
|---|---|---|
| `ServerName`, `ShortName`, `MOTD` | | Ce que voient les joueurs ; `VersionInName=True` ajoute ` [v<version>]`, et avec plusieurs instances ` - <mode>` |
| `AdminPassword` | généré | En jeu : console `adminlogin <mot de passe>`, puis `admin <commande>` |
| `GamePassword` | vide | Mot de passe pour rejoindre |
| `Advertise` | `False` | `True` publie le serveur sur les master servers d'OldUnreal. **Uniquement sur votre serveur public** |
| `ServerBehindNAT` | `False` | `True` derrière une box avec redirection de ports |
| `IP` | vide | Adresse publique sur une machine qui en a plusieurs (`-multihome`) |
| `Instances` | `dm,tdm,ctf,lms` | Instances générées (un mode chacune) |
| `Run` | `dm` | Instances lancées par `run-all.cmd` / activées par `install-units` |
| `BasePort` | `7777` | L'instance numéro k (0 = la première de `Instances`) utilise `BasePort + 20*k` |
| `MaxPlayers`, `MaxSpectators` | `16`, `2` | |
| `MinPlayers`, `BotSkill` | `0`, vide | Bots (DM, TDM, CTF, LMS) : complètent chaque partie jusqu'à `MinPlayers` joueurs au total, ils laissent leur place aux joueurs ; niveau 0 à 7, vide = niveau par défaut du jeu (6) |
| `WebAdmin`, `WebAdminPort` | `False`, `8075` | Web admin d'UT2004, port TCP `WebAdminPort + k` *(à confirmer avec ce jeu)* |
| `GamespyQuery` | `False` | Ancien port de requête GameSpy (port de jeu + 10), pour les outils qui en ont besoin ; demande `Advertise=True` |
| `LogsKept` | `10` | Journaux gardés par instance (un par lancement) |
| `Discord`, `DiscordKills` | `False`, `humans` | Fil d'activité Discord de chaque instance (voir plus bas) ; frags postés seulement quand un joueur tue ou meurt (`humans`), toujours (`all`) ou jamais (`off`) |
| `User` | l'utilisateur courant | Linux : l'utilisateur qui fait tourner les services |

Une section par instance (`[dm]`, `[tdm]`, `[ctf]`, `[lms]`) remplace ces clés et peut définir `Maps=` (la
rotation des cartes, séparées par des virgules), `Port=`, `GoalScore=`, `TimeLimit=` (minutes), `MaxLives=`,
`MinPlayers=`, `BotSkill=`, `Mutators=`, `ExtraURL=` (options `?Clé=Valeur` en plus), `Discord=`, `DiscordPort=`. Toute section
`[Package.Classe]` est recopiée dans la configuration de chaque instance (`[dm:Package.Classe]` pour une seule) :
`Clé=` fixe une clé, `+Clé=` ajoute une ligne, `-Clé=` en retire une.

Rotations par défaut : DeathMatch, Team DeathMatch et Last Man Standing jouent les 7 cartes DM (LostCity, Tomb,
Hatak, Langara, Subterranean, KelownanTrain, WorstCaseScenario) ; la Capture du drapeau joue CTF-LostCity,
CTF-Abydos et SGCTF-AbydosVsSGC, comme dans le menu d'hébergement du jeu.

### Ports

Chaque instance utilise un **port de jeu** UDP et un **port de requête** UDP (listes de serveurs, `status`, la
surveillance). Avec `BasePort=7777` :

| Instance | Mode | Jeu (UDP) | Requête (UDP) |
|---|---|---|---|
| `dm` | DeathMatch | 7777 | 7778 |
| `tdm` | Team DeathMatch | 7797 | 7798 |
| `ctf` | Capture du drapeau | 7817 | 7818 |
| `lms` | Last Man Standing | 7837 | 7838 |

N'ouvrez que ceux des instances que vous faites tourner. Avec `GamespyQuery=True`, ajoutez le port de jeu + 10
(UDP) ; avec `WebAdmin=True`, le port du web admin (TCP). Le port LAN 10777 d'UT2004 n'a pas besoin d'être ouvert
sur un serveur Internet.

### Bots

`MinPlayers=N` complète chaque partie avec des bots jusqu'à N joueurs au total (joueurs + bots, 0 à 16 ; les bots
s'ajoutent à `MaxPlayers`, qui ne compte que les joueurs). Un bot part quand un joueur arrive (à sa prochaine mort) et
revient quand un joueur s'en va ; 0 = pas de bots. Les bots jouent en **DeathMatch**, **Last Man Standing**,
**Team DeathMatch** et **Capture du drapeau** (SG-1 contre les Jaffa dans les deux modes en équipe), avec les 11 personnages multijoueur ; en Last Man Standing ils ont
autant de vies que tout le monde.

`BotSkill` va de 0 (Very Easy) à 7 (Elite) ; vide, c'est le niveau par défaut du jeu, **6** (Expert). Les deux clés sont
transmises telles quelles au jeu (`?MinPlayers=`, `?BotSkill=`). Les bots tournent uniquement sur le serveur : les
joueurs ne téléchargent rien. Un serveur vide attend ; la partie démarre quand le premier joueur arrive et appuie sur
Tir.

Pour des tests ou pour collecter des statistiques, les bots peuvent aussi jouer seuls : `ExtraURL=?SGBBotsOnly=1` dans
la section d'une instance (ou `bStartWithBotsOnly=True` dans une section `[SGBots.SGBotSupport]`), avec `MinPlayers`
au-dessus de 0. Sans joueur sur le serveur, chaque partie démarre alors avec les bots 10 s après le chargement de la
carte, et la rotation des cartes continue après chaque partie. Un joueur qui arrive rejoint la partie en cours (un
bot part à sa prochaine mort) ; avec un joueur présent au chargement de la carte, le démarrage habituel s'applique.
Ces bots ne se mettent pas en pause sur le serveur vide (ajoutez `?SGBEmptyPause=1` pour les y mettre quand même).
Désactivé par défaut.
`?SGBBalanceLog=1` (désactivé par défaut, pour les statistiques) écrit des statistiques d'équilibrage dans le
journal du serveur (lignes `SGBAL`).

### Packs d'armes

Chaque joueur choisit un pack d'armes avec son personnage (Tau'ri : Assault = P90 + grenades à fragmentation, Close
Quarters = fusil à pompe + C4, Marksman = fusil de précision + grenades paralysantes ; Goa'uld : Warrior = lance
Goa'uld + grenades à fragmentation, Zat = zat + grenades paralysantes, Lord = arme de poing Goa'uld (ribbon device) +
grenades à fragmentation) et commence avec ce pack et le pistolet. Les bots prennent un pack de leur camp au hasard.
Pour garder le départ de 2005 (le pistolet seul), ajoutez `ExtraURL=?SGPacks=0` dans la section d'une instance, ou
`bPacks=False` dans une section `[SGBase.SGPacks]` (`[dm:SGBase.SGPacks]` pour une seule instance). Activé par défaut.

### Fil d'activité Discord (facultatif)

Le serveur peut publier son activité dans un salon de votre serveur Discord : arrivées des joueurs (avec leur
personnage) et départs, frags où un joueur tue ou meurt (regroupés en un message toutes les 45 s), début et
résultat des parties (vainqueur, scores), changements de carte, et un bilan quand le dernier joueur s'en va. Avec
votre propre bot : dans le Discord Developer Portal, créez une application, ajoutez-lui un bot, copiez son jeton,
invitez-le sur votre serveur avec les permissions *Voir le salon* et *Envoyer des messages* dans ce salon, et copiez
l'identifiant du salon (paramètres Discord : Mode développeur, puis clic droit sur le salon → Copier l'identifiant).

1. Dans `server-settings.ini`, `Discord=True` pour les instances à suivre (dans `[Server]` ou une section
   d'instance), puis `configure`. Chacune reçoit le paquet côté serveur `SGDiscordFeed` (une ligne `ServerActors` ;
   il n'est jamais envoyé aux joueurs) et envoie ses événements au port UDP local port de jeu + 6 (`DiscordPort=`
   pour le changer).
2. Mettez le jeton et l'identifiant du salon dans `Server/discord-<instance>.env`, que `configure` crée (mode 600
   sous Linux ; il contient un secret : ne le partagez jamais) : `SGR_DISCORD_TOKEN=...`, `SGR_DISCORD_CHANNEL=...`,
   et si vous voulez `SGR_DISCORD_BOT_ID=...` (le jeton d'un autre bot est alors refusé).
3. Test : `python3 sgr-server.py discord dm --test` publie un message de test.
4. Linux : `sudo python3 sgr-server.py install-units` démarre le relais `sgredial-discord@<instance>` (journal :
   `journalctl -u sgredial-discord@dm`). Windows : lancez `python sgr-server.py discord dm` (Python 3.8+) à côté
   du serveur.

Le relais publie au plus un message toutes les 1,2 s et 120 par heure, n'affiche jamais d'adresse, et montre les
noms des joueurs comme du code (pas de mentions). Le statut du bot montre l'état du serveur, mis à jour chaque
minute, par exemple `DM-LostCity [1/16] +5 bots` (carte, joueurs/places, bots), ou « server not responding ».

Le relais garde aussi chaque événement (frags entre bots compris) dans `Server/logs/<instance>-events.jsonl` : une
ligne JSON chacun, avec seulement les noms en jeu (ni adresse, ni clé CD), un nouveau fichier chaque jour ou au-delà
de 10 Mo, 14 jours gardés. `python3 sgr-server.py stats all --since 24h` (ou une instance) les résume : parties,
frags et K/D par personnage et par arme (bots et joueurs à part), victoires d'équipe, joueurs vus, redémarrages du
serveur et traces de plantage, et ce qui semble anormal (une arme qui domine, un personnage qui ne gagne jamais).

### Ligne de commande du serveur (avancé)

Les scripts lancent `UCC server "<carte>?game=<classe>?<options>" -ini=<ini de l'instance> -userini=<…> -nohomedir
-log=<…>` depuis le dossier `System` d'UT2004. Classes de jeu : `StargateGame.StargateDeathMatch`,
`StargateGame.TeamDeathMatch`, `StargateGame.SGxCTFGame`, `StargateGame.LastManStandingGame`. Options lues par le
jeu : `MaxPlayers`, `MaxSpectators`, `MinPlayers`, `BotSkill`, `GoalScore`, `TimeLimit`, `MaxLives`, `Mutator`.
Chaque instance lit son propre ini principal, donc `-mod=` n'est pas utilisé : avec `-mod=`, UT2004 ignore `-ini=`.

### En cas de problème

- « This server runs Stargate Redial v... You have v... » (ou « Connection failed: Downloading package '...'
  failed: Server refused to send '...' » d'UT2004) à la connexion : le joueur et le serveur n'ont pas la même
  version (ou pas le même patch OldUnreal). Le serveur n'envoie jamais les paquets du jeu : mettez les deux à la
  même version.
- `install-linux-server.sh` dit que les paquets OldUnreal diffèrent : installez le dernier patch OldUnreal 3374
  sur les deux machines.
- Un joueur ne voit pas le serveur dans la liste Internet : `Advertise=True`, ports de jeu et de requête ouverts, et
  attendez quelques minutes. `sgr-server.py status` sur le serveur doit montrer l'instance « up ».
