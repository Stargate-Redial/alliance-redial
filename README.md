<!-- Public repository https://github.com/Stargate-Redial/alliance-redial: this README, CHANGELOG.md, NOTICE.md, docs/GUIDE.md, docs/KNOWN_ISSUES.md, docs/CHEATS.md and docs/SERVER.md only; the installer is a Release asset. Also shipped inside the release zip. -->
# Stargate SG-1 The Alliance: Redial

:gb: **English** · :fr: [Français](#français)

The unreleased *Stargate SG-1: The Alliance* (an Xbox prototype from December 2005), playable on your PC as a
mod for **Unreal Tournament 2004** with the OldUnreal patch. A [Stargate Redial](https://github.com/Stargate-Redial)
fan project. Current release: **V0.1**. Join the community on [Discord](https://discord.gg/SgHPP4mZyB).

> Apart from its title picture, no game data is included: the installer rebuilds the game on your PC from your
> own copy of the 2019 release. Fan project, not affiliated with or endorsed by MGM, Perception, JoWooD,
> Microsoft or Epic Games. See [NOTICE.md](NOTICE.md).

## 🛸 About this prototype

This is an **unfinished game**: a December 2005 Xbox prototype that was never completed or released. We restore
and fix what exists and add nothing new.

- **The real SG-1:** voiced by the show's cast, Richard Dean Anderson (O'Neill), Amanda Tapping (Carter),
  Michael Shanks (Daniel Jackson) and Christopher Judge (Teal'c), with Carmen Argenziano as Jacob Carter, in
  sessions directed by the series' Peter DeLuise. The SGC is there too: even Walter is a playable character in
  multiplayer.
- **Stargate action:** give orders to your squad, drive vehicles, and dial the Stargates on the multiplayer maps.
- **Playable:** the solo campaign (the tutorial and missions 2, 4, 7, 10 and 12 to 21) and
  multiplayer (DeathMatch, Team DeathMatch, Capture the Flag and Last Man Standing, on ten maps).
- **Expect flaws:** some surfaces are plain white or grey where the 2005 data has no texture; a few sounds and HUD
  icons are missing; mouths move only in some dialogues; some features were never built
  (co-op, split-screen, the *Extras* page) and are hidden; Capture the Flag with bots is rough.
- **The story may not make full sense:** missions 1, 3, 5, 6, 8, 9 and 11 are not in the build (the first one,
  *Replicator Attack*, was cut), so the story jumps between missions, and some recorded scenes are never played.

See [KNOWN_ISSUES.md](docs/KNOWN_ISSUES.md) and the [CHANGELOG](CHANGELOG.md).

## ✨ What Redial brings

A few highlights (the [CHANGELOG](CHANGELOG.md) has the full list):

**🧩 Restored from the 2005 data**
- Last Man Standing is back in the multiplayer mode list.
- About 150 recorded voice lines that the 2005 game never played are back in the squad's chatter.
- The SG-1 crew's lip sync plays in every mission, where the 2005 build had it in only a few.
- Cheat codes work from the console in single player ([docs/CHEATS.md](docs/CHEATS.md)).
- Menu and HUD features that were left unwired are back, such as Options from the pause menu and the binocular read-out.

**🖥️ Made for PC**
- Mouse and keyboard, or an Xbox controller with the original 2005 layout.
- Any resolution up to 4K, widescreen field of view, and quick save (F5) and quick load (F9).
- Menus that work with a mouse click, and graphics at their highest by default.

**🌐 Online**
- Internet and LAN games, and dedicated servers for Windows and Linux.
- Bots in every multiplayer mode.
- A weapon pack per side, and a *Change Character* option in game.
- A quick voice menu (V) with each character's own 2005 voice, and text chat that servers can relay to Discord.

**⚙️ Easy to live with**
- One-click automatic updates, with your settings and saves kept.
- Your solo progress shown in the Single Player menu.

---

## 🚀 Quick start

1. **UT2004 with the OldUnreal patch.**
   - **No UT2004 yet?** Install it with OldUnreal's
     [full-game installer](https://www.oldunreal.com/downloads/ut2004/full-game-installers/): it also installs
     the latest OldUnreal patch, nothing else to do.
   - **Already have it** (Steam, GOG, CD)? Add the latest
     [OldUnreal patch](https://github.com/OldUnreal/UT2004Patches/releases) (3374, 2026-10-20 or later).
   - Our installer checks the patch version and tells you if it is too old.
2. **The 2005 game files.** Download `Stargate_SG-1_-_The_Alliance-2005-12-15.7z` (about 1 GB) from
   [archive.org](https://archive.org/details/StargateSG1TheAlliance20051215) and leave it in your Downloads folder.
3. **The installer.** Download `Stargate-Redial-Alliance-v<version>-win64.zip` from the
   [Releases page](https://github.com/Stargate-Redial/alliance-redial/releases), extract it and run
   **Stargate Redial Setup.exe** (if SmartScreen appears: *More info*, then *Run anyway*).
4. **Install, then play.** The window finds the `.7z` and UT2004 by itself: click *Install* (a few minutes), then
   *Play*. Next time, start the game from its desktop shortcut: it checks for updates automatically and installs them in one
   click.

## 🔄 Automatic updates

- Starting the game from its shortcut checks this GitHub page for a new version: no account, no personal data.
- A window shows what is new and updates in one click; the download is signature-checked.
- Your settings and saves are kept.
- You can turn this off in the installer. Details: [Updating in detail](docs/GUIDE.md#updating-in-detail).

## 💡 Good to know

- The installer is not signed: Windows SmartScreen may warn you. Click *More info*, then *Run anyway*.
- Windows 11 *Smart App Control*, when on, blocks unsigned programs: the installer cannot run there.
- Plan about 9 GB of free space and an Internet connection during the install.

More: [player guide](docs/GUIDE.md) · [installer details](docs/GUIDE.md#installer-details) (options, files written,
updating, uninstalling) · [known issues](docs/KNOWN_ISSUES.md) · [cheats](docs/CHEATS.md) ·
[dedicated servers](docs/SERVER.md) · [CHANGELOG](CHANGELOG.md)

---

## 🐞 Problem?

Open an [issue](https://github.com/Stargate-Redial/alliance-redial/issues) or ask on
[Discord](https://discord.gg/SgHPP4mZyB). Please give the version, what you did and what happened, and attach
`<UT2004>\System\UT2004.log` (see [Troubleshooting](docs/GUIDE.md#reporting-a-problem)).

---

## 🗺️ Roadmap (ideas, no promises)

- **French translation**: subtitles, menus, HUD and objectives in French (the voices stay in English), with a
  language choice in the options and in the installer.
- **Replicators**: the 2005 build still holds unused Replicator code and models (the spider-like Replicator, the
  Queen, a playable Replicator with its own HUD) from a cut mission. We will see whether they can be brought
  back to life.

## 🙏 Thanks

- The **OldUnreal** team, for the UT2004 community patches and full-game installer: without them, this project
  would not exist. <https://www.oldunreal.com>
- **CVLT OF OSIRIS**, who dumped this Xbox build and released it in 2019, and **Hidden Palace**, who documented
  it.
- **Perception**, who made *The Alliance* on **Epic Games'** Unreal Engine 2.5.

---

## ⚖️ Legal

Stargate Redial is a free, non-commercial fan project that aims to preserve an unreleased prototype. It has no
link with MGM, Perception, JoWooD, Microsoft or Epic Games, and none of them has approved it. Every name,
character and logo belongs to its owner.

- **What we publish:** only our own work (installer, tools, documents) and one title picture credited in
  [NOTICE.md](NOTICE.md). No file from the game, and nothing built from one.
- **What stays with you:** the installer turns *your* copy of the 2019 release into a mod on *your* PC. The files
  it generates come from the game: do not upload, share, bundle or sell them, and do not let a server hand them
  out (see [docs/SERVER.md](docs/SERVER.md)).
- **Rights holders:** to have something changed or removed, open an issue or contact us on Discord. We will act
  promptly.
- **Not legal advice:** this text claims no "fair use" in any country. If you redistribute something yourself,
  you are responsible for it.

## 📜 Licence

Free to use, non-commercial. Third-party licences: [NOTICE.md](NOTICE.md).

---

## Français

:gb: [English](#stargate-sg-1-the-alliance-redial) · :fr: **Français**

Le prototype inédit *Stargate SG-1: The Alliance* (version Xbox de décembre 2005), jouable sur PC comme mod
d'**Unreal Tournament 2004** avec le patch OldUnreal. Un projet de fans
[Stargate Redial](https://github.com/Stargate-Redial). Version actuelle : **V0.1**. Retrouvez la communauté sur
[Discord](https://discord.gg/SgHPP4mZyB).

> Hormis son image de titre, aucune donnée du jeu n'est incluse : l'installeur reconstruit le jeu sur votre PC à
> partir de votre propre copie de la publication de 2019. Projet de fans, sans lien avec MGM, Perception, JoWooD,
> Microsoft ou Epic Games, ni autorisé par eux. Voir [NOTICE.md](NOTICE.md).

### 🛸 À propos de ce prototype

C'est un **jeu inachevé** : un prototype Xbox de décembre 2005, jamais terminé ni publié. Nous restaurons et
corrigeons l'existant, sans rien ajouter de nouveau.

- **Le vrai SG-1 :** les voix des acteurs de la série, Richard Dean Anderson (O'Neill), Amanda Tapping (Carter),
  Michael Shanks (Daniel Jackson) et Christopher Judge (Teal'c), avec Carmen Argenziano dans le rôle de Jacob
  Carter, sous la direction de Peter DeLuise, réalisateur de la série. Le SGC est là aussi : même Walter est un
  personnage jouable en multijoueur.
- **L'action Stargate :** donnez des ordres à votre escouade, pilotez des véhicules et composez l'adresse des
  portes des étoiles sur les cartes multijoueur.
- **Jouable :** la campagne solo (le tutoriel et les missions 2, 4, 7, 10 et 12 à 21) et le
  multijoueur (DeathMatch, Team DeathMatch, Capture du drapeau et Last Man Standing, sur dix cartes).
- **Attendez-vous à des défauts :** certaines surfaces sont blanches ou grises faute de texture dans les données de
  2005 ; quelques sons et icônes d'interface manquent ; les bouches ne bougent que dans certains dialogues ;
  certaines fonctions n'ont jamais été faites (coop, écran partagé, la page *Extras*) et sont masquées ; la Capture du drapeau
  avec bots est rudimentaire.
- **L'histoire peut manquer de cohérence :** les missions 1, 3, 5, 6, 8, 9 et 11 ne sont pas dans la version (la
  première, *Replicator Attack*, a été coupée) : l'histoire saute d'une mission à l'autre, et certaines scènes
  enregistrées ne sont jamais jouées.

Voir [KNOWN_ISSUES.md](docs/KNOWN_ISSUES.md#français) et le [CHANGELOG](CHANGELOG.md) (en anglais).

### ✨ Ce qu'apporte Redial

Quelques points forts (le [CHANGELOG](CHANGELOG.md), en anglais, donne la liste complète) :

**🧩 Restauré à partir des données de 2005**
- Last Man Standing est de retour dans la liste des modes multijoueur.
- Environ 150 répliques enregistrées que le jeu de 2005 ne jouait jamais reviennent dans les échanges de l'équipe.
- La synchro labiale de l'équipe SG-1 joue dans toutes les missions, alors que la version de 2005 ne l'avait que
  dans quelques-unes.
- Les codes de triche fonctionnent depuis la console en solo ([docs/CHEATS.md](docs/CHEATS.md#français)).
- Des fonctions de menu et d'interface laissées de côté sont de retour, comme les Options depuis le menu pause et l'affichage des jumelles.

**🖥️ Pensé pour le PC**
- Souris et clavier, ou manette Xbox avec la disposition d'origine de 2005.
- Toutes les résolutions jusqu'à la 4K, champ de vision adapté au grand écran, sauvegarde rapide (F5) et chargement rapide (F9).
- Des menus utilisables à la souris, et des graphismes au maximum par défaut.

**🌐 En ligne**
- Parties Internet et en réseau local, et serveurs dédiés pour Windows et Linux.
- Des bots dans tous les modes multijoueur.
- Un pack d'armes par camp, et un choix de *Change Character* en cours de partie.
- Un menu vocal rapide (V) avec la voix d'origine de 2005 de chaque personnage, et un chat texte que les serveurs peuvent relayer vers Discord.

**⚙️ Simple au quotidien**
- Mises à jour automatiques en un clic, avec vos réglages et vos sauvegardes conservés.
- Votre progression solo affichée dans le menu Solo.

---

### 🚀 Démarrage rapide

1. **UT2004 avec le patch OldUnreal.**
   - **Pas encore UT2004 ?** Installez-le avec
     l'[installeur complet](https://www.oldunreal.com/downloads/ut2004/full-game-installers/) d'OldUnreal : il
     installe aussi le dernier patch OldUnreal, rien d'autre à faire.
   - **Vous l'avez déjà** (Steam, GOG, CD) ? Ajoutez le dernier
     [patch OldUnreal](https://github.com/OldUnreal/UT2004Patches/releases) (3374 du 20/10/2026 ou plus récent).
   - Notre installeur vérifie la version du patch et vous prévient si elle est trop ancienne.
2. **Les fichiers du jeu de 2005.** Téléchargez `Stargate_SG-1_-_The_Alliance-2005-12-15.7z` (environ 1 Go) sur
   [archive.org](https://archive.org/details/StargateSG1TheAlliance20051215) et laissez-le dans vos Téléchargements.
3. **L'installeur.** Téléchargez `Stargate-Redial-Alliance-v<version>-win64.zip` sur la
   [page Releases](https://github.com/Stargate-Redial/alliance-redial/releases), décompressez-le et lancez
   **Stargate Redial Setup.exe** (si SmartScreen s'affiche : *Informations complémentaires*, puis *Exécuter quand
   même*).
4. **Installez, puis jouez.** La fenêtre trouve seule le `.7z` et UT2004 : cliquez sur *Installer* (quelques
   minutes), puis sur *Jouer*. Les fois suivantes, lancez le jeu par son raccourci sur le bureau : il cherche seul les
   mises à jour et les installe en un clic.

### 🔄 Mises à jour automatiques

- Lancer le jeu par son raccourci cherche une nouvelle version sur cette page GitHub : aucun compte, aucune donnée
  personnelle.
- Une fenêtre montre les nouveautés et met à jour en un clic ; le téléchargement est vérifié par signature.
- Vos réglages et vos sauvegardes sont conservés.
- Vous pouvez le désactiver dans l'installeur. Détails : [Mise à jour en détail](docs/GUIDE.md#mise-à-jour-en-détail).

### 💡 À savoir

- L'installeur n'est pas signé : SmartScreen peut vous avertir. Cliquez sur *Informations complémentaires*, puis
  *Exécuter quand même*.
- Le *Contrôle intelligent des applications* de Windows 11, s'il est activé, bloque les programmes non signés :
  l'installeur ne peut pas s'y exécuter.
- Prévoyez environ 9 Go d'espace libre et une connexion Internet pendant l'installation.

Pour aller plus loin : [guide du joueur](docs/GUIDE.md#français) ·
[détails de l'installeur](docs/GUIDE.md#détails-de-linstalleur) (options, fichiers écrits, mise à jour,
désinstallation) · [problèmes connus](docs/KNOWN_ISSUES.md#français) · [triches](docs/CHEATS.md#français) ·
[serveurs dédiés](docs/SERVER.md#français) · [CHANGELOG](CHANGELOG.md) (en anglais)

---

### 🐞 Un problème ?

Ouvrez une [issue](https://github.com/Stargate-Redial/alliance-redial/issues) ou demandez sur
[Discord](https://discord.gg/SgHPP4mZyB). Indiquez la version, ce que vous avez fait et ce qui s'est passé, et
joignez `<UT2004>\System\UT2004.log` (voir [Signaler un problème](docs/GUIDE.md#signaler-un-problème)).

---

### 🗺️ Feuille de route (idées, sans promesse)

- **Traduction française** : sous-titres, menus, HUD et objectifs en français (les voix restent en anglais),
  avec un choix de langue dans les options et dans l'installeur.
- **Réplicateurs** : la version de 2005 contient encore du code et des modèles de Réplicateurs inutilisés (le
  Réplicateur araignée, la reine, un Réplicateur jouable avec son propre HUD), issus d'une mission coupée. Nous
  regarderons s'il est possible de leur redonner vie.

### 🙏 Remerciements

- L'équipe **OldUnreal**, pour les patchs communautaires d'UT2004 et son installeur complet : sans eux, ce projet
  n'existerait pas. <https://www.oldunreal.com>
- **CVLT OF OSIRIS**, qui a extrait cette version Xbox et l'a publiée en 2019, et **Hidden Palace**, qui l'a
  documentée.
- **Perception**, qui a créé *The Alliance* sur l'Unreal Engine 2.5 d'**Epic Games**.

---

### ⚖️ Mentions légales

Stargate Redial est un projet de fans gratuit et non commercial qui vise à préserver un prototype inédit. Il n'a
aucun lien avec MGM, Perception, JoWooD, Microsoft ou Epic Games, et aucune de ces sociétés ne l'a approuvé. Noms,
personnages et logos appartiennent à leurs propriétaires.

- **Ce que nous publions :** uniquement notre propre travail (installeur, outils, documents) et une image de titre
  créditée dans [NOTICE.md](NOTICE.md). Aucun fichier du jeu, rien qui en soit tiré.
- **Ce qui reste chez vous :** l'installeur transforme *votre* copie de la publication de 2019 en un mod sur
  *votre* PC. Les fichiers qu'il génère viennent du jeu : ne les mettez pas en ligne, ne les partagez pas, ne les
  incluez dans aucun paquet, ne les vendez pas, et ne laissez pas un serveur les distribuer (voir
  [docs/SERVER.md](docs/SERVER.md#français)).
- **Ayants droit :** pour une modification ou un retrait, ouvrez une issue ou contactez-nous sur Discord. Nous
  agirons rapidement.
- **Pas un avis juridique :** ce texte ne revendique aucun « usage équitable » dans aucun pays. Si vous
  redistribuez vous-même quelque chose, c'est sous votre responsabilité.

### 📜 Licence

Utilisation libre, non commerciale. Licences tierces : [NOTICE.md](NOTICE.md).
