# 🧱 Mon aventure LEGO (SMUR)

Petit jeu motivationnel en **un seul fichier HTML** (`aventure-lego.html`), pensé pour aider à **initier l’action** quand le TDAH rend le démarrage difficile. Aucune installation : on ouvre le fichier dans un navigateur.

## Principe

Le personnage LEGO SMUR parcourt une **carte d’itinéraire** de 17 étapes, de l’ambulance et du sac de secours jusqu’à la porte du bureau d’entretien du concours, en passant par le cœur, les poumons, le cerveau, le défibrillateur… Chaque journée validée le fait avancer d’une étape.

L’interface est volontairement épurée : fond crème chaleureux, peu d’éléments, tout est lisible d’un coup d’œil.

## Les 4 piliers

1. 🌿 Gestion des émotions
2. 🌙 Sommeil
3. 🍎 Alimentation
4. 👟 Activité physique

Chaque pilier contient de **1 à 5 actions personnalisées**, modifiables dans l’**🔒 Admin** (voir plus bas), qui n’est pas accessible à la joueuse.

## Déroulé d’une journée

1. On note son **humeur** en cliquant sur un émoticone (😞 😕 😐 🙂 😄).
2. On coche les actions réalisées.
3. Quand tout est coché, le bouton **« Demander la validation »** apparaît.
4. Un **tiers** (parent, conjoint, ami) saisit le code secret (**1234** par défaut, modifiable dans l’Admin).
5. La validation fait avancer le personnage sur la carte, avec confettis, message festif et badge.

Les coches se remettent à zéro chaque nouveau jour, sans aucune conséquence.

## 📝 To-do list

Un encadré à part permet d’ajouter des tâches libres, de les **cocher** (elles restent visibles, barrées) et de les **supprimer** avec ✕. Cette liste est indépendante du jeu : elle ne compte ni pour la validation de la journée, ni pour la règle d’inactivité.

## Bienveillance

- Aucune sanction, aucun message culpabilisant ou alarmiste.
- Si **aucune action des piliers n’est cochée pendant 24 h**, le personnage revient simplement à l’étape précédente de la carte, avec un message neutre et doux.
- L’humeur est un simple repère, jamais une condition pour avancer.

## Tester

Dans **🔒 Admin → Outils de test** :

- **Simuler 1 jour sans action** : déclenche le recul d’une étape.
- **Tout réinitialiser** : repart de zéro (l’image, l’historique d’humeur et la to-do list sont conservés).

## Personnaliser l’image

La figurine est intégrée au fichier. Pour la changer : **Admin → Choisir mon image LEGO**.

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `aventure-lego.html` | Le jeu complet (HTML, CSS et JavaScript, figurine et favicon inclus) |
| `favicon.png`, `favicon.ico` | Icône de l’onglet, en fichiers séparés (optionnel) |
| `README.md` | Ce document |

Pour utiliser les fichiers séparés, ajouter dans le `<head>` : `<link rel="icon" href="favicon.ico">`.

## 🔒 Admin

Les réglages (actions des 4 piliers, code secret, image, outils de test) sont **réservés à un tiers**. Le bouton « 🔒 Admin » en bas de page demande le **code secret** (le même que pour la validation) ; le panneau se referme avec « 🔒 Verrouiller » ou au rechargement de la page.

> Ce verrou protège contre un usage involontaire, pas contre un utilisateur averti : le code est stocké avec les données.

## ☁️ Données sur Firebase (Realtime Database)

Les données (progression, actions, humeur, to-do list, code) sont enregistrées dans **Firebase Realtime Database** et synchronisées entre appareils (par exemple le téléphone de la joueuse et celui du proche). Une copie locale sert de secours hors connexion.

### Mise en place

1. Sur [console.firebase.google.com](https://console.firebase.google.com), créer un projet, puis **Build → Realtime Database → Créer une base**.
2. Copier l’**URL de la base** (du type `https://mon-projet-default-rtdb.europe-west1.firebasedatabase.app`).
3. Dans l’onglet **Règles**, coller :

```json
{
  "rules": {
    ".read": false,
    ".write": false,
    "aventure": {
      "$espace": { ".read": true, ".write": true }
    }
  }
}
```

4. Dans `aventure-lego.html`, modifier le bloc `FIREBASE` (au début du script) :

```js
const FIREBASE = {
  url: "https://smur-leila-default-rtdb.europe-west1.firebasedatabase.app/",
  space: "17nov2026"
};
```

Tant que ces valeurs ne sont pas changées, l’application fonctionne en **mode local** (l’Admin indique l’état de la synchronisation).

### À savoir sur la confidentialité

Avec ces règles, **toute personne connaissant l’identifiant d’espace peut lire et modifier les données**. Si le dépôt est public, cet identifiant est visible dans le code. Pour un usage plus sensible (humeur, santé), il est possible d’ajouter **Firebase Authentication** et des règles du type `auth != null`.

## Publier avec GitHub Pages

Renommer `aventure-lego.html` en `index.html`, puis *Settings → Pages* → branche `main`.
