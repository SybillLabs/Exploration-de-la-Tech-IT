# Le monde du DevSecOps

## DevOps vs DevSecOps
### Le DevOps
Les tâches du DevOps sont :
- l'Automatisation et le déploiement
  - Gère et optimise les pipelines CI/CD pour accélérer le développement et le déploiement des applications
  - Utilisation des outils pour assurer l’intégration et la livraison continues
- la Gestion de l'infrastructure
  - Met en place et administre des infrastructures Cloud
  - Surveille la plateforme et la scalabilité des services déployés
- la Fiabilité et l'optimisation
  - Assure la disponibilité et la résilience des services
  - Optimise les performances et les coûts des infrastructures en automatisant les opérations

#### Les pipelines CI/CD

#### Les infrastructures Cloud

### Le DevSecOps
Les tâches du DevSecOps sont :
- Sécurisation des déploiements
  - Intègre des contrôles de sécurité automatisés dans les pipelines CI/CD
  - Utilise des outils pour détecter les vulnérabilités avant la mise en production
- Surveillance et conformité
  - Met en place des outils de monitoring pour détecter et prévenir les menaces en temps réel
  - Assure la conformité aux normes de sécurité
- Collaboration sécurité et DevOps
  - Travaille avec les développeurs et les équipes de sécurité pour intégrer la cybersécurité
  - Applique une Shift Left en intégrant des tests de sécurité dès les premières étapes du développement
 
#### Le Shift Left

## Les outils du DevSecOps
Il y a de nombreux outils qui existe, et personnellement je vais mettre l'accent sur deux outils.

### SonarQube
- Outils d’analyse de code source qui détecte les vulnérabilités et les mauvaises pratiques de codage.
- Il prend en charge plusieurs langages de programmation et s’intègre facilement dans les pipelines CI/CD

### Owasp Zap
- Outil de test d’intrusion pour les applications web.
- Conçu pour trouver automatiquement les failles de sécurité pendant le développement et les tests.

## Les tendances dans la communauté DevSecOps
### Adoption croissante du shift left
- Intégrer des tests de sécurité le plus tôt possible dans le cycle de développement du logiciel
- Méthode proactive permettant de renforcer la sécurité des applications tout en réduisant les coûts

### Architecture zero trust
- Principe qu’aucune machine, utilisateurs, logiciels, etc... n’est considéré comme fiable
- Vérification continue de l’identité et des autorisations avant d’accorder l’accès aux ressources

## Sources
Voici mes différentes sources.

### Normes
ISO 27001 : https://www.iso.org/fr/standard/27001
Nist : https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=958795
RGPD : https://www.economie.gouv.fr/entreprises/reglement-general-protection-donnees-rgpd#:~:text=conformer%20au%20RGPD-,Le%20RGPD%2C%20qu%27est-ce%20que%20c%27est,application%20le%2025%20mai%202018.

### SonarQube
https://www.gologic.ca/top-10-outils-devsecops/
https://www.sonarsource.com/products/sonarqube/

### Owasp
https://bluegoatcyber.com/blog/integrating-owasp-zap-in-devsecops/
https://www.zaproxy.org

### Tendances
https://yoursky.blue/fr/articles/tendances-devsecops
https://www.redhat.com/fr/topics/devops/shift-left-vs-shift-right
https://learn.microsoft.com/en-us/security/zero-trust/develop/secure-devops-environments-zero-trust
https://www.paloaltonetworks.com/resources/ebooks/cloud-security-spotlight-how-organizations-adopt-devsecops-and-shift-left-security  
