# 📱 RealTimeChatApp - Application de Messagerie en Temps Réel

Une application mobile de messagerie développée avec **React Native** et **Socket.IO**, permettant à deux utilisateurs de discuter en temps réel dans des **salles sécurisées par code**. Backend optimisé avec Node.js, Express, Redis, et déploiement via Docker, PM2 et Nginx.

---

## 🚀 Fonctionnalités

- Authentification des utilisateurs (JWT)
- Création / Rejoindre une **room sécurisée par code**
- Envoi et réception de messages en temps réel avec **Socket.IO**
- Liste des utilisateurs connectés à une room
- Interface mobile responsive avec **React Native**
- Optimisation backend : cache Redis, gestion mémoire
- Tests de charge avec **JMeter / Gatling**
- Déploiement avec Docker, PM2, Nginx

---

## 🛠️ Technologies utilisées

### Frontend
- React Native
- React Navigation
- Socket.IO Client

### Backend
- Node.js
- Express.js
- MongoDB + Mongoose
- JWT (authentification)
- Socket.IO
- Redis (cache)
- PM2 (process manager)

### Tests & Déploiement
- JMeter / Gatling (tests de performance)
- Docker / Docker Compose
- Nginx (reverse proxy)
- PM2 (gestion des processus)

---


---

## ⚙️ Installation & Lancement

### Prérequis

- Node.js
- Docker & Docker Compose
- MongoDB
- Redis

### 1. Cloner le projet

```bash
git clone https://github.com/votre-utilisateur/RealTimeChatApp.git
cd RealTimeChatApp

2. Backend
cd backend
npm install
npm run dev

3. Frontend (React Native)
cd frontend
npm install
npx expo start

4. Lancement avec Docker
docker-compose up --build

5. Lancement avec PM2 (backend uniquement)
pm2 start ecosystem.config.js
🔒 Authentification
Email / mot de passe

Token JWT (stocké localement dans l’app)

Middleware de vérification dans les routes protégées

💬 Fonctionnement des Rooms
Création ou connexion à une salle via un code aléatoire

Messages échangés uniquement entre les membres de la salle

Liste dynamique des utilisateurs connectés

📊 Tests de Performance
JMeter : test API login/register avec 100 utilisateurs

Gatling : test de charge sur Socket.IO (200 utilisateurs simultanés)

Résultats enregistrés dans /tests/results/

🧪 Exemple .env
PORT=5000
MONGO_URI=mongodb://mongo:27017/chatdb
JWT_SECRET=your_jwt_secret
REDIS_HOST=redis
REDIS_PORT=6379
