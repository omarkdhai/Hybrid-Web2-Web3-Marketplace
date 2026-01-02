# Marketplace E-commerce Hybride Web2/Web3

Ce projet, réalisé dans le cadre d'un Projet de Fin d'Études, présente la conception et l'implémentation d'une marketplace e-commerce moderne et hybride. Il fusionne l'expérience utilisateur simple et accessible des applications Web2 avec les garanties de confiance et de transparence offertes par les technologies Web3 telles que la blockchain et la signature électronique.

L'innovation centrale réside dans un système où un paiement standard en monnaie fiduciaire (via **Stripe**) déclenche un enregistrement immuable et vérifiable de la commande sur une blockchain compatible Ethereum, grâce à un **Oracle** développé sur mesure.

---

## ✨ Fonctionnalités

### Pour le Client (Acheteur)
- **Expérience E-commerce Classique :** Parcourir les produits, gérer un panier, consulter l'historique des commandes.
- **Paiements Fiduciaires Sécurisés :** Payer simplement et en toute sécurité par carte bancaire avec Stripe.
- **Confiance et Transparence Accrues :**
    - **Signature Électronique :** Signer cryptographiquement l'intention de commande avec un portefeuille **Metamask** avant le paiement pour garantir la non-répudiation.
    - **Suivi de Commande On-Chain :** Visualiser le statut immuable de la commande (`Payée`, `Expédiée`, `Complétée`) tel qu'il est enregistré sur la blockchain.
    - **Gestion des Litiges :** Ouvrir un litige sur une commande, dont le statut est également enregistré et résolu on-chain.
- **Notifications en Temps Réel :** Recevoir des mises à jour instantanées via WebSockets.
- **Système de Support :** Contacter l'administrateur via un système de tickets.

### Pour l'Administrateur (Vendeur)
- **Gestion Complète des Produits :** Fonctionnalités CRUD (Créer, Lire, Mettre à jour, Supprimer) pour le catalogue.
- **Gestion des Commandes :** Visualiser toutes les commandes et gérer leur cycle de vie.
- **Actions On-Chain :** Marquer une commande comme "Expédiée" en signant une transaction avec un portefeuille.
- **Résolution des Litiges :** Examiner les litiges des clients et enregistrer la décision finale sur la blockchain.
- **Tableau de Bord Analytique :** Visualiser des indicateurs clés (revenus, ventes par catégorie, etc.).

---

## 🏛️ Architecture Globale

Ce projet est construit sur une **architecture microservices**, conteneurisée avec Docker et unifiée derrière une API Gateway. Cette approche garantit la scalabilité, la maintenabilité et une séparation claire des responsabilités.

- **Frontend :** Deux Single Page Applications développées avec **Angular** (une pour les clients, une pour l'admin).
- **Backend :** Une suite de microservices développés avec **Quarkus (Java)**.
    - `auth-service`: Gère l'identité et les accès avec **Keycloak**.
    - `product-service`: Gère le catalogue, les commandes et agit en tant qu'**Oracle**.
    - `payment-service`: Isole toute la communication avec l'API **Stripe**.
    - `notification-service`: Gère les connexions **WebSocket** en temps réel.
    - `support-service`: Gère le système de tickets du support client.
- **Blockchain :**
    - Un smart contract `OrderStatusTracker` écrit en **Solidity**.
    - **Hardhat** utilisé comme environnement de développement et de test.
- **Infrastructure :**
    - **Docker & Docker Compose :** Pour la conteneurisation et l'orchestration locale.
    - **Kong API Gateway :** Agit comme point d'entrée unique et sécurisé pour toutes les requêtes API.
    - **Bases de Données :** **MongoDB** pour les données applicatives et **PostgreSQL** pour Keycloak.

---

## 🛠️ Stack Technologique

- **Frontend :** Angular, TypeScript, Ethers.js
- **Backend :** Quarkus (Java)
- **Blockchain :** Solidity, Hardhat, Web3j
- **Bases de Données :** MongoDB, PostgreSQL
- **Identité :** Keycloak
- **Paiement :** Stripe
- **Infrastructure & DevOps :** Docker, Docker Compose, Kong API Gateway
- **Outils :** Postman, Stripe CLI, IntelliJ IDEA, Visual Studio Code

---

## 🚀 Démarrage Rapide

Pour exécuter ce projet en local, vous devez avoir Docker et Docker Compose installés.

### 1. Cloner le Dépôt
```bash
git clone https://github.com/votre-nom-utilisateur/votre-repo.git
cd votre-repo
```

### 2. Configuration de l'Environnement
Avant de lancer, vous devez configurer vos variables d'environnement. Copiez le fichier .env.example en .env dans chaque répertoire de microservice et remplissez les secrets et configurations requis (clés Stripe, paramètres Keycloak, etc.).
Des instructions plus détaillées pour configurer les realms Keycloak et les webhooks Stripe se trouvent dans le dossier /docs.

### 3. Lancer l'Application
Exécutez l'écosystème complet avec une seule commande :
```bash
docker-compose up --build
```
Cette commande va :
Construire les images Docker pour tous les microservices et frontends.
Démarrer tous les conteneurs (bases de données, Keycloak, Kong, services backend, etc.).
Le nœud Hardhat démarrera, et le script de déploiement déploiera automatiquement le smart contract.

### 4. Accéder à l'Application
Une fois tous les services en cours d'exécution :

Frontend Client : http://localhost:4201

Frontend Admin : http://localhost:4202

Console d'Administration Keycloak : http://localhost:8180

API d'Administration Kong : http://localhost:8001

Dozzle (pour visualiser les logs) : http://localhost:9999

## 👤 Auteur
Omar KOUDHAI

LinkedIn : linkedin.com/in/omar-koudhai

Email : omarkdhai@gmail.com
