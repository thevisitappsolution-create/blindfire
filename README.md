# BLINDFIRE

> *Tes yeux mentent. Tes oreilles, jamais.*

Jeu de tir sensoriel dans le noir total : tu localises les monstres **à l'oreille**
(son 3D binaural), tu lèves ton téléphone pour éclairer et viser — mais la lumière
**révèle aussi ta position**. Un seul bouton : tirer. Tête = mort instantanée.

Basé sur le PRD v0.1 (`PRD_Jeu_Duel_Obscurite.md`) — MVP « Option A » : le mode
solo Survie d'abord, pour valider le game feel avant le PvP.

## Jouer maintenant (iPhone)

Le prototype est une web-app autonome. **Lien principal (gyroscope actif)** :

**https://thevisitappsolution-create.github.io/blindfire/**

> Il existe aussi une version artifact (https://claude.ai/code/artifact/f2a039c2-e9bb-483b-ba0a-f4527b18e188),
> mais elle est intégrée dans un cadre qui **bloque les capteurs de mouvement sur iOS**
> (refus automatique sans pop-up) — utilisable uniquement en mode tactile / sur ordinateur.

1. Ouvre le lien **directement dans Safari** sur ton iPhone (pas dans le navigateur
   intégré d'une autre app — les capteurs de mouvement y sont souvent bloqués).
2. Branche tes **écouteurs** (indispensable — le son est le jeu).
3. Touche **JOUER**, puis sur l'écran « Capteurs » touche **ACTIVER LE GYROSCOPE**
   et accepte la demande iOS « Mouvement et orientation ». L'écran confirme
   « Gyroscope actif ✓ » quand les données arrivent, et t'explique quoi faire sinon.
4. Tiens le téléphone à la verticale devant toi, comme une caméra :
   - **pivote physiquement** sur toi-même pour balayer la pièce ;
   - **baisse** le téléphone = noir, silence, sécurité ;
   - **lève-le** = lumière, visée à hauteur de tête… et exposition ;
   - bouton rouge = **tirer** (une balle, puis rechargement).
5. Astuce : Partager → « Sur l'écran d'accueil » pour le plein écran.

Sans gyroscope (ou sur ordinateur) : glisser sur l'écran pour viser,
Espace ou clic sur le bouton pour tirer.

## Contenu de la V0.1

- **Audio 3D binaural (HRTF)** entièrement synthétisé au runtime : pas, souffle,
  grognements, cris, gouttes, écho de caverne, battement de cœur qui s'accélère
  avec le danger — zéro fichier audio, zéro dépendance.
- **Mécanique-clé du PRD** : inclinaison = visée verticale **et** niveau de lumière.
  Impossible d'être à la fois invisible et précis.
- **Symétrie sonore** : tirer alerte tous les monstres ; la lumière les enrage.
- **Tête = kill, corps = ralenti + repoussé + révélé** (contour rouge).
- **Yeux luminescents** : chaque monstre se repère à ses yeux qui brillent dans le
  noir, de plus en plus fort à mesure qu'il approche (avec clignements).
- **Encerclement progressif** : vagues 1–4 face à la position de départ (±90°),
  5–6 débordement (±135°), 7+ à 360° — annoncé en jeu.
- **Test auditif gauche/droite** (menu) : trois sons à localiser pour vérifier
  que le casque n'est pas inversé avant de jouer.
- **Pavé fléché 8 directions** en mode tactile (haut/bas/gauche/droite +
  diagonales, maintenir pour pivoter, accélération progressive), en plus du
  glisser-viser.
- **Sons personnalisés** : les WAV sources vivent dans `Sons/` (ignoré par git,
  trop lourd) ; ils sont compressés en `.m4a` dans `docs/sons/` (ffmpeg, AAC 96k)
  et chargés par la version GitHub Pages — ambiance en boucle de 96 s et son de
  début de partie. La version artifact garde l'ambiance synthétique en repli.
- **Bestiaire illustré crescendo** : zombie, loup putréfié au sol (vague 2+),
  chauve-souris en zigzag (4+) — sprites fournis dans `Monstre/`, détourés
  (damier incrusté supprimé) et pré-assombris en 9 niveaux — plus téléporteurs
  (8+ : il change de couleur, la seconde d'après il a bougé). Chaque créature a
  ses propres pas : traînants (zombie), pattes feutrées rapides (loup),
  battements d'ailes (chauve-souris).
- **Dévoration** : la gueule du monstre qui t'attrape grossit en fondu jusqu'à
  avaler l'écran (zoom sur la bouche), avec sang et hurlement.
- **Pause** : bouton ⏸ en haut à droite en partie (auto-pause quand l'app passe
  en arrière-plan) ; logo BlindFire fourni au menu (repli texte hors ligne).
- **3 vies** : être dévoré coûte une vie et relance la vague en cours ; les trois
  perdues, on repart de zéro.
- **Reprise de partie** : après 10 minutes de jeu cumulées, un bouton « Reprendre —
  vague N » apparaît au menu et restaure la vague, le score et les vies
  sauvegardés à chaque début de vague (localStorage).
- **Fin de partie : LA HORDE (vague 20)** : 20 zombies + 10 chauves-souris +
  5 loups mélangés, arrivant de loin (24-34 m) en marche inexorable ; les abattre
  tous = victoire (+500 pts, +2000 pièces).
- **Économie (bêta, 100 % virtuelle)** : boutique d'armes 2/3/4/5 coups
  (200/400/600/1000 pièces — plus de coups = rechargement plus long), bonus de
  vies 24 h / 7 j, coffre toutes les 10 min de jeu (50-150 pièces, barre de
  progression en bas de l'écran), parrainage par partage (paliers 10/20/30/50
  amis). Aucun paiement réel pour l'instant ; grille indicative 100 pièces ≃ 1 €.
- **Profil & stats** : pseudo, avatar, précision, réflexe moyen, victoires,
  meilleurs scores locaux — le classement mondial en ligne nécessitera un
  backend (Firebase/Supabase) à la sortie.
- **Mentions légales intégrées** (écran dédié) : avertissements horreur/
  photosensibilité/volume, RGPD (données 100 % locales, bouton d'effacement),
  monnaie virtuelle — modèle à faire valider juridiquement avant commercialisation.
- **Lumière = vitesse** : à luminosité maximale, toutes les créatures foncent à
  leur vitesse max. Et leurs yeux brillent d'autant plus qu'il fait sombre
  (l'inverse en pleine lumière).
- **Épouvante** : gouttes de sang sur l'écran et visage horrifique en jumpscare
  quand on est dévoré ; souffles chuchotés spatialisés à la position des
  créatures, noyés dans une réverbération de château hanté (réponse
  impulsionnelle synthétique ~3 s sur tout l'univers sonore).
- **Munition unique + rechargement** (1,4 s) — le tir raté coûte cher.
- **Mode Survie** : vagues croissantes, score, record local.
- **Tutoriel progressif** conforme au PRD : Écoute → Lumière → Tir → Survie.
- Gyroscope via quaternions (pas de gimbal lock à la verticale), repli tactile,
  wake lock, option « flashs réduits » (photosensibilité).

## Architecture

Un seul fichier, `index.html` (~1 100 lignes) :
- `AU` — moteur audio Web Audio (PannerNode HRTF, synthèse procédurale, bus d'écho) ;
- `Voice` — voix spatialisée d'un monstre (grognement continu, pas, cris) ;
- `Monster` — IA (rôde/pause/charge/attaque), zones de tir tête/corps ;
- `Input` — fusion gyroscope (quaternions type three.js) + repli tactile ;
- rendu Canvas 2D : silhouettes, halo de lampe, poussière, vignette cardiaque.

## Feuille de route

1. **V0.1 (fait)** — prototype web jouable sur iPhone : valider « est-ce tendu et fun ? »
2. **V0.2** — équilibrage d'après tes retours, roguelite léger (améliorations entre
   vagues), retour haptique (Android / via wrapper natif).
3. **V1 iOS (App Store)** — empaqueter tel quel avec **Capacitor**
   (`npx cap add ios`) : nécessite un Mac + Xcode + compte Apple Developer (99 $/an),
   ou un service de build cloud (Ionic Appflow). La base web actuelle est 100 %
   compatible ; on y gagne haptique, icône, plein écran natif.
4. **V1.x Android (Play Store)** — même base, `npx cap add android` (buildable
   directement depuis ce PC Windows).
5. **V2** — Duel 1v1 en ligne par code (serveur relais autoritaire), puis
   matchmaking, rangs, cosmétiques (cf. PRD §7–9).

## Développement local & déploiement

- `index.html` — source unique du jeu (format « contenu nu » compatible artifact).
  L'ouvrir dans un navigateur suffit pour tester au clavier/souris.
- `docs/index.html` — copie enveloppée (`<!doctype html>…`) servie par **GitHub Pages**
  (Réglages du dépôt → Pages → branche `main`, dossier `/docs`).

Après toute modification de `index.html`, régénérer la copie et pousser :

```powershell
$c = Get-Content index.html -Raw -Encoding utf8
[IO.File]::WriteAllText("docs\index.html", "<!doctype html>`n<html lang=`"fr`">`n$c`n</html>")
git add -A; git commit -m "maj"; git push
```
