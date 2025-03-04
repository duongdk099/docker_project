# **Documentation du Projet E-Commerce Microservices**

---

## **Table des Matières**
1. [Introduction](#introduction)
2. [Architecture du Projet](#architecture-du-projet)
   - [Vue d'Ensemble](#vue-densemble)
   - [Microservices](#microservices)
3. [Structure des Répertoires](#structure-des-répertoires)
4. [Installation et Démarrage](#installation-et-démarrage)
   - [Prérequis](#prérequis)
   - [Démarrage avec Docker Compose](#démarrage-avec-docker-compose)
   - [Démarrage Manuel](#démarrage-manuel)
5. [API Endpoints](#api-endpoints)
6. [CI/CD avec GitLab](#cicd-avec-gitlab)
7. [Bonnes Pratiques](#bonnes-pratiques)
8. [Ressources et Documentation](#ressources-et-documentation)

---

## **Introduction**

Ce projet est une **application e-commerce** basée sur une **architecture microservices**, avec une séparation claire entre le **frontend** (Vue.js) et le **backend** (Node.js/Express).  
L’application est entièrement **conteneurisée avec Docker** et inclut un pipeline **CI/CD GitLab**.

---

## **Architecture du Projet**

### **Vue d'Ensemble**
L’architecture repose sur :
- **Frontend Vue.js** : Interface utilisateur avec Vue Router et Axios.
- **Backend Node.js/Express** :
  - **Auth Service** : Gestion des utilisateurs et JWT.
  - **Product Service** : Gestion des produits et du panier.
  - **Order Service** : Gestion des commandes.
- **MongoDB** : Base de données distribuée.
- **Orchestration avec Docker et Docker Swarm** pour la production.
- **CI/CD GitLab** pour automatiser les tests et le déploiement.

### **Microservices**
1. **Auth Service** : Inscription, connexion et gestion des utilisateurs via JWT.
2. **Product Service** : Gestion des produits et panier.
3. **Order Service** : Gestion des commandes.

---

## **Structure des Répertoires**
```bash
.
├── frontend/             # Vue.js Frontend
├── services/
│   ├── auth-service/     # Authentification et JWT
│   ├── order-service/    # Gestion des commandes
│   ├── product-service/  # Produits et panier
├── scripts/              # Automatisation
├── docker-compose.yml    # Déploiement local
├── README.md             # Documentation
└── .gitlab-ci.yml        # CI/CD pipeline
```

---

## **Installation et Démarrage**

### **📌 Prérequis**
- **Docker** (v20+), **Docker Compose** (v1.27+)
- **Node.js** (v18+), **npm**
- **Git**
- **MongoDB** (installé ou via Docker)

### **🚀 Démarrage avec Docker Compose**
```sh
# 1️⃣ Cloner le projet
git clone <repo_url>
cd docker-project

# 2️⃣ Démarrer tous les services
docker-compose up --build -d

# 3️⃣ Accéder à l’application
# Frontend : http://localhost:8080
# Mongo Express UI : http://localhost:8081
```

### **🚀 Démarrage Manuel**
```sh
# 1️⃣ Démarrer MongoDB
mongod --dbpath /data/db

# 2️⃣ Lancer chaque microservice
cd services/auth-service && npm install && npm start
cd services/product-service && npm install && npm start
cd services/order-service && npm install && npm start

# 3️⃣ Lancer le frontend
cd frontend && npm install && npm run dev
```

---

## **API Endpoints**

### **🔹 Auth Service**
| Méthode | Endpoint                 | Description            |
|---------|--------------------------|------------------------|
| `POST`  | `/api/auth/register`     | Créer un compte       |
| `POST`  | `/api/auth/login`        | Connexion             |
| `GET`   | `/api/auth/profile`      | Profil utilisateur    |

### **🔹 Product Service**
| Méthode | Endpoint                  | Description         |
|---------|---------------------------|---------------------|
| `GET`   | `/api/products`           | Liste des produits |
| `POST`  | `/api/cart/add`           | Ajouter au panier  |

### **🔹 Order Service**
| Méthode | Endpoint                   | Description        |
|---------|----------------------------|--------------------|
| `POST`  | `/api/orders`              | Passer commande   |
| `GET`   | `/api/orders/user/:userId` | Historique       |

---

## **CI/CD avec GitLab**

### **🔹 Workflow du pipeline**
1. **Build & Test** : Vérification du code et tests.
2. **Build Docker** : Création des images Docker.
3. **Push vers la registry GitLab**.
4. **Déploiement automatique** si validé.

### **📌 Déclenchement du pipeline**
Chaque commit sur `main` ou `develop` déclenche **automatiquement** le pipeline :
```sh
git push origin develop
```

---

## **Bonnes Pratiques**
✅ **Docker** : Multi-stage builds, images légères  
✅ **Sécurité** : JWT pour l’auth, bcrypt pour les mots de passe  
✅ **CI/CD** : Tests et validation avant déploiement  
✅ **Monitoring** (Bonus) : Prometheus & Grafana  

---

## **Ressources et Documentation**
📖 **Docker Docs** → [https://docs.docker.com/](https://docs.docker.com/)  
📖 **GitLab CI/CD** → [https://docs.gitlab.com/](https://docs.gitlab.com/)  
📖 **MongoDB Docs** → [https://www.mongodb.com/docs/](https://www.mongodb.com/docs/)  

---

## **📌 Dernière étape : Pousser les changements**
Ajoutez et poussez votre mise à jour **README.md** :

```sh
git add README.md
git commit -m "Updated README with installation & API documentation"
git push origin <your-branch>
```