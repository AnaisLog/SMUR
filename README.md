# 🧱 Mon aventure LEGO (SMUR)

Petit outil en **un seul fichier HTML** (`index.html`) pour préparer l’oral du 17 novembre : des défis à cocher, un personnage LEGO qui avance sur un itinéraire, et un compte pour retrouver ses données sur tous ses appareils.

## Ce qu’on voit

1. **Le personnage LEGO et l’itinéraire** (de l’ambulance à la porte du bureau d’entretien). Il avance à mesure que les cases sont cochées (61 cases au total) et recule si on en décoche.
2. **« Aujourd’hui, j’ai : »** : les cases des 4 piliers (émotions 🌿, sommeil 🌙, alimentation 🍎, activité physique 👟), compactes, en haut de page.
3. **« Mon humeur du jour »** : 5 émoticônes à toucher.
4. **Les défis** (contenu repris tel quel) : un **onglet déroulant par défi** (Défi 1 à 8), puis le **Bilan final** et un onglet par journée du **14 au 17 novembre**. Dans chaque défi : l’échéance (dates déjà renseignées, modifiables), les étapes, l’action et « Validation : Défi terminé » sont des cases à cocher. Le suivi de progression se met à jour tout seul.
5. **Le bouton « Valider ✨ »** (toujours visible en bas de l’écran) enregistre tout dans le compte et affiche « ✅ Enregistré ! ».

Toutes les cases sont **modifiables à tout moment**, et on peut valider **autant de fois que l’on veut**. Il n’y a **aucune remise à zéro automatique**, ni message négatif.

## 🔒 Admin

Le bouton « 🔒 Admin » (bas de page) demande le **code Admin** (**1234** par défaut) et ouvre un petit tableau de bord : actions des 4 piliers (1 à 5 par pilier), code Admin, image du personnage, historique des enregistrements, « Tout réinitialiser » (deux clics pour confirmer) et déconnexion.

## 👤 Compte et données (Firebase Realtime Database)

La **connexion est obligatoire** : identifiant + mot de passe (6 caractères minimum), avec « Créer un compte » la première fois. L’identifiant est transformé en adresse technique `identifiant@aventure-lego.app` : aucun e-mail n’est envoyé et il n’y a pas de récupération de mot de passe.

Les données sont envoyées dans la base **à chaque « Valider »** (et lorsque l’on quitte la page s’il reste des modifications). Entre-temps, elles sont gardées sur l’appareil, donc rien ne se perd.

### Règles de sécurité de la base

```json
{
  "rules": {
    ".read": false,
    ".write": false,
    "aventure": {
      "$uid": {
        ".read": "auth != null && auth.uid === $uid",
        ".write": "auth != null && auth.uid === $uid"
      }
    },
    "config": {
      ".read": "auth != null",
      ".write": false
    }
  }
}
```

### Configuration

Dans `index.html`, le bloc `FIREBASE` (début du script) contient l’URL de la base et la clé API web (elle n’est pas secrète : ce sont les règles ci-dessus qui protègent les données).

## 🔄 Remise à zéro de tous les comptes

Dans la console Firebase (*Realtime Database → Données*), créer ou modifier le nœud **`config` → `resetAt`** avec un nombre **plus grand que le précédent** (par exemple `20261104`). Au prochain lancement, **chaque compte se remet à zéro une seule fois** : cases, humeur et historique sont effacés ; les actions des piliers, le code Admin et l’image sont conservés.

## 🧹 Tout effacer (données et comptes)

1. **Données :** console Firebase → *Realtime Database → Données* → supprimer le nœud **`aventure`** (et `pieces` s’il existe).
2. **Comptes :** *Authentication → Users* → sélectionner tous les utilisateurs → supprimer.
3. **Appareils :** la version actuelle du fichier ignore les anciennes données et les anciennes sessions enregistrées sur les appareils : chacun repart d’une page vierge avec la fenêtre de connexion, puis « Créer un compte ».

Une fois les nouveaux comptes créés, on peut désactiver la création de comptes dans *Authentication → Settings → User actions*.

## Publier avec GitHub Pages

Le fichier s’appelle déjà `index.html` : *Settings → Pages* → branche `main`.
