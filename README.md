<h1 align="center"> recommandation movielens </h1>

<p align="center"> An Intelligent, Multi-Model Hybrid Recommendation Engine for Personalized Cinema Exploration </p>

<p align="center">
  <img alt="Build" src="https://img.shields.io/badge/Build-Passing-brightgreen?style=for-the-badge">
  <img alt="Issues" src="https://img.shields.io/badge/Issues-0%20Open-blue?style=for-the-badge">
  <img alt="Contributions" src="https://img.shields.io/badge/Contributions-Welcome-orange?style=for-the-badge">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge">
</p>
<!-- 
  **Note:** These are static placeholder badges. Replace them with your project's actual badges.
  You can generate your own at https://shields.io
-->

## 📑 Table of Contents
- [Overview](#-overview)
- [Key Features](#-key-features)
- [Tech Stack & Architecture](#-tech-stack--architecture)
- [Project Structure](#-project-structure)
- [Environment Variables](#-environment-variables)
- [API Keys Setup](#-api-keys-setup)
- [Getting Started](#-getting-started)
- [Usage](#-usage)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌟 Overview

**recommandation movielens** is a sophisticated, full-stack predictive analytics platform designed to solve the "Paradox of Choice" in digital cinema. By leveraging the industry-standard MovieLens dataset, the system provides users with a seamless, highly personalized discovery interface that evolves based on individual preferences and community behavior.

> In the modern era of streaming, users spend an average of 45 minutes simply searching for content to watch. Generic "Top 10" lists fail to capture individual nuances, leading to decision fatigue and decreased user engagement. Current recommendation systems often suffer from the "Cold Start" problem for new users and fail to provide transparent explanations for why a specific movie was suggested.

The solution is a comprehensive **Hybrid Recommendation Engine** that merges collaborative filtering, content-based analysis, and K-Means clustering. This ensures that whether you are a first-time visitor or a long-term cinephile, the platform delivers accurate, context-aware suggestions. Built on a robust **Microservices Architecture** with a **React-driven Frontend** and a **Flask-powered REST API**, the system ensures high availability, scalability, and sub-second response times for complex recommendation calculations.

---

## ✨ Key Features

### 🧠 Advanced Hybrid Recommendation Engine
- **Intelligent Personalization:** Utilizes `HybridRecommender` to combine item-to-item similarity and user-to-user collaborative filtering for pinpoint accuracy.
- **New User Onboarding:** Employs Bayesian popularity calculations and K-Means clustering (`clustering.py`) to solve the cold-start problem, providing immediate value to first-time users.
- **Content-Aware Discovery:** Analyzes movie metadata and genres to suggest films similar to those you already love.
- **Explainable AI:** Generates human-readable explanations for recommendations, building trust and transparency with the user.

### 🎬 Immersive User Experience
- **Interactive Dashboard:** A centralized hub built with React that displays popular trends, personalized picks, and your viewing history.
- **Dynamic Media Integration:** Features specialized components like `VideoPlayerTMDB` and `MovieCardWithVideo` for a rich, visual browsing experience.
- **Real-time Search:** Instantly find films across the entire MovieLens database using high-performance search endpoints.
- **Personalized Watchlists:** Manage your future viewing plans with a dedicated tracking system.

### 🛡️ Secure & Scalable Backend
- **Robust Authentication:** Secure user registration and login powered by JWT (JSON Web Tokens) and industry-standard password hashing.
- **Automated Data Pipelines:** Includes `data_loader.py` and `load_movies.py` for seamless ingestion of large-scale movie datasets.
- **System Health Monitoring:** Integrated health check endpoints ensure high reliability and easy maintenance in production environments.
- **Admin Control Center:** Specialized scripts for database cleanup, offline computation triggers, and global statistics monitoring.

---

## 🛠️ Tech Stack & Architecture

### Architecture Pattern
The project follows a **Microservices-inspired architecture** with a clear separation between the **Recommender Engine (Offline Calculations)**, the **RESTful API Service (Online Service)**, and the **Component-based Frontend**.

| Layer | Technology | Purpose | Why it was Chosen |
| :--- | :--- | :--- | :--- |
| **Frontend** | React | User Interface | Component-based reusability and efficient DOM updates for dynamic movie grids. |
| **Backend** | Flask | API & Logic | Lightweight and extensible, ideal for serving Machine Learning models via REST. |
| **Styling** | Tailwind CSS | Visual Design | Rapid UI development with a utility-first approach for responsive layouts. |
| **ML/Computation** | Python | Intelligence | Native support for advanced mathematical operations and data processing. |
| **Database** | MongoDB | Data Persistence | Flexible document storage perfect for varied movie metadata and user preference profiles. |
| **Containerization**| Docker | Deployment | Ensures environment parity between development and production. |
| **Build Tool** | Vite | Frontend Tooling | Extremely fast hot-module replacement and optimized production builds. |

---

## 📁 Project Structure

```
fatimamellouki-Movies-IA-2dc0343/
├── 📁 Backend/                 # Flask Backend Services
│   ├── 📁 offline/             # ML Recommendation Core
│   │   ├── 📄 recommender.py   # Hybrid engine logic
│   │   ├── 📄 clustering.py    # K-Means user grouping
│   │   └── 📄 similarity.py    # Item-item & User-user similarity
│   ├── 📁 scripts/             # Admin & Initialization scripts
│   │   ├── 📄 load_movies.py   # Data ingestion
│   │   └── 📄 init_db.py       # Database bootstrapping
│   ├── 📁 utils/               # Shared utilities
│   │   ├── 📄 database.py      # MongoDB connection management
│   │   ├── 📄 security.py      # JWT & Hashing logic
│   │   └── 📄 validators.py    # Input data sanitization
│   ├── 📄 app.py               # Main API Entry Point
│   ├── 📄 config.py            # Environment configurations
│   └── 📄 run.py               # Backend startup script
├── 📁 Frontend/                # React Frontend Application
│   ├── 📁 src/                 # Application source
│   │   ├── 📁 components/      # UI Components (VideoPlayer, MovieCard)
│   │   ├── 📁 pages/           # View Logic (Dashboard, Profile, Search)
│   │   ├── 📁 api/             # Axios client configurations
│   │   └── 📄 main.jsx         # Frontend entry point
│   ├── 📄 vite.config.js       # Vite configuration
│   └── 📄 tailwind.config.cjs  # Styling rules
├── 📄 docker-compose.yml       # Orchestration for App & DB
├── 📄 data_loader.py           # Dataset processing utility
├── 📄 u.data                   # MovieLens Rating Data
├── 📄 u.item                   # MovieLens Movie Metadata
├── 📄 u.user                   # MovieLens User Metadata
├── 📄 .env.example             # Configuration template
└── 📄 README.md                # Project documentation
```

---

## 🔐 Environment Variables

The application requires several environment variables to function correctly. These should be defined in a `.env` file in the root directory.

| Variable | Description | Default/Example |
| :--- | :--- | :--- |
| `FLASK_APP` | Entry point for the Flask server | `Backend/app.py` |
| `FLASK_ENV` | Development or Production mode | `development` |
| `SECRET_KEY` | Key for session encryption | `your_secret_key_here` |
| `JWT_SECRET_KEY`| Key for signing JWT tokens | `jwt_secret_token` |
| `MONGO_URI` | Production MongoDB connection string | `mongodb://localhost:27017/movies` |
| `MONGO_URI_DEV` | Development MongoDB string | `mongodb://localhost:27017/movies_dev` |
| `FLASK_HOST` | Host for the API server | `0.0.0.0` |
| `FLASK_PORT` | Port for the API server | `5000` |
| `ADMIN_TOKEN` | Token for admin-only endpoints | `admin_super_secret` |

---

## 🔑 API Keys Setup

### Database Integration
1. **MongoDB Setup:** Ensure you have a MongoDB instance running locally or via a cloud provider like MongoDB Atlas.
2. **Connection:** Update the `MONGO_URI` in your `.env` file to point to your instance.
3. **Initialization:** Run the `Backend/scripts/init_db.py` script to create the necessary indexes and collections required for high-speed recommendation queries.

---

## 🚀 Getting Started

### Prerequisites
- **Python:** 3.8 or higher
- **Node.js:** 16.x or higher
- **Docker:** (Optional) For containerized deployment
- **MongoDB:** 4.4+ 

### Installation Steps

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/fatimamellouki/Movies-IA.git
   cd fatimamellouki-Movies-IA-2dc0343
   ```

2. **Backend Setup:**
   ```bash
   # Create and activate virtual environment
   python -m venv venv
   source venv/bin/activate # On Windows: venv\Scripts\activate

   # Install dependencies
   pip install -r requirements.txt # Note: Use install.py for automated setup
   python install.py
   ```

3. **Frontend Setup:**
   ```bash
   cd Frontend
   npm install
   ```

4. **Data Ingestion:**
   ```bash
   python Backend/scripts/load_movies.py
   python Backend/scripts/init_db.py
   ```

---

## 🔧 Usage

### Running the Application

**Option A: Using Docker (Recommended)**
```bash
docker-compose up --build
```

**Option B: Manual Execution**
1. **Start Backend:**
   ```bash
   python Backend/run.py
   ```
2. **Start Frontend:**
   ```bash
   cd Frontend
   npm run dev
   ```

### Core API Endpoints

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/register` | Create a new user account |
| `POST` | `/api/login` | Authenticate and receive JWT |
| `GET` | `/api/movies/popular` | Retrieve high-rated films (Anonymous access) |
| `GET` | `/api/movies` | Get full movie listing (Authenticated) |
| `GET` | `/api/health` | System status and database connectivity |
| `POST` | `/api/rate_movie` | Submit a rating for a film |
| `GET` | `/api/recommendations` | Fetch personalized hybrid recommendations |

