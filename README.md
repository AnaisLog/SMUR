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
3. Le bouton **« Valider »** est disponible à tout moment, même si toutes les actions ne sont pas cochées.
4. Un clic sur « Valider » **enregistre la journée** et affiche un message « Enregistré » : l’aventurière passe à l’étape suivante de la carte, avec confettis, message festif et badge. Aucun code n’est demandé. Il n’y a qu’une validation par jour : ensuite le bouton indique « ✅ Enregistré aujourd’hui ».

La journée change à **23 h 58** (et non à minuit). À **23 h 58**, tout est remis à zéro **et l’enregistrement du jour est envoyé en même temps** : les actions des piliers et les tâches de la to-do list sont décochées (les tâches restent dans la liste) et la validation du jour repart de zéro, sans aucune conséquence.

Le navigateur ne peut rien faire lorsque l’application est fermée : dans ce cas, la remise à zéro et l’enregistrement de la veille se font à la prochaine ouverture, avec les données exactes de la veille.

## 📅 Un enregistrement par jour

Chaque jour a son propre enregistrement (clé `jours/AAAA-MM-JJ` dans les données) : nombre d’actions faites sur le total, actions cochées, tâches cochées, humeur, journée validée ou non, et étape de l’aventure. L’**🔒 Admin** affiche l’historique des 30 derniers jours. Un jour où l’application n’est jamais ouverte n’a pas d’enregistrement.

## 📝 To-do list

Un encadré à part permet d’ajouter des tâches libres, de les **cocher** (elles restent visibles, barrées) et de les **supprimer** avec ✕. Cette liste est indépendante du jeu : elle ne compte ni pour la validation de la journée, ni pour la règle d’inactivité. Le même encadré est aussi disponible dans l’**🔒 Admin**, pour que le proche puisse ajouter, cocher ou supprimer des tâches.

## 📎 Pièces jointes et défi

Chaque tâche de la to-do list a un bouton **📎** pour y **ajouter et envoyer une pièce jointe** (photo, PDF, document texte). Les photos sont réduites automatiquement ; les autres fichiers sont limités à 1 Mo. Le nom de la pièce jointe s’affiche sur la tâche : un clic la télécharge.

La **première pièce jointe envoyée** débloque le **défi 1** : le message **« Tu viens de débloquer un nouveau défi 🏆 »** s’affiche et une to-do list d’instructions à cocher apparaît. Sous les instructions, le bouton **« Validé ✅ »** ouvre **le défi suivant** (même message). Les défis se définissent dans l’**🔒 Admin** (rubrique « Défis », jusqu’à 10, chacun avec un titre et de 1 à 8 instructions). Un défi reste affiché chaque jour, **sans remise à zéro**, jusqu’à ce qu’on appuie sur « Validé ». Après le dernier défi, un message de félicitations s’affiche.

### Envoi par e-mail

Un bouton **✉️** apparaît sur les tâches qui ont une pièce jointe (dans l’**🔒 Admin**, on peut en plus renseigner une **adresse e-mail de destination**, rappelée dans le message). Sur téléphone, il ouvre le menu de partage avec le fichier prêt à envoyer (choisir l’application e-mail). Sur ordinateur, il télécharge le fichier et ouvre un e-mail pré-rempli : il reste à joindre le fichier. Un envoi entièrement automatique, sans action de la joueuse, demande un petit serveur (par exemple une Cloud Function Firebase).

Les pièces jointes sont gardées sur l’appareil et, quand Firebase est configuré, envoyées dans `pieces/<compte>` (voir les règles plus bas).

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

Les réglages (actions des 4 piliers, code secret, image, outils de test) sont **protégés par le bouton « 🔒 Admin »**, en bas de page, qui demande le **code Admin** (**1234** par défaut) et sert uniquement à accéder à ce tableau de bord ; le panneau se referme avec « 🔒 Verrouiller » ou au rechargement de la page.

> Ce verrou protège contre un usage involontaire, pas contre un utilisateur averti : le code est stocké avec les données.

## 👤 Compte et données sur Firebase

Chaque personne a **son compte** (identifiant + mot de passe). Ses données (progression, actions, humeur, to-do list, historique par jour, code Admin) sont enregistrées dans **Firebase Realtime Database**, sous son propre espace, et se retrouvent sur tous ses appareils. Une copie locale par compte sert de secours hors connexion.

### Utilisation

- Au premier lancement, une fenêtre **Connexion** s’affiche : « Créer un compte » (identifiant simple + mot de passe de 6 caractères minimum) ou connexion à un compte existant. La connexion est **obligatoire** : tant que l’on n’est pas connecté, la fenêtre reste affichée et le jeu est inaccessible (une session déjà ouverte continue de fonctionner hors connexion).
- À la création du compte, la progression déjà présente sur l’appareil est reprise dans le compte.
- Le bouton **👤 Se connecter**, en haut à droite, ouvre la fenêtre de connexion ; une fois connecté, il affiche l’identifiant. Tant que Firebase n’est pas configuré, il l’indique par un message.
- La session est conservée et se renouvelle automatiquement. Le bouton **Se déconnecter / Se connecter** se trouve dans l’**🔒 Admin**, qui affiche aussi le compte connecté.
- La joueuse et le proche peuvent utiliser **le même compte** sur leurs deux appareils : ils voient alors les mêmes données.

L’identifiant est transformé en adresse technique du type `identifiant@aventure-lego.app` : aucune vraie adresse e-mail n’est demandée, et aucun e-mail n’est envoyé (pas de récupération de mot de passe par e-mail).

### Mise en place (une seule fois)

1. Sur [console.firebase.google.com](https://console.firebase.google.com), créer un projet.
2. **Build → Authentication → Sign-in method** : activer **E-mail/Mot de passe**.
3. **Build → Realtime Database → Créer une base**, puis copier son **URL** (du type `https://mon-projet-default-rtdb.europe-west1.firebasedatabase.app`).
4. **Project settings → General → Web API Key** : copier la clé (elle n’est pas secrète, ce sont les règles qui protègent les données).
5. Onglet **Règles** de la base, coller :

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
    "pieces": {
      "$uid": {
        ".read": "auth != null && auth.uid === $uid",
        ".write": "auth != null && auth.uid === $uid"
      }
    }
  }
}
```

6. Dans `aventure-lego.html`, modifier le bloc `FIREBASE` (au début du script) :

```js
const FIREBASE = {
  url: "https://mon-projet-default-rtdb.europe-west1.firebasedatabase.app",
  apiKey: "AIza..."
};
```

Tant que `url` et `apiKey` ne sont pas renseignées, l’application fonctionne en **mode local** et le bouton de connexion est masqué.

### Confidentialité

Grâce aux règles ci-dessus, chaque compte ne peut lire et modifier **que ses propres données**, même si le dépôt est public. Tout le monde peut toutefois créer un compte : pour l’empêcher une fois les comptes créés, désactiver la création de comptes dans Firebase (*Authentication → Settings → User actions*). Le code Admin est stocké avec les données du compte : c’est un verrou léger entre la joueuse et le proche, pas une protection contre un utilisateur averti.

## Publier avec GitHub Pages

Renommer `aventure-lego.html` en `index.html`, puis *Settings → Pages* → branche `main`.
