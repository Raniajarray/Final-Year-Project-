# 🛡️ Plateforme DevSecOps Intelligente

### Détection d’anomalies applicatives et automatisation des alertes par l'Intelligence Artificielle

> **Projet de Fin d'Études (PFE) — 2025/2026**
> 
> Plateforme DevSecOps intégrant la sécurité dans le cycle CI/CD, la supervision applicative, la détection d'anomalies et un assistant SOC intelligent basé sur l'IA.

---

## 📌 Table des Matières

- [Vue d'ensemble](#-vue-densemble)
- [Objectifs](#-objectifs)
- [Architecture Technique](#️-architecture-technique)
- [Pipeline DevSecOps](#-pipeline-devsecops)
- [Sécurité du Pipeline](#-sécurité-du-pipeline)
- [Observabilité et Détection d'Anomalies](#-observabilité-et-détection-danomalies)
- [Assistant SOC Intelligent](#-assistant-soc-intelligent)
- [Automatisation des Alertes](#-automatisation-des-alertes)
- [Stack Technologique](#-stack-technologique)
- [Fonctionnalités Clés](#-fonctionnalités-clés)
- [Structure du Projet](#-structure-du-projet)
- [Installation & Lancement](#-installation--lancement)
- [Résultats](#-résultats)
- [Perspectives](#-perspectives)
- [Auteur](#-auteur)

---

## 🎯 Vue d'ensemble

Cette plateforme a été développée dans le cadre d'un **Projet de Fin d'Études** avec pour objectif de mettre en place une chaîne **DevSecOps intelligente**, permettant d'intégrer automatiquement la sécurité dans le cycle de développement tout en assurant la supervision des applications et la détection d'anomalies.

La solution combine :

- 🔄 **CI/CD** pour automatiser le cycle de livraison
- 🔐 **DevSecOps** pour intégrer plusieurs contrôles de sécurité
- 📊 **Observabilité** pour surveiller les applications et les infrastructures
- 🚨 **Détection d'anomalies** basée sur l'analyse des logs
- 🤖 **Intelligence Artificielle** pour assister l'analyse des incidents
- 🧠 **RAG** pour exploiter des connaissances de cybersécurité
- ⚡ **Automatisation des alertes** et du traitement des incidents

---

## ❓ Problématique

Les applications modernes génèrent un volume important de données, de logs et d'événements de sécurité.

Une surveillance manuelle de ces événements peut rendre difficile :

- l'identification rapide des comportements anormaux ;
- la corrélation de plusieurs événements ;
- l'analyse des incidents ;
- la priorisation des alertes ;
- la réaction rapide face aux menaces.

L'objectif est donc de proposer une plateforme capable de **sécuriser le cycle de développement**, **surveiller les applications** et **assister les analystes SOC dans l'analyse des événements**.

---

## 💡 Solution proposée

La plateforme repose sur plusieurs composants complémentaires :

```text
                    ┌──────────────────────────┐
                    │      Développeur         │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │       GitLab CI/CD       │
                    └────────────┬─────────────┘
                                 │
             ┌───────────────────┼───────────────────┐
             ▼                   ▼                   ▼
        ┌─────────┐        ┌────────────┐      ┌─────────┐
        │  SAST   │        │    SCA     │      │ Secrets │
        │SonarQube│        │ OWASP /    │      │Gitleaks │
        │         │        │ npm audit  │      │         │
        └─────────┘        └────────────┘      └─────────┘
             │                   │                   │
             └───────────────────┼───────────────────┘
                                 ▼
                    ┌──────────────────────────┐
                    │   Build & Docker Image   │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │   Security Containers    │
                    │         Trivy            │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │       Staging            │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │        OWASP ZAP         │
                    │          DAST             │
                    └────────────┬─────────────┘
                                 │
                                 ▼
                    ┌──────────────────────────┐
                    │     Application          │
                    └────────────┬─────────────┘
                                 │
                    ┌────────────┴─────────────┐
                    ▼                          ▼
             ┌─────────────┐            ┌─────────────┐
             │ Prometheus  │            │   Filebeat  │
             │ / Grafana   │            │             │
             └─────────────┘            └──────┬──────┘
                                               │
                                               ▼
                                      ┌─────────────────┐
                                      │   OpenSearch    │
                                      │ Logs + Anomaly  │
                                      │    Detection    │
                                      └────────┬────────┘
                                               │
                                               ▼
                                      ┌─────────────────┐
                                      │   SOC Assistant │
                                      │ FastAPI + RAG   │
                                      │ Mistral / Ollama│
                                      └────────┬────────┘
                                               │
                              ┌────────────────┼────────────────┐
                              ▼                ▼                ▼
                         Risk Score        n8n        Slack Alerts
🔄 Pipeline DevSecOps

Le pipeline CI/CD automatise les différentes étapes nécessaires à la construction, au test et à la sécurisation de l'application.

Étapes principales
Code
 │
 ▼
Build
 │
 ▼
Tests
 │
 ▼
SAST
 │
 ▼
SCA
 │
 ▼
Secret Detection
 │
 ▼
Container Security
 │
 ▼
Infrastructure Security
 │
 ▼
Staging
 │
 ▼
DAST
 │
 ▼
Registry
🔐 Sécurité du Pipeline

Plusieurs contrôles de sécurité sont intégrés directement dans le pipeline CI/CD.

Contrôle	Outil	Objectif
SAST	SonarQube	Analyse statique du code
SCA	OWASP Dependency-Check	Détection des dépendances vulnérables
SCA	npm audit	Analyse des dépendances frontend
Container Security	Trivy	Analyse des images Docker
Secrets	Gitleaks	Détection des secrets exposés
IaC Security	Checkov	Analyse de la configuration IaC
DAST	OWASP ZAP	Tests dynamiques de sécurité
🔎 Quality Gates

Les principaux objectifs du pipeline sont notamment :

Security Rating : A
Aucun problème Blocker / High critique accepté
Vérification des Security Hotspots
Couverture de tests ≥ 50 %
Duplication du code < 15 %
📊 Observabilité et Détection d'Anomalies

La plateforme utilise une architecture d'observabilité permettant de centraliser les métriques et les logs.

Monitoring

Prometheus collecte les métriques tandis que Grafana permet leur visualisation.

Centralisation des logs

Les logs applicatifs sont collectés avec Filebeat puis centralisés dans OpenSearch.

Application
     │
     ▼
   Logs
     │
     ▼
  Filebeat
     │
     ▼
 OpenSearch
     │
     ├──────────────► Recherche & Analyse
     │
     └──────────────► Anomaly Detection

La plateforme a permis de centraliser plusieurs millions d'événements pour l'analyse et la détection des comportements anormaux.

🚨 Détection d'Anomalies

Le moteur OpenSearch Anomaly Detection utilise l'algorithme Random Cut Forest (RCF).

Configuration utilisée dans le projet :

Paramètre	Valeur
Window size	128
Shingle size	8
Anomaly grade threshold	0.7

Le système analyse l'évolution des événements afin d'identifier des comportements qui s'écartent du comportement habituel.

🤖 Assistant SOC Intelligent

La plateforme intègre un assistant SOC développé avec FastAPI.

Son rôle est d'assister l'analyste dans :

l'analyse des logs ;
l'identification des types d'événements ;
l'évaluation du niveau de risque ;
la recherche d'informations de cybersécurité ;
la corrélation d'événements ;
la génération d'une réponse contextualisée.
Architecture
                  SOC Web Interface
                         │
                         ▼
                    FastAPI
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
     Intent/NLU      Log Analyzer    Risk Scorer
          │              │              │
          └──────────────┼──────────────┘
                         ▼
                  Rules Engine
                         │
             ┌───────────┴───────────┐
             ▼                       ▼
        OpenSearch                  RAG
        Logs / Data            MITRE ATT&CK
             │                       │
             └───────────┬───────────┘
                         ▼
                    Mistral LLM
                      Ollama
                         │
                         ▼
                  Analyse / Réponse
                         │
                         ▼
                    Risk Score
                         │
                         ▼
                  n8n / Slack
🧠 Intelligence Artificielle & RAG

L'assistant utilise un modèle Mistral exécuté localement avec Ollama.

La solution utilise également une approche Retrieval-Augmented Generation (RAG) permettant d'enrichir les réponses du modèle avec une base de connaissances de cybersécurité.

Base de connaissances

La base soc_knowledge contient notamment :

connaissances MITRE ATT&CK ;
procédures d'analyse ;
playbooks SOC ;
informations utiles à l'investigation.

Les documents sont transformés en embeddings puis stockés dans OpenSearch.

🧩 Analyse des intentions

Le chatbot dispose d'un module de classification des intentions permettant d'identifier le type de demande de l'analyste.

Exemples :

Question analyste
       │
       ▼
 Intent Classifier
       │
       ├── Analyse de log
       ├── Threat Intelligence
       ├── Incident
       ├── Recherche
       └── Autre

L'analyse combine notamment :

règles ;
expressions régulières ;
NLU ;
classification ;
recherche RAG ;
LLM.
⚠️ Risk Scoring

Chaque événement analysé peut recevoir un score de risque.

Logs
 │
 ▼
Analyse
 │
 ▼
Corrélation
 │
 ▼
Risk Scoring
 │
 ├── Faible
 ├── Moyen
 └── Élevé
       │
       ▼
   Automatisation

Lorsque le niveau de risque dépasse le seuil défini, une automatisation peut être déclenchée via n8n.

⚡ Automatisation des Alertes

La plateforme permet de connecter l'analyse SOC à un workflow d'automatisation.

Détection
    │
    ▼
Risk Score
    │
    │ Score > seuil
    ▼
   n8n
    │
    ▼
Notification
    │
    ▼
  Slack

Cette approche permet de réduire les actions manuelles nécessaires pour le traitement initial des événements.

💻 Stack Technologique
Backend
☕ Java / Spring Boot
🐍 Python
⚡ FastAPI
Frontend
Angular
DevSecOps
GitLab CI/CD
Docker
SonarQube
OWASP Dependency-Check
npm audit
Trivy
Gitleaks
Checkov
OWASP ZAP
Monitoring & Observabilité
Prometheus
Grafana
Filebeat
OpenSearch
Intelligence Artificielle
Ollama
Mistral
Embeddings
RAG
OpenSearch Vector Search
Automatisation
n8n
Slack
✨ Fonctionnalités Clés
🔄 Pipeline CI/CD automatisé
🔐 Intégration de contrôles de sécurité dans le pipeline
🧪 Tests automatisés
🔎 Analyse SAST et SCA
🐳 Sécurisation des images Docker
🔑 Détection des secrets
🏗️ Analyse de l'Infrastructure as Code
🌐 Tests DAST
📊 Monitoring avec Prometheus et Grafana
📝 Centralisation des logs avec OpenSearch
🚨 Détection d'anomalies
🤖 Assistant SOC basé sur l'IA
🧠 RAG basé sur des connaissances de cybersécurité
⚠️ Risk scoring
🔗 Corrélation d'événements
⚡ Automatisation des alertes avec n8n
💬 Notifications Slack
📁 Structure du Projet
devsecops-pfe/
│
├── backend/
│   └── ...
│
├── frontend/
│   └── ...
│
├── soc-chatbot/
│   ├── app/
│   │   ├── main.py
│   │   ├── intent_classifier.py
│   │   ├── nlu.py
│   │   ├── risk_scorer.py
│   │   ├── rules_engine.py
│   │   ├── log_analyzer.py
│   │   ├── temporal_analyzer.py
│   │   ├── attack_correlator.py
│   │   └── ...
│   │
│   └── ...
│
├── .gitlab-ci.yml
├── docker-compose.yml
├── Dockerfile
└── README.md

La structure ci-dessus doit être adaptée à la structure exacte du dépôt.

🚀 Installation & Lancement
Prérequis
Java 17
Maven / Maven Wrapper
Node.js
Docker
Docker Compose
Python 3.x
Git
Cloner le projet
git clone <URL_DU_REPOSITORY>
cd devsecops-pfe
Lancer les services
docker compose up -d
Vérifier les conteneurs
docker ps
Lancer le backend
./mvnw spring-boot:run
Lancer le frontend
npm install
npm start

Les commandes exactes doivent être adaptées à la configuration finale du projet.

📈 Résultats

Quelques résultats obtenus durant le projet :

🐳 Optimisation des images Docker
Service	Avant	Après	Réduction
Backend	648 MB	187 MB	~71 %
Frontend	432 MB	52 MB	~88 %
🔐 Sécurité
Checkov : 91 % de conformité sur les contrôles évalués
Backend Trivy : 0 Critical, 1 High
Frontend Trivy : 0 Critical / High
SonarQube : objectif Security Rating A
📊 Logs
Centralisation de plusieurs millions d'événements dans OpenSearch
Détection d'anomalies basée sur Random Cut Forest
🔮 Perspectives

Plusieurs améliorations peuvent être envisagées :

intégration de davantage de sources Threat Intelligence ;
amélioration de la corrélation multi-événements ;
enrichissement automatique des incidents ;
ajout de nouveaux playbooks SOC ;
amélioration du modèle de classification des intentions ;
intégration avec d'autres outils SIEM/SOAR ;
amélioration de l'automatisation de la réponse aux incidents.
👩‍💻 Auteur

Rania Jarray

Ingénieure Cybersécurité & DevSecOps

🎓 Projet de Fin d'Études — TEK-UP

📌 Thème :

Plateforme DevSecOps intelligente avec détection d’anomalies applicatives et automatisation des alertes par l’intelligence artificielle

⭐ Projet réalisé dans le cadre du Projet de Fin d'Études — 2025/2026


**Mais je ne te conseille pas encore de copier-coller cette version telle quelle.** La prochaine étape intéressante serait de faire une version **100 % adaptée à ton dépôt réel**, notamment la partie `Structure du Projet`, les commandes d'installation, les URLs, les screenshots et l'architecture. Comme ça, le README ne donnera pas l'impression d'être un modèle générique mais vraiment celui de **ton PFE**.
