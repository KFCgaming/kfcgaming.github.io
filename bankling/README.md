# 🪴 Bankling — Gestionnaire de finances local

> **« Bankling — fais pousser ton argent » 🌱**

Application web **100 % locale et hors-ligne** (PWA) : aucune librairie externe, aucun serveur,
aucune donnée ne quitte ton appareil. Tout est enregistré dans le `localStorage` du navigateur.

- **Logo / mascotte** : *Bling* 🌱, la petite plante dont les feuilles sont des billets.
- **Nom** : Bankling = *bank* (banque) + *-ling* (le petit en anglais) + *bling* (l'argent qui brille). ✨

---

## 🚀 Hébergement GitHub Pages (recommandé — 3 étapes, zéro config)

Le projet est **pensé pour GitHub Pages** : tous les chemins sont relatifs, donc
l'appli fonctionne à `https://<ton-user>.github.io/<ton-repo>/`, quel que soit le nom du repo.

1. **Crée un repo** sur GitHub (public, nom libre, ex. `bankling`).
2. **Ajoute les fichiers** du dossier (Drag & drop sur `Add file → Upload files`) :
   `index.html`, `sw.js`, `manifest.webmanifest`, `README.md` et les 4 icônes
   `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png`.
   (Rien d'autre à créer.)
3. Active Pages : **Settings → Pages → Source : « Deploy from a branch » → main / (root) → Save**.
   Après ~1 minute, l'appli est en ligne sur `https://<ton-user>.github.io/<ton-repo>/` ✅

C'est tout : le service worker s'auto-enregistre, l'appli est installable et fonctionne hors-ligne.
Quand tu mets à jour des fichiers, il suffit de re-pusher (les visiteurs reçoivent
automatiquement la nouvelle version).

> 💡 Pour l'installer sur téléphone : ouvre l'URL → menu ⋮ → « Ajouter à l'écran d'accueil » /
> « Installer l'application ».

### Variante : tester en local avant de publier
```bash
cd localbank-pwa
python -m http.server 8080
# → http://localhost:8080
```

---

## ✨ Fonctionnalités v4

| Fonction | Détail |
|---|---|
| **Wallets libres** | Plus de CB / Espèces / PayPal imposés : tu crées tes wallets avec **nom + emoji** (ex. « Mon PayPal 🅿️ », « Livret A 🏦 »). |
| **Import intelligent (ancien format)** | Détecte les JSON de l'ancienne version (card/cash/paypal) et te fait **choisir vers quel wallet** va chaque ancien portefeuille — **valeurs conservées**, noms/emojis à toi. |
| **Graphique paramétrable** | **Argent / jour** ou **Argent / transaction**, intervalles : 7 j, 1 mois, 3 mois, 6 mois, 1 an, tout, personnalisé. Périmètre : wallet ou tous. Tooltip + export PNG. |
| **Wrapped** | Bilan sur une période : dépensé / reçu, moyennes, plus grosse dépense, jour le plus dépensier, top catégories, recherche approximative (« bus » → « bus 12 », « BUS », « BZS 12 »…). |
| **Catégories** | Directement dans l'onglet du wallet (montant → intitulé → catégorie → OK) + catégories personnalisées. |
| **Historique amélioré** | Recherche approximative, filtres (type, catégorie, wallet), regroupement par jour, suppression d'opération (solde recalculé). |
| **Design** | Interface refaite (cartes, gradients, navigation basse, drawer, animations) avec **8 thèmes** (violet, bleu, vert, orange, rouge, rose, sarcelle, N&B). |
| **Mini-stats** | Dépensé / reçu ce mois-ci + solde total de tous les wallets. |
| **Export** | Backup JSON v4 (téléchargement ou copie), import avec choix **fusionner** ou **remplacer**. |

## 🗂 Données & migration
- Stockage : `localStorage` (clé `bankling_v4`) — **attention** : sur `user.github.io`, toutes
  tes repos partagent la même origine, donc la même base locale. C'est sans risque (clé unique),
  mais ne fais pas tourner deux apps de finances sur la même origine.
- **Migration automatique** : les données `localbank_v4` (ancien nom) sont reprises à l'ouverture.
  Les données v3 (`personalFinanceV3_2`) déclenchent l'assistant de migration.
- `sw.js` = simple cache offline, aucune donnée traitée.

## 🧪 Tests
24 tests unitaires (recherche floue, séries, wrapped) + 33 tests d'intégration de bout en bout
(onboarding → opérations → graphique → wrapped → historique → import ancien format → migration auto
→ export → thèmes → suppression), plus un test de **déploiement sous-chemin** (type GitHub Pages).
