# Notice

## Disclaimer

This is an independent, non-commercial fan preservation project by the [Stargate Database](https://stargatedatabase.link/en/) team, part of
[Stargate Redial](https://github.com/Stargate-Redial), which brings Stargate mods back on today's platforms. It
is **not affiliated with, authorised, sponsored or endorsed by** Metro-Goldwyn-Mayer (MGM), Perception Pty Ltd,
JoWooD Productions, Microsoft or Epic Games, nor by any other rights holder.

*Stargate SG-1* and related names and marks are the property of MGM. *Unreal*, *Unreal Tournament* and
*Unreal Engine* are trademarks of Epic Games. *Xbox* is a trademark of Microsoft. They are used here only to
describe what this software works with.

**No game data is included or distributed**, apart from one title picture (see *Game material* below).
Neither this repository nor the installer contains any other executable, package, map, texture, mesh, animation,
sound, music, speech, script source, configuration or other file from the game, or any file generated from them. The installer works on a copy of the 2019 release that the
user obtains independently; every converted file is created locally on the user's machine and stays there.

The installer carries our changes to the game's scripts as recipes: line positions, hashes and our own lines.
They contain no text of the original scripts and only work against a byte-identical, locally extracted copy of
the original.

The files the installer generates on your PC are derived from your own copy of the game and are for your
own use only: do not share, upload or sell them, and keep downloads off on any server you run. This project
cannot grant rights it does not hold, and this notice is not legal advice.

If you are a rights holder and object to this project, please open an issue or contact the maintainers. The
project will comply.

This software is provided "as is", without warranty of any kind.

### En français

Projet de fans indépendant et non commercial de l'équipe [Stargate Database](https://stargatedatabase.link/fr/), dans le cadre de
[Stargate Redial](https://github.com/Stargate-Redial), qui fait
revivre des mods Stargate sur les plateformes actuelles. Il n'est **ni affilié à, ni autorisé, parrainé ou
soutenu par** Metro-Goldwyn-Mayer (MGM), Perception Pty Ltd, JoWooD Productions, Microsoft ou Epic Games, ni
par aucun autre ayant droit. *Stargate SG-1* et les noms et marques associés appartiennent à MGM ; *Unreal*,
*Unreal Tournament* et *Unreal Engine* sont des marques d'Epic Games ; *Xbox* est une marque de Microsoft. Ils
ne sont cités que pour décrire ce avec quoi ce logiciel fonctionne.

**Aucune donnée du jeu n'est incluse ni distribuée**, hormis une image de titre (voir *Game material*
ci-dessous). L'installeur travaille sur une copie de la publication de
2019 que l'utilisateur se procure lui-même ; chaque fichier converti est créé sur sa machine et y reste. Si vous
êtes ayant droit et vous opposez à ce projet, ouvrez une issue ou contactez les mainteneurs : le projet s'y
conformera.

Les fichiers que l'installeur génère sur votre PC sont tirés de votre propre copie du jeu et réservés à votre
usage : ne les partagez pas, ne les mettez pas en ligne, ne les vendez pas, et laissez les téléchargements
désactivés sur tout serveur que vous hébergez. Ce projet ne peut accorder des droits qu'il ne détient pas, et cet
avis n'est pas un avis juridique.

## Game material

The installer window shows one title picture: the splash screen of the 2005 prototype *Stargate SG-1: The
Alliance* (Perception), cropped. It is shown for identification only; all rights belong to their owners. It is the
only material from the game in the installer, and the notice above still applies: this project is not affiliated
with or endorsed by any rights holder.

*En français :* la fenêtre de l'installeur affiche une image de titre : l'écran de démarrage du prototype de 2005
*Stargate SG-1: The Alliance* (Perception), recadré. Elle n'est montrée qu'à des fins d'identification ; tous les
droits appartiennent à leurs propriétaires. C'est le seul élément du jeu présent dans l'installeur, et l'avis
ci-dessus s'applique toujours : ce projet n'est ni affilié à, ni soutenu par aucun ayant droit.

The README on GitHub shows one frame of the E3 2005 trailer (JoWooD Productions / Perception), with a play button
added, as a link to the trailer on YouTube, and three screenshots of the game running with Redial. They are shown
for illustration only; all rights belong to their owners. They are not part of the installer.

*En français :* le README sur GitHub montre une image de la bande-annonce de l'E3 2005 (JoWooD Productions /
Perception), avec un bouton de lecture ajouté, comme lien vers la bande-annonce sur YouTube, et trois captures du
jeu lancé avec Redial. Elles ne sont montrées qu'à titre d'illustration ; tous les droits appartiennent à leurs
propriétaires. Elles ne font pas partie de l'installeur.

## Licence

The installer and its tools are provided free of charge for non-commercial use, without warranty of any kind.
They are our own code: the readers of the game's packages, script text, default properties and LIPSinc data
were written independently from a functional description, and the installer does not download or run any
third-party GPL tool besides ffmpeg (a separate program, below). The installer window, its starter program
`Stargate Redial Setup.exe` and its icon are our own work too.

## Third-party software

| Component | Used for | Licence | How it is obtained |
|---|---|---|---|
| [FFmpeg](https://ffmpeg.org) (gyan.dev build `2025-01-08-git-251de1791e` essentials) | decoding Xbox ADPCM, encoding Ogg Vorbis | GPL-3.0 (this build) | not included: downloaded by the installer from the build's GitHub release, SHA-256 checked; runs as a separate program. `--ffmpeg` uses yours |
| [7-Zip](https://www.7-zip.org) `7zr.exe` 26.06 | extracting the release archive and the FFmpeg archive | LGPL-2.1 | not included: downloaded from the official GitHub release, SHA-256 checked, only when no 7-Zip is installed |
| CPython 3.13 runtime and standard library | runs the installer (compiled into it) | PSF License | included in the installer (`licenses/Python-LICENSE.txt`) |
| Tcl/Tk 8.6 (as shipped with CPython 3.13 for Windows) | the installer window | Tcl/Tk licence (BSD-style) | included in the installer (`licenses/Tcl-Tk-license.txt`) |
| Nuitka runtime library | the compiled installer | AGPL-3.0 with the Nuitka Runtime Library Exception | included in the installer (`licenses/Nuitka-Runtime-Library-Exception.txt`) |
| Microsoft Visual C++ runtime | the compiled installer | Visual Studio redistributable terms | included in the installer |
| Unreal Tournament 2004 | engine, compiler (`ucc`) | Epic Games EULA | the user's own copy |
| OldUnreal UT2004 patch 3374 | updated engine binaries | OldUnreal / Epic terms | installed by the user |
