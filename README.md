<div align="center">

# 🤖 Systèmes Distribués Agentiques & Microservices

**Un écosystème intelligent alliant Spring Cloud, Spring AI et le protocole MCP**

[![Java](https://img.shields.io/badge/Java-17%2B-orange?style=for-the-badge&logo=java)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-brightgreen?style=for-the-badge&logo=spring-boot)](https://spring.io/projects/spring-boot)
[![Spring AI](https://img.shields.io/badge/Spring_AI-MCP_Enabled-blue?style=for-the-badge&logo=spring)](https://spring.io/projects/spring-ai)
[![OpenAI](https://img.shields.io/badge/OpenAI-API-412991?style=for-the-badge&logo=openai)](https://openai.com/)

*Développé par **Hasnae Amchich***

[📺 Présentation Générale](https://www.youtube.com/watch?v=ua5XHtSPI3Y) • [🎬 Démo Partie 1](https://www.youtube.com/watch?v=cdFz3VemT1Q) • [🎬 Démo Partie 2](https://www.youtube.com/watch?v=JHvxSZTWSsY)

</div>

---

## 📌 À propos du projet

Ce dépôt contient l'implémentation complète d'une architecture **Microservices résiliente** connectée à un **Agent IA conversationnel**. Grâce au standard **MCP (Model Context Protocol)**, l'agent est capable d'invoquer dynamiquement les opérations métier des microservices bancaires et clients depuis plusieurs interfaces (REST, Telegram, Discord, WhatsApp).

> ### 🔐 Avertissement de Sécurité
> Conformément aux bonnes pratiques de sécurité, **aucune clé secrète n'est exposée dans ce dépôt**.  
> Les tokens d'authentification pour **WhatsApp**, **Telegram**, **Discord** ainsi que la clé d'API **OpenAI** ont été **volontairement vidés** dans les fichiers de configuration. Vous devrez renseigner vos propres identifiants pour lancer l'application.

---

## 🧭 Vue d'ensemble de l'Architecture

```text
+-------------------+      +-------------------+      +-------------------+
|   Client REST     |      |   Bot Telegram    |      |   Bot Discord     |
+---------+---------+      +---------+---------+      +---------+---------+
          |                          |                          |
          +--------------------------+--------------------------+
                                     |
                                     v
                     +-------------------------------+
                     |    AI Agent Service (Spring)  |
                     |      [ OpenAI + Client ]      |
                     +---------------+---------------+
                                     |  Protocole MCP
                                     v
                     +-------------------------------+
                     |       API Gateway (Cloud)     |
                     +-------+---------------+-------+
                             |               |
            +----------------+               +----------------+
            v                                                 v
+-----------------------+                         +-----------------------+
|   Customer-Service    | <--- OpenFeign / ---> |    EBank-Service      |
|  (Gestion Clients)    |     Resilience4J        |  (Gestion Comptes)    |
+-----------+-----------+                         +-----------+-----------+
            |                                                 |
            +------------------------+------------------------+
                                     v
                     +-------------------------------+
                     |  Discovery Service (Eureka)   |
                     +-------------------------------+
```

---

## 🚀 Feuille de Route & Réalisations

### Phase 1 : Fondations Microservices & Résilience
*Développement de l'infrastructure distribuée sous Spring Cloud ([Voir la vidéo](https://www.youtube.com/watch?v=cdFz3VemT1Q))*

| Composant / Fonctionnalité | Technologie | Description |
| :--- | :--- | :--- |
| **Customer-Service** | Spring Boot / JPA | Microservice dédié à la gestion des données clients. |
| **EBank-Service** | Spring Boot / JPA | Microservice gérant les comptes et opérations bancaires. |
| **Communication Synchrone** | **OpenFeign** | Appels déclaratifs fluides entre `EBank-Service` et `Customer-Service`. |
| **Tolérance aux Pannes** | **Resilience4J** | Protection des appels inter-services via le pattern *Circuit Breaker*. |
| **Routage Centralisé** | **Spring Cloud Gateway** | Point d'entrée unique assurant le routage dynamique vers les services. |
| **Annuaire de Services** | **Eureka Discovery** | Enregistrement et découverte automatique des instances de microservices. |
| **Validation API** | **Postman & Swagger-UI** | Documentation interactive et tests fonctionnels des endpoints REST. |

### Phase 2 : Intelligence Artificielle Agentique & MCP
*Intégration de l'Agent IA et exposition des outils métier ([Voir la vidéo](https://www.youtube.com/watch?v=JHvxSZTWSsY))*

* 🧠 **Agent IA avec Spring AI :** Création d'un assistant intelligent capable de comprendre les requêtes en langage naturel.
* 🔌 **Exposition via MCP (Model Context Protocol) :** Transformation des fonctionnalités des microservices en outils (*Tools*) exploitables par un modèle de langage.
* 🧪 **Validation MCP Client :** Tests unitaires et fonctionnels des outils exposés via un client MCP dédié.
* 🔗 **Orchestration Chatbot :** Liaison directe entre le moteur conversationnel et les microservices via MCP.
* 💬 **Déploiement Multi-Canaux :**
  * ✅ Validation via **Client REST**
  * ✅ Interfaçage avec **Telegram**
  * ✅ Interfaçage avec **Discord**
  * ✅ Pré-configuration pour **WhatsApp**

---

## 🛠️ Guide d'Installation Rapide

### 1. Récupération du code source
```bash
git clone https://github.com/<votre-username>/<nom-du-projet>.git
cd <nom-du-projet>
```

### 2. Paramétrage des variables sensibles
Avant de démarrer les services, éditez le fichier `application.properties` (ou `application.yml`) du module Agent IA afin d'y insérer vos clés personnelles :

```properties
# Clé API LLM
spring.ai.openai.api-key=

# Tokens des plateformes de messagerie (laissés vides par sécurité)
telegram.bot.token=
discord.bot.token=
whatsapp.api.token=
```

### 3. Séquence d'exécution
Lancez les modules dans l'ordre suivant pour garantir le bon enregistrement des services :
1. **Discovery-Service** *(Serveur Eureka)*
2. **Gateway-Service** *(API Gateway)*
3. **Customer-Service** & **EBank-Service** *(Services Métier)*
4. **AI-Agent-Service** *(Agent Spring AI & Serveur/Client MCP)*

---

## 👩‍💻 Auteure

**Hasnae Amchich**  
*Projet réalisé dans le cadre de l'étude des Systèmes Distribués Agentiques et des architectures Microservices.*
