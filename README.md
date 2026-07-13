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
