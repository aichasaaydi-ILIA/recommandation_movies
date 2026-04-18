<h1 align="center">🎬 MovieLens Recommandations IA</h1>

<p align="center">
  Moteur de recommandation de films hybride et intelligent basé sur le dataset MovieLens
</p>

<p align="center">
  <img alt="Python" src="https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img alt="Flask" src="https://img.shields.io/badge/Flask-REST%20API-000000?style=for-the-badge&logo=flask&logoColor=white">
  <img alt="React" src="https://img.shields.io/badge/React-Frontend-61DAFB?style=for-the-badge&logo=react&logoColor=black">
  <img alt="MongoDB" src="https://img.shields.io/badge/MongoDB-Database-47A248?style=for-the-badge&logo=mongodb&logoColor=white">
  <img alt="Docker" src="https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge">
</p>

---

## 📑 Table des Matières

- [Vue d'ensemble](#-vue-densemble)
- [Fonctionnalités](#-fonctionnalités)
- [Architecture & Stack Technique](#️-architecture--stack-technique)
- [Structure du Projet](#-structure-du-projet)
- [Prérequis](#-prérequis)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Lancement](#-lancement)
- [API Endpoints](#-api-endpoints)
- [Dataset MovieLens](#-dataset-movielens)
- [Déploiement](#-déploiement)
- [Contribuer](#-contribuer)
- [Licence](#-licence)

---

## 🌟 Vue d'ensemble

**MovieLens Recommandations IA** est une plateforme full-stack de recommandation cinématographique qui exploite le célèbre dataset **MovieLens**. Elle combine plusieurs algorithmes de machine learning pour fournir des suggestions personnalisées, précises et explicables à chaque utilisateur.

> **Problème résolu** : Les utilisateurs de plateformes de streaming passent en moyenne 45 minutes à chercher quoi regarder. Ce système résout ce problème en proposant des recommandations contextuelles et personnalisées, même pour les nouveaux utilisateurs (Cold Start Problem).

### Comment ça marche ?

1. **Collecte des données** : Les notes et préférences des utilisateurs sont stockées en temps réel via l'API.
2. **Calcul offline** : Un moteur hybride (filtrage collaboratif + similarité de contenu + clustering K-Means) génère des modèles de recommandation.
3. **Recommandation online** : L'API Flask sert les résultats au frontend React en temps quasi-réel.

---

## ✨ Fonctionnalités

### 🧠 Moteur de Recommandation Hybride
- **Filtrage Collaboratif** — Recommandations basées sur les utilisateurs similaires (`similarity.py`)
- **Similarité Item-Item** — Films similaires à ceux déjà appréciés
- **Clustering K-Means** — Groupes d'utilisateurs pour résoudre le Cold Start (`clustering.py`)
- **Popularité Bayésienne** — Recommandations pertinentes pour les nouveaux utilisateurs
- **IA Explicable** — Chaque recommandation est accompagnée d'une justification lisible

### 🎬 Interface Utilisateur
- **Dashboard interactif** — Films populaires, historique et recommandations personnalisées
- **Intégration vidéo** — Composants `VideoPlayerTMDB` et `MovieCardWithVideo`
- **Recherche temps réel** — Recherche instantanée dans toute la base MovieLens
- **Watchlist personnalisée** — Système de suivi des films à voir

### 🛡️ Backend Robuste
- **Authentification JWT** — Inscription, connexion et gestion de sessions sécurisées
- **25+ Endpoints RESTful** — API complète et documentée
- **Monitoring & Healthcheck** — Vérification de l'état du système en temps réel
- **Administration** — Endpoints dédiés pour la gestion de la base de données

### 🐳 Déployable partout
- Docker & Docker Compose configurés
- Compatible Heroku, AWS, Azure, GCP
- Support dev / test / production

---

## 🛠️ Architecture & Stack Technique

```
┌─────────────────────────────────────────────────────┐
│                     FRONTEND                        │
│              React + Vite + Tailwind CSS             │
└───────────────────────┬─────────────────────────────┘
                        │ HTTP / REST
┌───────────────────────▼─────────────────────────────┐
│                  BACKEND (Flask)                    │
│           REST API · JWT Auth · 25+ Routes           │
└───────┬───────────────────────────┬─────────────────┘
        │                           │
┌───────▼────────┐         ┌────────▼────────┐
│    MongoDB     │         │   ML Engine     │
│  (Données &    │         │  (Offline)      │
│  Préférences)  │         │  recommender.py │
│                │         │  clustering.py  │
│                │         │  similarity.py  │
└────────────────┘         └─────────────────┘
```

| Couche | Technologie | Rôle |
|:---|:---|:---|
| **Frontend** | React + Vite | Interface utilisateur (SPA) |
| **Styling** | Tailwind CSS | Design utilitaire et responsive |
| **Backend** | Flask (Python) | API REST et orchestration ML |
| **Machine Learning** | Python (scikit-learn) | Moteur de recommandation |
| **Base de données** | MongoDB | Stockage des films, users, ratings |
| **Auth** | JWT + bcrypt | Sécurité et gestion de sessions |
| **Conteneurisation** | Docker + Compose | Déploiement portable |

---

## 📁 Structure du Projet

```
Movielens-Recommandations_IA/
│
├── 📁 Backend/                     # Service Flask
│   ├── 📄 app.py                   # Point d'entrée principal (25+ routes)
│   ├── 📄 config.py                # Configuration (dev/test/prod)
│   ├── 📄 run.py                   # Script de démarrage
│   ├── 📄 wsgi.py                  # Entrée WSGI pour production
│   ├── 📄 healthcheck.py           # Vérification de santé
│   ├── 📄 API_ROUTES.md            # Documentation des routes
│   │
│   ├── 📁 offline/                 # Moteur ML (calculs offline)
│   │   ├── 📄 recommender.py       # 🧠 Moteur hybride principal
│   │   ├── 📄 clustering.py        # K-Means (Cold Start)
│   │   └── 📄 similarity.py        # Similarités item-item & user-user
│   │
│   ├── 📁 scripts/                 # Scripts d'administration
│   │   ├── 📄 load_movies.py       # Ingestion du dataset MovieLens
│   │   └── 📄 init_db.py           # Initialisation MongoDB
│   │
│   ├── 📁 utils/                   # Utilitaires partagés
│   │   ├── 📄 database.py          # Connexion MongoDB
│   │   ├── 📄 security.py          # JWT & hashing bcrypt
│   │   └── 📄 validators.py        # Validation et sanitisation
│   │
│   └── 📁 tests/
│       └── 📄 test_api.py          # Tests unitaires
│
├── 📁 Frontend/                    # Application React
│   ├── 📁 src/
│   │   ├── 📁 components/          # Composants réutilisables
│   │   ├── 📁 pages/               # Pages (Dashboard, Profil, Recherche)
│   │   └── 📁 api/                 # Client Axios
│   ├── 📄 vite.config.js
│   ├── 📄 tailwind.config.cjs
│   └── 📄 package.json
│
├── 📄 u.data                       # Dataset MovieLens — Ratings (100k)
├── 📄 u.item                       # Dataset MovieLens — Films
├── 📄 u.user                       # Dataset MovieLens — Utilisateurs
├── 📄 data_loader.py               # Chargeur de données utilitaire
├── 📄 install.py                   # Installation automatique
├── 📄 start.py                     # Menu de démarrage interactif
├── 📄 check_requirements.py        # Vérification des prérequis
├── 📄 docker-compose.yml           # Orchestration Docker
├── 📄 Dockerfile                   # Image Docker Backend
├── 📄 Procfile                     # Configuration Heroku
└── 📄 .env.example                 # Template des variables d'environnement
```

---

## ✅ Prérequis

| Outil | Version minimale |
|:---|:---|
| Python | 3.8+ |
| Node.js | 16.x+ |
| MongoDB | 4.4+ |
| Docker *(optionnel)* | 20.x+ |

---

## 🚀 Installation

### Option A — Installation automatique *(recommandée)*

```bash
# 1. Cloner le dépôt
git clone https://github.com/votre-user/Movielens-Recommandations_IA.git
cd Movielens-Recommandations_IA

# 2. Lancer l'installateur automatique
python install.py
```

### Option B — Installation manuelle

```bash
# 1. Cloner le dépôt
git clone https://github.com/votre-user/Movielens-Recommandations_IA.git
cd Movielens-Recommandations_IA

# 2. Backend — Environnement virtuel Python
python -m venv venv
# Windows :
venv\Scripts\activate
# Linux/macOS :
source venv/bin/activate

pip install -r Backend/requirements.txt

# 3. Frontend — Dépendances Node
cd Frontend
npm install
cd ..

# 4. Ingestion du dataset MovieLens
python Backend/scripts/load_movies.py
python Backend/scripts/init_db.py
```

### Option C — Docker

```bash
docker-compose up --build
```

---

## 🔐 Configuration

Copiez le fichier `.env.example` en `.env` et renseignez vos valeurs :

```bash
cp .env.example .env
```

| Variable | Description | Exemple |
|:---|:---|:---|
| `FLASK_ENV` | Environnement Flask | `development` |
| `SECRET_KEY` | Clé de session Flask | `votre_clé_secrète` |
| `JWT_SECRET_KEY` | Clé de signature JWT | `votre_jwt_secret` |
| `MONGO_URI` | URI MongoDB production | `mongodb+srv://...` |
| `MONGO_URI_DEV` | URI MongoDB développement | `mongodb://localhost:27017/movies_dev` |
| `FLASK_PORT` | Port de l'API | `5000` |
| `ADMIN_TOKEN` | Token admin protégé | `admin-secret-token` |
| `RECOMMENDATION_N_CLUSTERS` | Nombre de clusters K-Means | `5` |
| `REACT_APP_API_URL` | URL de l'API côté frontend | `http://localhost:5000` |

---

## ▶️ Lancement

### Démarrage rapide (menu interactif)

```bash
python start.py
```

### Démarrage manuel

```bash
# Terminal 1 — Backend Flask
python Backend/run.py

# Terminal 2 — Frontend React
cd Frontend
npm run dev
```

### Vérification de santé

```bash
python check_requirements.py        # Vérifier les prérequis
python Backend/healthcheck.py       # Vérifier l'état du système
```

L'application sera accessible à :
- **Frontend** → http://localhost:5173
- **API Backend** → http://localhost:5000
- **Health Check** → http://localhost:5000/api/health

---

## 📡 API Endpoints

| Méthode | Route | Auth | Description |
|:---|:---|:---:|:---|
| `POST` | `/api/register` | ❌ | Créer un compte utilisateur |
| `POST` | `/api/login` | ❌ | Connexion (retourne un JWT) |
| `GET` | `/api/health` | ❌ | État du système |
| `GET` | `/api/movies/popular` | ❌ | Films populaires (accès public) |
| `GET` | `/api/movies` | ✅ | Liste complète des films |
| `POST` | `/api/rate_movie` | ✅ | Soumettre une note pour un film |
| `GET` | `/api/recommendations` | ✅ | Recommandations personnalisées |

> 📄 Voir [`Backend/API_ROUTES.md`](Backend/API_ROUTES.md) pour la documentation complète des routes.

---

## 📊 Dataset MovieLens

Ce projet utilise le **MovieLens 100K Dataset** (GroupLens Research) :

| Fichier | Contenu | Taille |
|:---|:---|:---|
| `u.data` | 100 000 notes (userId, movieId, rating, timestamp) | ~2 MB |
| `u.item` | Métadonnées des 1 682 films (titre, genres, date) | ~236 KB |
| `u.user` | Profils de 943 utilisateurs (âge, sexe, profession) | ~23 KB |

---

## 🐳 Déploiement

### Docker Compose (recommandé)

```bash
docker-compose up -d
# Initialiser la base :
docker-compose exec backend python scripts/init_db.py
```

### Heroku

```bash
heroku create votre-app
heroku config:set $(cat .env | xargs)
git push heroku main
```

### Autres plateformes

Le projet est compatible avec **AWS**, **Azure**, **GCP** et tout hébergeur supportant Docker.  
Consultez [`DEPLOYMENT.md`](DEPLOYMENT.md) pour les guides détaillés par plateforme.

---

## 📚 Documentation

| Document | Description |
|:---|:---|
| [`QUICKSTART.md`](QUICKSTART.md) | Démarrer en 5 minutes |
| [`INSTALLATION.md`](INSTALLATION.md) | Installation détaillée & troubleshooting |
| [`DEPLOYMENT.md`](DEPLOYMENT.md) | Déploiement sur Heroku, AWS, Azure, Docker |
| [`Backend/API_ROUTES.md`](Backend/API_ROUTES.md) | Référence complète de l'API |
| [`PROJECT_STATUS.md`](PROJECT_STATUS.md) | État et avancement du projet |

---

## 🤝 Contribuer

Les contributions sont les bienvenues !

```bash
# 1. Forker le dépôt
# 2. Créer une branche
git checkout -b feature/ma-fonctionnalite

# 3. Commiter vos changements
git commit -m "feat: ajout de ma fonctionnalité"

# 4. Pousser la branche
git push origin feature/ma-fonctionnalite

# 5. Ouvrir une Pull Request
```

---

## 📄 Licence

Ce projet est distribué sous licence **MIT**. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

<p align="center">
  Fait avec ❤️ — Projet ILIA · MovieLens Recommandations IA
</p>
