# 🧱 Mon aventure LEGO (SMUR)

Petit jeu motivationnel en **un seul fichier HTML** (`aventure-lego.html`), pensé pour aider à **initier l’action** quand le TDAH rend le démarrage difficile. Aucune installation : on ouvre le fichier dans un navigateur.

## Principe

Le personnage LEGO SMUR parcourt une **carte d’itinéraire** de 17 étapes (de l’ambulance et du sac de secours jusqu’à la porte du bureau d’entretien du concours, en passant par le cœur, les poumons, le cerveau…). Chaque journée validée le fait avancer d’une étape.

## Les 4 piliers

1. 🌿 Gestion des émotions
2. 🌙 Sommeil
3. 🍎 Alimentation
4. 👟 Activité physique

Chaque pilier contient de **1 à 5 actions personnalisées**, modifiables dans **⚙️ Configuration** (masquable).

## Déroulé d’une journée

1. On note son **humeur** en cliquant sur un émoticone (😞 😕 😐 🙂 😄).
2. On coche les actions réalisées.
3. Quand tout est coché, le bouton **« Demander la validation »** apparaît.
4. Un **tiers** (parent, conjoint, ami) saisit le code secret (**1234** par défaut, modifiable dans Configuration).
5. La validation fait avancer le personnage sur la carte, avec confettis, message festif et badge.

Les coches se remettent à zéro chaque nouveau jour, sans aucune conséquence.

## Bienveillance

- Aucune sanction, aucun message culpabilisant ou alarmiste.
- Si **aucune action n’est cochée pendant 24 h**, le personnage revient simplement à l’étape précédente de la carte, avec un message neutre et doux.
- L’humeur est un simple repère, jamais une condition pour avancer.

## Tester

Dans **⚙️ Configuration → Outils de test** :

- **Simuler 1 jour sans action** : déclenche le recul d’une étape.
- **Tout réinitialiser** : repart de zéro (l’image et l’historique d’humeur sont conservés).

## Personnaliser l’image

L’image du personnage est intégrée au fichier. Pour la changer : **Configuration → Choisir mon image LEGO**.

## Données

Tout est enregistré **localement dans le navigateur** (`localStorage`) : rien n’est envoyé sur Internet. Changer d’appareil ou de navigateur repart d’une progression vierge.

## Publier avec GitHub Pages

Renommer `aventure-lego.html` en `index.html`, puis *Settings → Pages* → branche `main`.
