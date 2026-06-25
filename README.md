# Mon carnet — installation

Un petit site privé pour noter tes prises au quotidien sur le téléphone, et tout
retrouver sur l'ordinateur. Couleurs grenat & sable, catégories de ta nutritionniste.
Trois fichiers : `index.html`, `firebase-config.js`, `README.md`.

---

## 1. Créer le projet Firebase (≈ 5 min, gratuit)

1. Va sur **console.firebase.google.com** → **Ajouter un projet**. Donne-lui un nom
   (ex. `mon-carnet`). Tu peux désactiver Google Analytics, ce n'est pas utile ici.
2. Dans le menu de gauche : **Créer** → **Authentication** → **Commencer** →
   onglet **Sign-in method** → active **Adresse e-mail/Mot de passe** → **Enregistrer**.
3. Toujours à gauche : **Créer** → **Firestore Database** → **Créer une base de données**
   → choisis un emplacement en Europe → démarre en **mode production**.
4. Onglet **Règles** de Firestore : remplace tout par ceci, puis **Publier** :

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{uid}/entries/{doc} {
         allow read, write: if request.auth != null && request.auth.uid == uid;
       }
     }
   }
   ```
   (Ces règles font que toi seule peux lire et écrire tes propres notes.)

## 2. Récupérer ta config

1. Roue crantée en haut à gauche → **Paramètres du projet**.
2. Section **Tes applications** → icône **</>** (Web) → donne un surnom → **Enregistrer**.
3. Firebase affiche un bloc `const firebaseConfig = { ... }`. Copie ces valeurs.
4. Ouvre **`firebase-config.js`** et remplace chaque `TODO...` par tes valeurs. Enregistre.

## 3. Mettre en ligne sur GitHub Pages

1. Crée un dépôt sur **github.com** (ex. `mon-carnet`), **Public** ou **Private** au choix.
2. Dépose les trois fichiers à la racine (glisser-déposer via *Add file → Upload files*).
3. Dans le dépôt : **Settings** → **Pages** → *Source* : **Deploy from a branch** →
   branche `main`, dossier `/ (root)` → **Save**.
4. Au bout d'une minute, l'adresse apparaît : `https://ton-pseudo.github.io/mon-carnet/`.

## 4. Sur le téléphone

1. Ouvre l'adresse dans Safari (iPhone) ou Chrome (Android).
2. Crée ton compte (e-mail + mot de passe) la première fois.
3. **Ajouter à l'écran d'accueil** → tu as une icône comme une vraie appli.
4. Connecte-toi avec le **même compte** sur l'ordinateur : tes notes s'y retrouvent.

---

## Utilisation
- **+** en bas : noter un moment. Seuls le type et la description sont nécessaires ;
  « Plus de détails » est facultatif.
- **Journal** : tes entrées par jour. Touche une carte pour la modifier ou la supprimer.
- **Aperçu** : tes repères, recalculés à chaque ajout. À regarder avec ta nutritionniste.
- Se déconnecter : double-clic / double-tap sur le bonjour en haut.

## Changer les catégories
Tout est en haut de `index.html` (cherche `const TYPES`, `LIEUX`, `QUI`,
`POS`, `ECR`, `EMO_A`, `EMO_P`). Modifie les listes, ré-enregistre, c'est tout.

## Couleurs
Au tout début du `<style>` dans `index.html` : les variables `--garnet`, `--sand`, etc.
Mets tes hex exacts si tu en as d'autres.
