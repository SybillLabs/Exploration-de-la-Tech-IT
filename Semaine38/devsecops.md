# 🌐 Le monde du DevSecOps

## 1. DevOps vs DevSecOps
### 🔄 Le DevOps
Les missions du DevOps sont principalement liées à l'automatisation, la fiabilité et la gestion des infrastructures :
- **Automatisation et déploiement**:
  - Mise en place et optimisation des pipelines CI/CD pour accélérer le développement et le déploiement
  - Intégration continue (CI) et livraison continue (CD)
- **Gestion de l'infrastructure**:
  - Déploiement et administration d’infrastructures Cloud (AWS, Azure, GCP…)
  - Supervision de la scalabilité et de la disponibilité des services
- **Fiabilité et optimisation** : 
  - Assurer la résilience et la haute disponibilité des applications
  - Optimiser les coûts et les performances via l’automatisation (IaC, monitoring)

#### ⚙️ Pipelines CI/CD
Un pipeline **CI/CD (Continuous Integration / Continuous Deployment)** est la colonne vertébrale du DevOps.
Il permet d’automatiser le cycle de vie logiciel du **développement jusqu’à la mise en production**.

🔹 **_Étapes typiques d’un pipeline CI/CD_**
1. **Build (Compilation & Packaging)**  
  - Transformation du code source en artefact exécutable (binaire, image Docker, jar, etc.)
  - Exemple : un développeur push du code → Jenkins/GitHub Actions lance un build.
2. **Tests automatisés (Qualité & Sécurité)**
  - Tests unitaires → vérifient que chaque fonction marche correctement
  - Tests d’intégration → assurent la compatibilité entre les modules
  - Tests de sécurité (DevSecOps) → SAST, DAST, scan des dépendances dès cette phase
  - Exemple : SonarQube vérifie le code, OWASP ZAP teste l’appli déployée sur un environnement temporaire.
3. **Déploiement (Release & Livraison)**
  - Mise en production automatisée avec rollback possible en cas de problème.
  - Exemple : GitLab CI déploie automatiquement une nouvelle version de l’application.

🔹 **_Livraison avec Kubernetes & Helm_**
Dans les environnements modernes, les applications sont souvent conteneurisées avec **Docker** et orchestrées par **Kubernetes (K8s)**.
- **Kubernetes (K8s)**
  - Orchestrateur de conteneurs qui gère le déploiement, la scalabilité et la résilience des services.
  - Avantages : tolérance aux pannes, montée en charge automatique, mise à jour sans interruption (rolling updates).
- **Helm**
  - Gestionnaire de paquets pour Kubernetes, utilisé pour déployer des applications via des charts (des templates YAML).
  - Avantages : simplification et standardisation des déploiements complexes.

👉 Exemple concret d’étape finale de pipeline :
1. CI construit une image Docker et la pousse dans un registry (DockerHub, GitLab Container Registry).
2. CD déclenche Helm qui déploie automatiquement la nouvelle version sur un cluster Kubernetes.
3. Kubernetes assure la montée progressive de la nouvelle version (rolling update) et rollback en cas d’échec.

🔹 **_DevSecOps dans la CI/CD_**

👉 La sécurité est intégrée à chaque étape :
- Analyse statique (SAST) dès le build
- Tests dynamiques (DAST) avant déploiement
- Scan d’images Docker avant push vers le registry
- Monitoring & alertes une fois en production (logs, SIEM, sécurité Kubernetes)

#### ☁️ Infrastructures Cloud
L’usage du **Cloud** (AWS, Azure, GCP, OVH…) est aujourd’hui la norme en DevOps.
Il offre **élasticité, rapidité et scalabilité**, mais introduit aussi de nouveaux risques de sécurité.

🔹 **_Enjeux de sécurité dans le Cloud_**
1. **Gestion des identités et accès (IAM)**
  - Contrôle strict des utilisateurs, rôles et permissions
  - Principe du least privilege → donner seulement les droits nécessaires
  - Exemple : un compte applicatif ne devrait pas avoir les mêmes droits qu’un administrateur.
2. **Chiffrement des données (Data Security)**
  - En transit → TLS/HTTPS obligatoire
  - Au repos → disques, bases de données et sauvegardes chiffrés
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
