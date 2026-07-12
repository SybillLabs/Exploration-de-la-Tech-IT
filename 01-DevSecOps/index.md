# 🛡️ Sécurité de l'infrastructure système et réseau : le DevSecOps



## 📝 Contexte
Cette veille technologique a été réalisée durant ma **formation bootcamp de 5 mois : Technicien Supérieur Système et Réseau**. 
Lors de cette formation, j'avais préparé une présentation **Canva** destinée à ma classe (fichier disponible dans [Ressources](/W38-DevSecOps/Ressources/LeMondeDuDevSecOps.pdf)).  

Aujourd'hui, j'ai souhaité :
- **l'enrichir** avec des explications plus détaillées, des schémas et des définitions.
- **l'ajouter** dans mon dépôt GitHub *Exploration de la Tech IT*, afin de garder une trace écrite et évolutive de mes apprentissages.

> ℹ️ **Note** : Ce document est une veille technologique réalisée dans le cadre de ma formation. Il n'a pas vocation à être une documentation officielle, mais une synthèse accessible pour découvrir le **DevSecOps**.

## ⚙️🛡️ DevOps vs DevSecOps
### ⚙️ DevOps
Les missions du **DevOps** sont principalement liées à l'automatisation, la fiabilité et la gestion des infrastructures.
- **Automatisation et déploiement**
  - Mise en place et optimisation des pipelines CI/CD pour accélérer le développement et le déploiement
  - Intégration continue (CI) et livraison continue (CD)
- **Gestion de l'infrastructure**
  - Déploiement et administration d’infrastructures Cloud (AWS, Azure, GCP…)
  - Supervision de la scalabilité et de la disponibilité des services
- **Fiabilité et optimisation**
  - Assurer la résilience et la haute disponibilité des applications
  - Optimiser les coûts et les performances via l’automatisation (IaC, monitoring)

### 🛡️ DevSecOps
Le DevSecOps est une **évolution naturelle du DevOps**, qui intègre la sécurité dès le début du cycle de vie logiciel.
- **Sécurisation des déploiements**
  - Automatisation des scans de vulnérabilités dans les pipelines CI/CD
  - Détection proactive des failles avant la mise en production
- **Surveillance et conformité**
  - Monitoring en temps réel pour prévenir les menaces
  - Respect des normes ISO 27001, RGPD, NIST, PCI-DSS…
- **Collaboration Dev, Ops et Sec**
  - Approche *Shift Left* : les tests de sécurité sont intégrés dès le développement
  - Culture partagée : la sécurité n’est plus seulement l’affaire des équipes **Security**, mais de tous

## 🛠️ Les outils du DevSecOps
🔹 **_Définitions clés_**
- **SAST (Static Application Security Testing)**  
  - Analyse statique du code source pour détecter les failles avant exécution.  
  - Exemples : SonarQube, Snyk Code, Checkmarx  
- **DAST (Dynamic Application Security Testing)**  
  - Test de l’application en exécution pour simuler des attaques.  
  - Exemples : OWASP ZAP, Burp Suite, AppScan  
- **Container Security**  
  - Sécurisation des images Docker, conteneurs et clusters Kubernetes.  
  - Exemples : Trivy, Falco, Aqua Security  
- **IaC Security (Infrastructure as Code)** 
  - Analyse des scripts d’infrastructure (Terraform, Ansible) pour éviter les configurations vulnérables.
  - Exemples : Checkov, Terraform Sentinel  
- **Monitoring & SIEM (Security Information and Event Management)**
  - Centralisation et analyse des logs pour détecter les menaces.
  - Exemples : ELK, Splunk, Wazuh

🔹 **_Outils choisis_**
- **SonarQube (SAST)**
  - Analyse statique de code source (SAST) pour détecter bugs, vulnérabilités et *code smells*
  - Support multi-langages (Java, Python, JavaScript, etc.)
  - Intégration native avec GitLab CI/CD, Jenkins, GitHub Actions
- **OWASP ZAP (DAST)**
  - Outil de tests d’intrusion automatisés (DAST) pour les applications web
  - Simule des attaques courantes (SQLi, XSS, CSRF, etc.)
  - Intégration possible dans un pipeline CI/CD pour scanner à chaque build

## 🔄🚀 Pipeline CI/CD
### 📦 Étapes d'un pipeline CI/CD
1. **Build (Compilation & Packaging)**
  - Transformation du code source en artefact exécutable (binaire, image Docker, jar, etc.)
  - Exemple : un développeur fait un *push* du code ➡️ Jenkins/GitHub Actions lance un build
2. **Tests automatisés (Qualité & Sécurité)**
  - Tests unitaires ➡️ vérifient que chaque fonction marche correctement
  - Tests d’intégration ➡️ assurent la compatibilité entre les modules
  - Tests de sécurité (DevSecOps) ➡️ SAST, DAST, scan des dépendances dès cette phase
  - Exemple : SonarQube vérifie le code, OWASP ZAP teste l’appli déployée sur un environnement temporaire.
3. **Déploiement (Release & Livraison)**
  - Mise en production automatisée avec rollback possible en cas de problème.
  - Exemple : GitLab CI déploie automatiquement une nouvelle version de l’application.

### ⚓ Livraison avec Kubernetes & Helm
Dans les environnements modernes, les applications sont souvent conteneurisées avec Docker et orchestrées par **Kubernetes (K8s)**.
- Kubernetes (K8s)
  - Orchestrateur de conteneurs qui gère le déploiement, la scalabilité et la résilience des services.
  - Avantages : tolérance aux pannes, montée en charge automatique, mise à jour sans interruption (rolling updates).
- Helm
  - Gestionnaire de paquets pour Kubernetes, utilisé pour déployer des applications via des charts (des templates YAML).
  - Avantages : simplification et standardisation des déploiements complexes.

👉 **Exemple concret d’étape finale de pipeline** :
1. CI construit une image Docker et la pousse dans un registry (DockerHub, GitLab Container Registry).
2. CD déclenche Helm qui déploie automatiquement la nouvelle version sur un cluster Kubernetes.
3. Kubernetes assure la montée progressive de la nouvelle version (rolling update) et rollback en cas d’échec.

### 🛡️ DevSecOps dans la CI/CD
👉 **La sécurité est intégrée à chaque étape** :
- Analyse statique (Static Application Security Testing) dès le build
- Tests dynamiques (Dynamic Application Security Testing) avant déploiement
- Scan d’images Docker avant push vers le registry
- Monitoring & alertes une fois en production (logs, SIEM, sécurité Kubernetes)

### ⚙️ Exemple d’une pipeline DevSecOps
```text
                ┌─────────────┐
                │   Code &    │
                │  Commit     │
                └──────┬──────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Analyse statique │  ← (SAST : SonarQube, Snyk…)
              │   du code        │
              └──────┬───────────┘
                     │
                     ▼
            ┌──────────────────┐
            │  Build & Test    │
            │ (Unit tests)     │
            └──────┬───────────┘
                   │
                   ▼
          ┌─────────────────────┐
          │  Analyse dynamique  │  ← (DAST : OWASP ZAP, Burp…)
          │   Sécurité App      │
          └────────┬────────────┘
                   │
                   ▼
        ┌───────────────────────┐
        │  Scan des dépendances │ ← (Librairies, packages)
        │  et des conteneurs    │ ← (Trivy, Clair, AquaSec)
        └──────────┬────────────┘
                   │
                   ▼
          ┌───────────────────┐
          │   Déploiement     │ ← (CI/CD vers Cloud / K8s)
          │   sécurisé        │
          └────────┬──────────┘
                   │
                   ▼
        ┌────────────────────────┐
        │   Monitoring & Logs    │ ← (SIEM : Wazuh, Splunk, ELK)
        │   Alertes sécurité     │
        └────────────────────────┘
```

## ☁️ Infrastructure Cloud
L’usage du **Cloud** (AWS, Azure, GCP, OVH…) est aujourd’hui la norme en DevOps.
Il offre **élasticité, rapidité et scalabilité**, mais introduit aussi de nouveaux risques de sécurité.

🔹 **_Enjeux de sécurité dans le Cloud_**
1. **Gestion des identités et accès (IAM)**
  - Contrôle strict des utilisateurs, rôles et permissions
  - Principe du *least privilege* ➡️ donner seulement les droits nécessaires
  - Exemple : un compte applicatif ne devrait pas avoir les mêmes droits qu’un administrateur.
2. **Chiffrement des données (Data Security)**
  - En transit ➡️ TLS/HTTPS obligatoire
  - Au repos ➡️ disques, bases de données et sauvegardes chiffrés
  - Exemple : activer le chiffrement natif AWS S3 pour protéger les données stockées.
3. **Conformité réglementaire**
  - ISO 27001 : gestion de la sécurité de l’information
  - RGPD : protection des données personnelles en Europe
  - NIST : bonnes pratiques de cybersécurité
  - Exemple : une application traitant des données médicales doit respecter le RGPD et parfois HIPAA (US).
4. **Surveillance et réponse aux menaces**
  - Collecte et analyse des logs avec des solutions de type SIEM (Splunk, Wazuh, ELK)
  - Détection d’anomalies en temps réel (IAM compromis, activités suspectes)
  - Exemple : alerte si plusieurs échecs de connexion proviennent d’une IP étrangère.

👉 En résumé : le Cloud n’est pas « moins sécurisé », mais il nécessite des pratiques strictes pour éviter erreurs de configuration et attaques.

## ⬅️ Le Shift Left
Le principe est de déplacer la sécurité en amont du cycle de développement.

```
         ┌──────────────┐
         │   Planifier  │
         │ (requirements│
         │   & design)  │
         └───────┬──────┘
                 │
                 ▼
        ┌──────────────────┐
        │   Développer     │ ← Analyse statique (SAST),
        │   (coding)       │    revues de code, secrets scan
        └───────┬──────────┘
                │
                ▼
       ┌─────────────────────┐
       │    Tester tôt       │ ← Tests sécurité intégrés :
       │   (build, CI/CD)    │    DAST, scans dépendances
       └────────┬────────────┘
                │
                ▼
     ┌────────────────────────┐
     │ Déployer & Surveiller  │ ← Détection d’anomalies,
     │   (prod monitoring)    │    logs, SIEM
     └────────────────────────┘
```

👉 L’idée : trouver les failles **avant** la mise en production.

🔹 **_Avantages_**
- Moins de bugs en production, coûts de correction réduits.
- Feedback rapide pour les devs (on corrige quand c’est encore frais).
- Culture sécurité diffusée dans l’équipe.

🔹 **_Limites / attention_**
- Le shift left **n’élimine pas** la nécessité du monitoring en production : certaines failles (config runtime, attaques ciblées) ne sont visibles qu’en prod.
- Nécessite automatisation et formation : ajout d’outils sans processus = faux sentiment de sécurité.

## 📈 Tendances actuelles
- **Adoption croissante du Shift Left** ➡️ sécurité intégrée dès le développement
- **Architecture Zero Trust** ➡️ « Ne jamais faire confiance, toujours vérifier »
- **Sécurité des conteneurs & Kubernetes** ➡️ clusters très ciblés par les attaques
- **Automatisation & IA** ➡️ détection et correction automatique des vulnérabilités simples

## 🔍 Analyse critique
- ✅ **Adoption en croissance** : DevSecOps devient un standard dans les grandes entreprises.
- ❌ **Maturité encore faible** : beaucoup d’équipes intègrent des outils mais sans réelle culture sécurité partagée.
- ⚠️ **Défi principal** : l’humain → former les développeurs et impliquer le management.
- 🎯 **Tendance future** : automatisation (IA, bots de correction, pipelines intelligents) et sécurité Cloud-native.

## 📚 Sources
- **Normes**
  - [ISO 27001](https://www.iso.org/fr/standard/27001)
  - [NIST](https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=958795)
  - [RGPD](https://www.economie.gouv.fr/entreprises/reglement-general-protection-donnees-rgpd#:~:text=conformer%20au%20RGPD-,Le%20RGPD%2C%20qu%27est-ce%20que%20c%27est,application%20le%2025%20mai%202018)
- **Outils**
  - [SonarQube](https://www.sonarsource.com/products/sonarqube/)
  - [OWASP ZAP](https://www.zaproxy.org/)
  - [Top outils DevSecOps – Gologic](https://www.gologic.ca/top-10-outils-devsecops/)
  - [Integrating OWASP ZAP – BlueGoatCyber](https://bluegoatcyber.com/blog/integrating-owasp-zap-in-devsecops/)
- **Tendances**
  - [Tendances DevSecOps – YourSky](https://yoursky.blue/fr/articles/tendances-devsecops)
  - [Shift Left vs Shift Right – Red Hat](https://www.redhat.com/fr/topics/devops/shift-left-vs-shift-right)
  - [Zero Trust – Microsoft](https://learn.microsoft.com/en-us/security/zero-trust/develop/secure-devops-environments-zero-trust)
  - [Cloud Security & Shift Left – Palo Alto](https://www.paloaltonetworks.com/resources/ebooks/cloud-security-spotlight-how-organizations-adopt-devsecops-and-shift-left-security)

## 📖 Glossaire pour débutants IT
- **Pipeline CI/CD** : une « chaîne de montage » automatisée qui construit, teste et déploie un logiciel.
- **Artefact** : le fichier final généré par un build (ex. un exécutable, une image Docker).
- **Registry**: un dépôt où sont stockées les images Docker (ex. DockerHub, GitLab Registry).
- **Rollback** : revenir à une version précédente d’une appli après un échec de mise à jour.
- **Orchestrateur (Kubernetes)** : un « chef d’orchestre » qui gère automatiquement plusieurs conteneurs (démarrage, arrêt, redémarrage, mise à jour).
- **Helm** : un « gestionnaire de recettes » pour Kubernetes, qui simplifie le déploiement d’applications complexes.
- **Logs** : fichiers qui enregistrent tout ce qui se passe (erreurs, accès, alertes).
- **SIEM** : un système qui collecte et analyse ces logs pour détecter des attaques.

## 📝 Conclusion personnelle
Cette veille technologique m’a permis de découvrir les fondements du DevSecOps et de comprendre comment la sécurité peut être intégrée dans chaque étape du cycle de développement logiciel.  
Je suis arrivé sur ce sujet un peu par hasard : j'aime beaucoup le scripting Bash, mon professeur m’a parlé du DevOps, et mes recherches m’ont conduit au DevSecOps.  
C’est cette découverte que j’ai choisi de partager lors de ma présentation, et que je documente aujourd’hui ici.

> ⚠️ Note : Je n’ai pas encore pratiqué directement les outils et concepts cités (SAST, DAST, Kubernetes, Helm, SIEM), mais cette veille m’a permis de les comprendre théoriquement et de les rendre accessibles à d’autres débutants IT.

---

<p align="center">  <i>↪️ Back to <a href="/README.md">Main Page</a></i> | <i>📍 From <a href="https://github.com/SybillLabs">SybillLabs</a></i></p>