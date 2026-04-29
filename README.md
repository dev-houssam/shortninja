# ShortNinja

An app for wiewing short made in Ocaml Web framework, let Eliom.


Voici un README professionnel pour **ShortNinja**, en partant de ta description (application de visualisation de courts-métrages, framework OCaml Eliom).

---

# ShortNinja 🎬

**ShortNinja** est une application web légère et rapide dédiée à la visualisation de **courts-métrages** (shorts).  
Construite avec **OCaml** et le framework web **Eliom**, elle offre des performances élevées, une sécurité de typage forte, et une expérience utilisateur fluide.

---

## ✨ Fonctionnalités principales

- **Catalogue de courts-métrages** : parcourez une collection organisée (durée < 20 min).
- **Lecteur vidéo intégré** : support MP4, WebM, HLS.
- **Tags & filtres** : par genre (comédie, drame, animation, SF, etc.), durée, popularité.
- **Système de "favoris"** (compte utilisateur optionnel).
- **Mode spectateur** : pas d'inscription requise pour visionner.
- **Profil Uploader** (backoffice simple) : pour les cinéastes (gestion de leurs courts).
- **API publique** (JSON/REST) pour récupérer la liste des courts (utile pour embarquement externe).

> *Typiquement conçu pour une cinémathèque indépendante, un festival en ligne, ou un portfolio de jeunes réalisateurs.*

---

## 🛠 Stack technique

| Composant          | Technologie                         |
|--------------------|-------------------------------------|
| Langage            | OCaml                               |
| Framework web      | **Eliom** (OCaml – côté serveur + client) |
| Syntaxe HTML/CSS   | TyXML / Bootstrap 5 (via Eliom)     |
| Base de données    | PostgreSQL (via `pgocaml` ou `caqti`) |
| Sessions & cookies | Eliom native                        |
| Vidéo              | HTML5 video + adaptation mobile     |

---

## 📦 Installation (développement local)

### Prérequis

- OCaml (>= 4.14) avec OPAM
- Node.js & `npm` (pour assets CSS/JS si besoin)
- PostgreSQL (>= 13)
- `make`

### Étapes

```bash
# 1. Cloner le dépôt
git clone https://github.com/toncompte/shortninja
cd shortninja

# 2. Installer les dépendances OCaml
opam switch create . 4.14.1
opam install . --deps-only

# 3. Initialiser la base de données
createdb shortninja_dev
psql -d shortninja_dev -f sql/schema.sql

# 4. Configurer les variables d'environnement
cp .env.example .env
# éditer .env (DATABASE_URL, COOKIE_SECRET, etc.)

# 5. Lancer le serveur Eliom
make serve
```

L'application sera disponible sur `http://localhost:8080`

---

## 🧭 Utilisation (quick start)

### En tant que spectateur :
1. Accédez à l'accueil → liste des courts par date d'ajout.
2. Cliquez sur un court → page de lecture.
3. Commentez / likez (sans compte : pseudo éphémère).

### En tant que réalisateur (uploader) :
1. Créez un compte avec rôle "Créateur".
2. Allez dans votre espace → "Ajouter un court".
3. Fournissez : titre, description, fichier vidéo (max 500 Mo), miniature.
4. Après validation (modération automatique basique), le court est publié.

### En tant qu'admin :
- Validez/supprimez les courts signalés.
- Générez des codes d’accès API.

---

## 🔌 API publique (exemple)

```http
GET /api/v1/shorts
    ?genre=animation
    &limit=10
    &offset=20
```

Réponse :
```json
{
  "shorts": [
    {
      "id": 42,
      "title": "Le dernier café",
      "duration_sec": 480,
      "thumbnail_url": "/static/thumb/42.jpg",
      "video_url": "/stream/42"
    }
  ],
  "total": 157
}
```

> Authentification API par clé (X-API-Key) pour les apps tierces.

---

## 🧪 Tests

```bash
make test
```

Les tests unitaires et d'intégration couvrent :
- Modèles de données
- Routes Eliom
- Validation de sessions

---

## 🚀 Déploiement (production)

Nous recommandons :

- Serveur : **Linux** (Ubuntu 22.04)
- Reverse proxy : **nginx** (avec TLS)
- Process manager : **systemd** pour le binaire Eliom
- Base de données : PostgreSQL avec réplication si besoin
- Stockage vidéo : CDN (CloudFront ou équivalent) ou disque local + caching

Exemple de service systemd :

```ini
[Service]
ExecStart=/home/deploy/shortninja/_build/default/server.exe
EnvironmentFile=/home/deploy/shortninja/.env
Restart=always
User=deploy
```

---

## 🤝 Contribuer

Les PRs sont les bienvenues, surtout pour :
- Améliorations du lecteur vidéo (accessibilité)
- Support de sous-titres
- Traductions (i18n)

Merci de suivre `ocamlformat` et d’ajouter des tests.

---

## 📜 Licence

**AGPL-3.0** – Code ouvert.  
*(Le contenu vidéo appartient à ses auteurs respectifs.)*

---

## 📬 Contact & communauté

- Créateur : [@tonhandle]  
- Signalement de bugs : [Issues GitHub]  
- Chat OCaml : [Discord Eliom](https://discord.gg/ocaml)

---

**ShortNinja – La puissance d’OCaml au service des courts-métrages.**
