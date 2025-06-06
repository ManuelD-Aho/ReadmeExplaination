# **Documentation Technique Exhaustive du Système "GestionMySoutenance"**

## **Introduction Générale**

### **Présentation du Système "GestionMySoutenance"**

Le système "GestionMySoutenance" est une application web dynamique conçue pour la gestion numérisée et centralisée de l'ensemble du processus de soutenance académique. Son objectif principal est d'offrir une plateforme unifiée pour les différents acteurs impliqués dans ce processus, incluant les étudiants, le personnel administratif, les enseignants (notamment ceux agissant en tant que membres de commissions de validation), et les administrateurs système. L'application vise à structurer, suivre et archiver les étapes clés, depuis la soumission des rapports par les étudiants jusqu'à la validation finale par les instances pédagogiques, en passant par les vérifications de conformité administrative et les évaluations. <sup>1</sup>

### **Aperçu de l'Architecture Technique Globale**

L'application "GestionMySoutenance" repose sur une pile technologique moderne et éprouvée pour le développement web. Le langage principal côté serveur est PHP, spécifiquement en version 8.2. Pour la présentation et l'interaction côté client, le système utilise HTML, CSS pur, et JavaScript pur, indiquant une approche qui privilégie la maîtrise directe des technologies de base sans l'intermédiaire de frameworks frontend lourds. \[UserQuery\]

Les dépendances clés gérées via Composer incluent :

- vlucas/phpdotenv pour la gestion des variables d'environnement, ce qui est une bonne pratique pour la configuration sécurisée et flexible de l'application selon les environnements (développement, test, production).
- nikic/fast-route pour le routage des requêtes HTTP, permettant une gestion claire et performante des URL et de leur association aux contrôleurs.
- phpmailer/phpmailer pour l'envoi d'emails, une fonctionnalité essentielle pour les notifications et communications système.
- robthree/twofactorauth et bacon/bacon-qr-code pour la mise en œuvre de l'authentification à deux facteurs (2FA), renforçant la sécurité des comptes utilisateurs.
- tecnickcom/tcpdf pour la génération de documents PDF, cruciale pour la production d'attestations, de procès-verbaux et autres documents officiels.
- phpoffice/phpspreadsheet pour la manipulation de feuilles de calcul, probablement utilisée pour les fonctionnalités d'import/export de données. \[UserQuery\]

L'environnement de déploiement est conteneurisé à l'aide de Docker, avec une configuration pour un serveur web Apache. L'accès à la base de données MySQL (ou compatible) est assuré par les extensions PHP ext-pdo et ext-mysqli. Les autres extensions PHP listées (ext-mbstring, ext-ctype, ext-json, ext-intl, ext-gd, ext-zip) sont courantes et nécessaires pour la manipulation de chaînes de caractères multi-octets, la validation de types de caractères, la gestion du format JSON, l'internationalisation, le traitement d'images, et la gestion d'archives ZIP. \[UserQuery\]

La structure des répertoires du projet, notamment avec les dossiers Public/ (contenant le point d'entrée index.php et les assets), routes/ (pour web.php définissant les routes), et src/ (comprenant Backend/, Config/, et Frontend/views/), suggère une organisation claire et une séparation des préoccupations. \[UserQuery\]

### **Principes de Conception Fondamentaux**

L'analyse de la structure du projet et des documents descriptifs met en lumière plusieurs principes de conception fondamentaux qui sous-tendent le système "GestionMySoutenance".

- **Architecture MVC (Modèle-Vue-Contrôleur)** : La structure des répertoires avec src/Backend/Controller, src/Backend/Model, et src/Frontend/views indique clairement l'adoption du patron de conception MVC. <sup>1</sup> Ce choix architectural est déterminant pour la qualité et la pérennité de l'application. Il favorise une séparation nette des responsabilités :
    1. Le **Modèle** est responsable de la logique métier et de l'interaction avec la base de données. Par exemple, des classes comme Utilisateur.php dans src/Backend/Model/ gèrent les opérations CRUD pour l'entité utilisateur et encapsulent les règles de validation associées. <sup>1</sup>
    2. La **Vue** se charge de la présentation des données à l'utilisateur. Les fichiers dans src/Frontend/views/, tels que Auth/login.php ou Administration/dashboard_admin.php, contiennent le code HTML et la logique d'affichage minimale. <sup>1</sup>
    3. Le **Contrôleur**, situé dans src/Backend/Controller/ (par exemple, AuthentificationController.php ou Administration/AdminDashboardController.php), reçoit les requêtes HTTP, interagit avec le Modèle pour récupérer ou modifier les données, puis sélectionne la Vue appropriée pour renvoyer une réponse. <sup>1</sup> Cette séparation des préoccupations est une pratique standard pour les applications web robustes, améliorant la maintenabilité, la testabilité, et permettant un développement plus organisé, potentiellement en parallèle par différentes équipes. <sup>1</sup>
- **Gestion Textuelle des Rapports** : Une caractéristique distinctive du système est que les étudiants ne téléversent pas de fichiers pour le corps principal de leur rapport. Au lieu de cela, ils saisissent le contenu textuellement via des formulaires et des éditeurs de texte enrichi intégrés à la plateforme. <sup>1</sup> Cette approche a des implications significatives :
  - Elle simplifie considérablement la gestion des fichiers côté serveur et réduit les risques de sécurité associés aux téléversements de documents (par exemple, l'introduction de malwares via des fichiers bureautiques complexes).
  - La recherche plein texte dans le contenu des rapports devient techniquement plus aisée à implémenter et plus performante.
  - La table document_soumis reflète cette approche en stockant le contenu dans un champ contenu_textuel (probablement de type LONGTEXT en SQL) plutôt qu'un chemin vers un fichier binaire, pour les sections principales du rapport. <sup>1</sup> L'Agent de Contrôle de Conformité examine ce contenu_textuel directement dans l'interface de vérification. <sup>1</sup>
  - Cependant, cette méthode peut imposer des contraintes sur le formatage et la présentation du rapport par l'étudiant, qui pourrait être limité par les capacités de l'éditeur de texte fourni, notamment pour l'intégration de graphiques complexes ou de mises en page très spécifiques.
- **Génération Centralisée de Documents PDF** : L'utilisation de la bibliothèque tecnickcom/tcpdf indique une stratégie de génération centralisée des documents officiels au format PDF. <sup>1</sup> Cette approche est essentielle pour garantir la cohérence, l'uniformité et le respect du branding de l'établissement pour tous les documents émis (attestations, procès-verbaux, relevés de notes, etc.). Le service ServiceDocumentGenerator.php est identifié comme le composant clé responsable de cette fonctionnalité. <sup>1</sup>
  - Les modèles de ces documents, probablement au format HTML/CSS, sont gérés par l'Administrateur Système (via la section D.3.1 du Module Administration). <sup>1</sup>
  - Le ServiceDocumentGenerator récupère les données pertinentes de la base de données et les fusionne avec le modèle sélectionné. <sup>1</sup>
  - La bibliothèque TCPDF est ensuite utilisée pour convertir ce contenu dynamique en un fichier PDF standardisé, prêt à être téléchargé ou archivé.
- **Sécurité via Contrôle d'Accès Basé sur les Rôles (RBAC)** : Le système implémente un mécanisme RBAC robuste pour gérer les permissions. Ceci est visible à travers l'utilisation des tables groupe_utilisateur, traitement, et de la table de jonction rattacher. <sup>1</sup> Ce principe de sécurité vise à accorder aux utilisateurs uniquement les droits strictement nécessaires à l'accomplissement de leurs tâches (principe du moindre privilège). <sup>1</sup>
  - La table type_utilisateur définit la nature fondamentale du compte utilisateur (ex: Étudiant, Personnel Administratif).
  - La table groupe_utilisateur définit des rôles fonctionnels plus spécifiques (ex: Agent de Conformité, Membre de Commission).
  - La table traitement catalogue chaque action ou fonctionnalité atomique du système qui est soumise à un contrôle de permission.
  - La table rattacher établit le lien entre un groupe_utilisateur et les traitement auxquels il a accès.
  - Un service dédié, tel qu'un ServicePermissions (implicite dans la conception), est chargé de vérifier, pour chaque action sensible, si l'utilisateur connecté (via son appartenance à un groupe) possède le droit d'exécuter le traitement demandé. <sup>1</sup>
- **Audit Détaillé des Actions** : La table enregistrer joue un rôle central dans la traçabilité des opérations au sein du système. <sup>1</sup> Ce principe d'audit détaillé est fondamental pour la sécurité, la résolution d'incidents, et la conformité réglementaire.
  - Chaque action significative (création, modification, suppression d'entités, changements de statut, connexions) est enregistrée.
  - Un enregistrement typique dans la table enregistrer contient des informations cruciales : l'identifiant de l'utilisateur ayant effectué l'action (numero_utilisateur), le type d'action (id_action), la date et l'heure (date_action), l'entité concernée (type_entite_concernee, id_entite_concernee), et, de manière très importante, un champ details_action au format JSON. Ce dernier permet de stocker des informations contextuelles riches et granulaires sur l'action, telles que les anciennes et nouvelles valeurs lors d'une modification. <sup>1</sup>
  - L'adresse IP et le User-Agent sont également capturés, fournissant un contexte technique supplémentaire.
- **Architecture Modulaire** : L'application est clairement structurée en modules fonctionnels distincts : Administration, Personnel Administratif, Étudiant, et Commission de Validation. <sup>1</sup> Cette modularité est un atout majeur pour la gestion de la complexité du système.
  - Chaque module possède ses propres contrôleurs, vues, et potentiellement des modèles ou services spécifiques, ce qui facilite le développement, la maintenance et l'évolution de chaque partie de manière relativement indépendante.
  - Les interactions entre ces modules sont gérées par des appels à des services bien définis ou par des modifications d'état dans la base de données, favorisant un couplage lâche.
  - Cela permet une meilleure répartition des responsabilités fonctionnelles et une compréhension plus segmentée et donc plus aisée du système global.
- **Services Centralisés pour Logique Transversale** : L'utilisation de classes de service dédiées (par exemple, ServiceAuthentification.php, ServiceNotification.php, ServiceRapport.php, ServiceDocumentGenerator.php) pour encapsuler la logique métier complexe ou les fonctionnalités partagées entre plusieurs modules est une pratique de conception robuste. <sup>1</sup>
  - Cette approche favorise la réutilisabilité du code et la cohérence dans l'application des règles métier. Par exemple, ServiceAuthentification centralise toute la logique liée à la connexion, à la gestion des sessions, et à la création/activation des comptes. <sup>1</sup> De même, ServiceNotification et ServiceEmail gèrent de manière unifiée l'envoi de toutes les communications. <sup>1</sup>
  - Les contrôleurs des différents modules font appel à ces services pour exécuter des opérations métier, évitant ainsi la duplication de logique et la dispersion des règles de gestion.

Ces principes architecturaux et de conception confèrent au système "GestionMySoutenance" une base solide pour répondre aux exigences fonctionnelles tout en visant la maintenabilité, la sécurité et l'évolutivité.

## **Partie I : Module Administration**

Le Module Administration de "GestionMySoutenance" est le centre de contrôle névralgique de la plateforme. Il est conçu pour offrir aux administrateurs système un ensemble complet d'outils pour superviser, configurer, maintenir et sécuriser l'ensemble de l'application.

### **A. Introduction et Objectifs du Module Administration** <sup>1</sup>

L'objectif stratégique fondamental du Module Administration est de garantir la performance, la stabilité, la sécurité et la conformité de la plateforme "GestionMySoutenance" sur le long terme. Il vise également à s'assurer que les processus métier critiques, tels que la soumission et la validation des rapports de soutenance, se déroulent sans heurts et que les données historiques sont correctement gérées, préservées et accessibles à des fins d'audit ou d'analyse. <sup>1</sup>

Sur le plan opérationnel, ce module fournit à l'Administrateur Système les interfaces et les fonctionnalités nécessaires pour :

- Superviser l'état général de la plateforme et l'activité des utilisateurs.
- Configurer les paramètres globaux de l'application et les règles métier.
- Gérer l'ensemble des comptes utilisateurs (étudiants, personnel administratif, enseignants) et leurs droits d'accès.
- Maintenir les référentiels de données (années académiques, niveaux d'étude, statuts, etc.).
- Intervenir en cas de problème technique ou de nécessité de correction de données.
- Produire des rapports et des analyses sur l'utilisation du système.

Le rôle de l'Administrateur Système est donc central ; il dispose d'un accès complet à toutes les fonctionnalités du module et est le garant de la configuration globale, de la sécurité et de la maintenance de la plateforme.

### **B. Interface Utilisateur Principale (Header, Sidebar)** <sup>1</sup>

L'interface utilisateur du Module Administration est conçue pour être à la fois complète et intuitive, permettant à l'administrateur d'accéder rapidement aux nombreuses fonctionnalités.

**1\. Header Proposé de l'Interface d'Administration**

L'en-tête de l'interface d'administration est un élément constant, visible sur toutes les pages du module, fournissant des informations contextuelles et des actions globales.

- **Intitulé** : Le titre "Panneau de Contrôle Principal - GestionMySoutenance" identifie clairement la section. "GestionMySoutenance" ancre l'outil dans le nom global du projet, tandis que "Panneau de Contrôle Principal" indique sa fonction centrale de supervision et de configuration. <sup>1</sup>
- **Fonctionnalités associées au header** : <sup>1</sup>
  - **Logo de l'Institution/Application** : Un élément visuel de branding.
  - **Nom de l'Administrateur connecté** : Affiche le nom et prénom de l'utilisateur administrateur, récupéré de utilisateur.login_utilisateur ou via une jointure avec personnel_administratif si l'administrateur possède également un profil détaillé dans cette table.
  - **Lien vers le profil utilisateur de l'Admin** : Permet à l'administrateur de gérer son propre compte (modification du mot de passe, informations de contact de base).
  - **Bouton/Lien de Déconnexion** : Assure une déconnexion sécurisée. Cette action invalide la session côté serveur (via ServiceAuthentification.detruireSessionUtilisateur()) et redirige vers la page de connexion. L'action est systématiquement journalisée dans la table enregistrer.
  - **Indicateur d'Année Académique Active** : Un affichage discret mais essentiel de l'id_annee_academique (ex: "AA_2024_2025") ou du libelle_annee_academique (ex: "2024-2025") actuellement marquée comme est_active = 1 dans la table annee_academique. La présence constante de cette information est cruciale car de nombreuses opérations administratives (gestion des inscriptions, soumissions de rapports, configurations de délais) sont intrinsèquement liées à l'année académique en cours. Ce rappel visuel permanent aide l'administrateur à éviter des erreurs de configuration ou de gestion qui pourraient avoir des conséquences importantes sur le déroulement des processus pour les utilisateurs.

**2\. Sidebar Dynamique et Fonctionnalités Associées**

La barre latérale de navigation (sidebar) est l'outil principal permettant à l'administrateur de naviguer entre les différentes sections et fonctionnalités du module. Elle est conçue pour être claire, bien organisée et exhaustive.

- **Structure hiérarchique** : La sidebar est organisée avec des sections principales de premier niveau, qui peuvent se déployer pour révéler des sous-sections ou des onglets spécifiques si la section principale est complexe. Cette structure arborescente facilite la localisation des fonctionnalités. <sup>1</sup>
  - **Niveau 1 : Sections Principales** (ex: Tableau de Bord, Gestion des Utilisateurs, Gestion des Habilitations).
  - **Niveau 2 : Sous-sections ou Onglets Spécifiques** (ex: sous "Gestion des Utilisateurs", on trouve "Étudiants", "Personnel Administratif").
- **Éléments de la Sidebar et Fonctionnalités Pointées** : Chaque élément de la sidebar est un lien hypertexte qui charge une interface spécifique (une "page" ou un "onglet") du module d'administration. Les icônes associées à chaque libellé aident à une identification visuelle rapide.
  - **Tableau de Bord Principal** : Lien vers la Section A.
  - **Gestion des Utilisateurs** : Menu déroulant vers B.0 (Tous les Utilisateurs), B.1 (Étudiants), B.2 (Personnel Administratif), B.3 (Enseignants).
  - **Gestion des Habilitations** : Menu déroulant vers C.1 (Types Utilisateur), C.2 (Groupes Utilisateur), C.3 (Niveaux d'Accès), C.4.1 (Fonctionnalités/Traitements), C.4.2 (Assignation Permissions).
  - **Configuration Système** : Menu déroulant vers D.1 (Référentiels, avec un sous-lien direct pour D.1.1 Années Académiques en raison de son importance), D.2 (Paramètres Généraux/Workflow), D.3 (Modèles Documents/Emails).
  - **Gestion Académique & Administrative (Supervision)** : Menu déroulant vers E.1 (Supervision Inscriptions), E.2 (Supervision Notes), E.3 (Supervision Stages), E.4 (Associations Enseignants).
  - **Supervision & Maintenance** : Menu déroulant vers F.1 (Suivi Workflows), F.2 (Gestion PV Admin), F.3 (Notifications Système), F.4 (Journaux d'Audit), F.5 (Import/Export Données), F.6 (Maintenance Technique).
  - **Reporting & Analytique** : Menu déroulant vers G.1 (Générer Rapports), G.2 (Configurer Dashboards).
- **Adaptabilité et Permissions** : Bien que le rôle d'Administrateur Système ait, par définition, accès à toutes les fonctionnalités, la conception de la sidebar pourrait permettre une adaptation dynamique. Si des rôles d'administrateurs délégués avec des permissions plus restreintes étaient introduits ultérieurement (par exemple, un "Administrateur Scolarité" avec accès uniquement aux sections B.1, E.1, E.2, E.3), la sidebar n'afficherait que les items autorisés pour ce rôle/groupe. Cela impliquerait une vérification des permissions (via le ServicePermissions et la table rattacher) pour chaque item de menu avant son affichage. <sup>1</sup>

La clarté des libellés, l'intuitivité de la structure hiérarchique et la réactivité de la navigation sont des aspects essentiels à la bonne conception de cette sidebar pour garantir l'efficacité de l'administrateur.

### **C. Fonctionnalités Détaillées (par Onglet/Section)**

#### **A. Tableau de Bord Principal** <sup>1</sup>

Le Tableau de Bord Principal est la page d'accueil du Module Administration. Il offre une synthèse visuelle et immédiate de l'état de santé et de l'activité de la plateforme.

- **1\. Objectif** : Fournir une vue d'ensemble en temps réel (ou quasi-réel) des métriques vitales, des anomalies potentielles, et des raccourcis vers les tâches administratives fréquentes. Il vise à réduire le temps de diagnostic et à faciliter une gestion proactive du système. <sup>1</sup>
- **2\. Interactions et Interface** : L'interface est typiquement organisée en "widgets" ou "cartes" thématiques. <sup>1</sup>
  - **A.1. Bloc/Widget : Statistiques d'Utilisation Clés et d'Activité** :
    - **A.1.1. Nombre Total d'Utilisateurs Actifs et Répartition** : Affiche le nombre total d'utilisateurs avec statut_compte = 'actif' et une répartition par libelle_type_utilisateur (Étudiants, Enseignants, Personnel Administratif, Administrateurs).
      - _Logique SQL_ : SELECT COUNT(numero_utilisateur) FROM utilisateur WHERE statut_compte = 'actif'; et SELECT tu.libelle_type_utilisateur, COUNT(u.numero_utilisateur) AS nombre_actifs FROM utilisateur u JOIN type_utilisateur tu ON u.id_type_utilisateur = tu.id_type_utilisateur WHERE u.statut_compte = 'actif' GROUP BY tu.id_type_utilisateur, tu.libelle_type_utilisateur; <sup>1</sup>
    - **A.1.2. Statistiques sur les Rapports de Soutenance** : Pour l'année académique sélectionnée (active par défaut), affiche un diagramme du nombre de rapports par libelle_statut_rapport (ex: 'Soumis', 'Conforme', 'Validé').
      - _Logique SQL_ : SELECT sr.libelle_statut_rapport, COUNT(r.id_rapport_etudiant) AS nombre_rapports FROM rapport_etudiant r JOIN statut_rapport_ref sr ON r.id_statut_rapport = sr.id_statut_rapport JOIN etudiant etu ON r.numero_carte_etudiant = etu.numero_carte_etudiant JOIN inscrire i ON etu.numero_carte_etudiant = i.numero_carte_etudiant WHERE i.id_annee_academique = '' GROUP BY sr.id_statut_rapport, sr.libelle_statut_rapport ORDER BY sr.etape_workflow; <sup>1</sup>
    - **A.1.3. Volume de Données et Indicateurs de Stockage** : Taille de la base de données, nombre total de document_soumis, espace disque utilisé par ces documents (via SUM(taille_fichier)). <sup>1</sup>
    - **A.1.4. Nombre de Nouvelles Inscriptions** : Pour l'année sélectionnée/active.
      - _Logique SQL_ : SELECT COUNT(DISTINCT i.numero_carte_etudiant) FROM inscrire i WHERE i.id_annee_academique = ''; <sup>1</sup>
    - **A.1.5. Indicateurs d'Activité Récente (Optionnel)** : Nombre de connexions ou de nouveaux rapports soumis sur les dernières 24h. <sup>1</sup>
  - **A.2. Bloc/Widget : Alertes Système Critiques et Notifications Administratives** :
    - **A.2.1. État de la Base de Données** : Indicateur simple "OK" ou "ERREUR". <sup>1</sup>
    - **A.2.2. Alertes de Performance Serveur** : Si un monitoring externe est interfacé (CPU, RAM, Disque). <sup>1</sup>
    - **A.2.3. Alertes de Sécurité** : Nombre de comptes utilisateurs actuellement bloqués (SELECT COUNT(\*) FROM utilisateur WHERE statut_compte = 'bloque';). <sup>1</sup>
    - **A.2.4. État des Processus Automatisés (Tâches CRON)** : Statut du dernier lancement des tâches majeures (nettoyage, rappels). <sup>1</sup>
    - **A.2.5. Années Académiques non Clôturées** : Alerte si une annee_academique dont la date_fin est passée est toujours marquée comme est_active = 1. <sup>1</sup>
      - La proactivité permise par ces alertes est un atout majeur. Par exemple, l'identification rapide des comptes bloqués peut signaler une vague de tentatives de connexion infructueuses, potentiellement malveillantes, ou un problème généralisé d'accès. De même, une tâche CRON qui échoue silencieusement peut impacter des processus de fond (comme l'envoi de rappels importants) ; une alerte sur le tableau de bord permet une intervention rapide. Le suivi des années académiques non clôturées est essentiel pour la bonne gestion du cycle de vie académique et pour éviter que des opérations ne soient effectuées par erreur sur une année révolue.
  - **A.3. Bloc/Widget : Raccourcis Rapides** : Liens vers les fonctionnalités les plus fréquentes (Gestion des utilisateurs, Configuration année académique, Journaux d'audit, etc.). <sup>1</sup>
- **3\. Règles Métiers** : L'affichage des statistiques et des données est, par défaut, contextuel à l'année académique active. L'administrateur doit avoir la possibilité de sélectionner une autre année académique pour visualiser les données historiques correspondantes.
- **4\. Logique Algorithmique et Services** : Les calculs des statistiques reposent principalement sur des requêtes SQL d'agrégation (COUNT, AVG, SUM) exécutées sur les tables utilisateur, rapport_etudiant, inscrire, document_soumis, etc. Ces requêtes doivent être optimisées pour un chargement rapide du tableau de bord. Pour les indicateurs de performance serveur ou l'état des tâches CRON, une interaction avec des services système ou des logs spécifiques peut être nécessaire.
- **5\. Validations** : Non applicable pour la consultation, mais les actions déclenchées depuis les raccourcis sont soumises aux validations de leurs modules respectifs.

L'optimisation des requêtes SQL pour ce tableau de bord est primordiale pour garantir une expérience utilisateur fluide, surtout avec l'augmentation du volume de données. L'utilisation d'index pertinents sur les colonnes fréquemment utilisées dans les clauses WHERE, JOIN, et GROUP BY est indispensable. Pour les statistiques particulièrement lourdes à calculer, une stratégie d'agrégation précalculée (via des tâches CRON nocturnes par exemple) et stockée dans des tables de résumé pourrait être envisagée pour améliorer la réactivité. <sup>1</sup>

#### **B. Gestion des Utilisateurs** <sup>1</sup>

Cette section est l'une des plus critiques du Module Administration, car elle permet de gérer l'ensemble des comptes utilisateurs et leurs profils associés.

- **Objectif Stratégique** : Donner à l'administrateur une vision consolidée de la population des utilisateurs, permettre d'identifier des tendances, de surveiller l'activité globale des comptes, et de s'assurer de la cohérence de la base utilisateurs. <sup>1</sup>
- **Objectif Opérationnel** : Fournir un point d'entrée unique pour des recherches rapides sur l'ensemble des utilisateurs, indépendamment de leur type principal, et permettre des actions administratives groupées ou des interventions ciblées. <sup>1</sup>

##### **B.0. Utilisateurs (Vue Générale et Actions Transversales)** <sup>1</sup>

Cette sous-section offre une vue d'ensemble de tous les utilisateurs enregistrés dans le système, quels que soient leurs rôles ou types.

- **Objectif** : Permettre une recherche et des actions administratives sur l'ensemble de la population des utilisateurs.
- **B.0.1. Zone de Listage Exhaustif de Tous les Utilisateurs** :
  - **Interface** : Le cœur de cette interface est un tableau de données interactif, paginé et triable, présentant tous les enregistrements de la table utilisateur. Des informations clés issues de tables liées comme type_utilisateur et groupe_utilisateur sont affichées grâce à des jointures SQL. <sup>1</sup>
  - **SQL Requête de Base (Illustrative)** :  
        SQL  
        SELECT u.numero_utilisateur, u.login_utilisateur, u.email_principal,  
        tu.libelle_type_utilisateur, gu.libelle_groupe_utilisateur,  
        u.statut_compte, u.date_creation, u.derniere_connexion  
        FROM utilisateur u  
        LEFT JOIN type_utilisateur tu ON u.id_type_utilisateur = tu.id_type_utilisateur  
        LEFT JOIN groupe_utilisateur gu ON u.id_groupe_utilisateur = gu.id_groupe_utilisateur  
        ORDER BY u.date_creation DESC  
        LIMIT,;  
        <sup>1</sup>
  - **Colonnes Principales Affichées** :
    - numero_utilisateur (PK de utilisateur) : Identifiant unique interne.
    - login_utilisateur (UNIQUE) : Identifiant de connexion.
    - email_principal (UNIQUE) : Email principal pour notifications et récupération de mot de passe.
    - libelle_type_utilisateur (via type_utilisateur.libelle_type_utilisateur) : Rôle principal (Étudiant, Personnel Admin, etc.).
    - libelle_groupe_utilisateur (via groupe_utilisateur.libelle_groupe_utilisateur) : Groupe de permissions principal.
    - statut_compte (ENUM utilisateur.statut_compte) : État du compte ('actif', 'inactif', 'bloque', 'en_attente_validation', 'archive'). Un codage couleur peut être utilisé pour une identification visuelle rapide (ex: actif en vert, bloqué en rouge).
    - date_creation (utilisateur.date_creation).
    - derniere_connexion (utilisateur.derniere_connexion, peut être NULL).
    - **Colonne "Actions"** : Boutons/icônes contextuels par ligne :
      - "Voir Détails" : Redirige vers la vue détaillée du profil spécifique (B.1, B.2, ou B.3) en fonction de utilisateur.id_type_utilisateur.
      - "Modifier Compte Utilisateur" : Ouvre un formulaire pour modifier les champs de la table utilisateur (login, email, groupe, statut, etc.).
      - "Changer Statut Compte" : Permet de changer rapidement le statut_compte avec confirmation. <sup>1</sup>
  - **Pagination et Tri** : Essentiels pour la performance et l'ergonomie. <sup>1</sup>
- **B.0.2. Zone de Moteur de Recherche Globale d'Utilisateurs** :
  - **Interface** : Champs de saisie pour rechercher par numero_utilisateur, login_utilisateur, email_principal. Une recherche par Nom/Prénom est plus complexe car elle nécessite de joindre les tables etudiant, personnel_administratif, et enseignant (qui contiennent les noms/prénoms) avec utilisateur via numero_utilisateur. <sup>1</sup>
  - **Logique SQL** : Utilisation de LIKE pour les recherches partielles. Pour la recherche par nom/prénom, une approche possible est d'utiliser une UNION de SELECT numero_utilisateur FROM... WHERE nom LIKE... sur les trois tables de profils, puis de filtrer la table utilisateur avec WHERE numero_utilisateur IN (résultat_union).
- **B.0.3. Panneau de Filtres Avancés** :
  - **Interface** : Listes déroulantes et sélecteurs de date pour filtrer par id_type_utilisateur, id_groupe_utilisateur, statut_compte, email_valide, preferences_2fa_active, période de date_creation, période de derniere_connexion. <sup>1</sup>
  - **Logique SQL** : Les critères sélectionnés sont combinés avec AND dans la clause WHERE.
- **B.0.4. Actions Transversales sur Sélection Multiple d'Utilisateurs** :
  - **Interface** : Cases à cocher par ligne et "Tout sélectionner". Boutons d'actions de masse. <sup>1</sup>
  - **B.0.4.1. Changement de Statut en Masse** : Sélection du nouveau statut, confirmation, puis UPDATE utilisateur SET statut_compte = '' WHERE numero_utilisateur IN ('id1', 'id2',...);. Journalisation détaillée. <sup>1</sup>
  - **B.0.4.2. Envoi de Notifications en Masse** : Sélection d'un template de message ou rédaction ad-hoc. INSERT dans recevoir pour chaque utilisateur et envoi email via ServiceEmail. <sup>1</sup>
  - **B.0.4.3. Réinitialisation de Mot de Passe en Masse (HAUTEMENT SENSIBLE)** : Génération de token_reset_mdp pour chaque sélectionné, envoi email avec lien. Action très détaillée dans enregistrer. <sup>1</sup>
    - La sensibilité de cette action réside dans son potentiel d'impact sur un grand nombre de comptes. Une utilisation malveillante ou erronée pourrait compromettre la sécurité ou bloquer l'accès pour de nombreux utilisateurs. Des mécanismes de confirmation robustes, voire une double authentification de l'administrateur effectuant l'action, sont recommandés. La journalisation doit être particulièrement précise, incluant la liste des utilisateurs affectés.
  - **B.0.4.4. Gestion des Tokens Actifs (Évolution)** : Si des tokens de session JWT ou API sont stockés, une action pour les invalider. <sup>1</sup>
- **B.0.5. Section Résumé : Vue d'Ensemble des Types et Groupes d'Utilisateurs** :
  - **Interface** : Deux petits tableaux affichant le nombre d'utilisateurs par libelle_type_utilisateur et par libelle_groupe_utilisateur. <sup>1</sup>
  - **Logique SQL** : SELECT tu.libelle_type_utilisateur, COUNT(u.numero_utilisateur) FROM type_utilisateur tu LEFT JOIN utilisateur u ON tu.id_type_utilisateur = u.id_type_utilisateur GROUP BY tu.id_type_utilisateur, tu.libelle_type_utilisateur; (et similaire pour les groupes).
- **Tables SQL Primordialement Impliquées pour B.0** : utilisateur, type_utilisateur, groupe_utilisateur, etudiant, personnel_administratif, enseignant, enregistrer, message, recevoir. <sup>1</sup>
- **Considérations Spécifiques pour B.0** :
  - **Performance et Indexation** : Des index composites sur utilisateur (ex: sur (id_type_utilisateur, statut_compte)) et des index sur les champs de nom/prénom des tables de profil sont nécessaires pour optimiser les recherches complexes. L'analyse des requêtes via EXPLAIN est recommandée. <sup>1</sup>
  - **Stratégie de Génération des IDs VARCHAR** : La logique PHP doit garantir l'unicité et suivre une convention pour tous les identifiants générés manuellement (ex: numero_utilisateur, id_type_utilisateur). <sup>1</sup>

##### **B.1. Étudiants (gestion spécifique via etudiant, utilisateur, et tables académiques associées)** <sup>1</sup>

Cette section est dédiée à la gestion complète des profils et des comptes des étudiants.

- **Objectifs** : Assurer la gestion complète du cycle de vie des étudiants, de la création à l'archivage. Fournir des outils pour lister, rechercher, filtrer, créer, modifier et gérer le statut des comptes étudiants, et consulter leurs informations académiques. <sup>1</sup>
- **B.1.1. Listage des Étudiants** : <sup>1</sup>
  - **Interface** : Tableau paginé et triable des étudiants (etudiant joint à utilisateur).
  - **Colonnes Essentielles** : numero_carte_etudiant (PK etudiant), nom_etudiant, prenom_etudiant, numero_utilisateur, login_utilisateur, email_principal, statut_compte, "Dernière Année d'Inscription" (calculée via inscrire et annee_academique), "Dernier Niveau Inscrit" (via inscrire et niveau_etude), date_creation_compte.
  - **Actions Contextuelles** : "Voir Profil Complet", "Modifier Profil Étudiant", "Modifier Compte Utilisateur", "Gérer Inscriptions", "Voir Rapports Soumis", "Désactiver/Archiver Compte".
- **B.1.2. Moteur de Filtrage et de Recherche Avancée pour les Étudiants** : <sup>1</sup>
  - **Interface** : Formulaire de recherche/filtre.
  - **Champs de Recherche Directe** : numero_carte_etudiant, nom/prenom étudiant, numero_utilisateur, login_utilisateur, email_principal, email_contact_secondaire.
  - **Filtres Combinables** : utilisateur.statut_compte, inscrire.id_niveau_etude (pour année active), inscrire.id_annee_academique, utilisateur.id_groupe_utilisateur, inscrire.id_statut_paiement (pour année active), rapport_etudiant.id_statut_rapport (pour année active), existence de stage enregistré (faire_stage).
- **B.1.3. Création d'un Nouvel Étudiant (Workflow Détaillé)** : <sup>1</sup>
  - **Déclenchement** : Bouton "Créer Nouvel Étudiant".
  - **Interface du Formulaire de Création** : Structuré en "Informations Personnelles (Profil Étudiant)" et "Informations du Compte Utilisateur".
  - **Étape 1 : Saisie Informations Profil Étudiant (table etudiant)** : numero_carte_etudiant (PK, unique), nom, prenom, date_naissance, lieu_naissance, pays_naissance, nationalite, sexe, adresse_postale, ville, code_postal, telephone, email_contact_secondaire, contact_urgence_nom, contact_urgence_telephone, contact_urgence_relation.
  - **Étape 2 : Saisie Informations Compte Utilisateur (table utilisateur)** : login_utilisateur (unique), email_principal (unique), Mot de Passe Initial (généré ou saisi, haché), id_groupe_utilisateur (défaut 'GRP_ETUDIANT'), id_niveau_acces_donne (défaut niveau étudiant), statut_compte ('actif' ou 'en_attente_validation'), photo_profil (optionnel).
  - **Étape 3 : Traitement Côté Serveur (Logique PHP)** :
        1. Validation approfondie (unicité numero_carte_etudiant, login_utilisateur, email_principal).
        2. Génération numero_utilisateur unique (ex: "ETU_" + UUID).
        3. Hachage du mot de passe (password_hash()).
        4. id_type_utilisateur fixé à 'TYPE_ETUD'. Génération token_validation_email si statut_compte = 'en_attente_validation'.
        5. Début de transaction DB.
        6. INSERT INTO utilisateur.
        7. INSERT INTO etudiant (lié au numero_utilisateur).
        8. Journalisation dans enregistrer.
        9. COMMIT / ROLLBACK.
        10. Confirmation à l'admin.
        11. Notification email à l'étudiant (via ServiceEmail et ServiceNotification) avec identifiants et lien de validation/définition MDP. <sup>1</sup>
  - **Gestion des Prérequis pour Accès Plateforme** : La création du profil/compte par l'Admin peut précéder la validation des prérequis (scolarité à jour, stage effectué). Cependant, le ServiceAuthentification vérifiera ces prérequis avant d'autoriser la _connexion_ effective de l'étudiant, même si son statut_compte est 'actif'. Le Responsable Scolarité, lui, est bloqué lors de sa tentative de "Générer Compte Étudiant" si ces prérequis ne sont pas remplis dans le système. <sup>1</sup> Cette distinction est importante : l'admin peut anticiper la création, mais l'accès fonctionnel de l'étudiant reste conditionné.
- **B.1.4. Vue Détaillée du Profil Étudiant (Consultation Approfondie)** : <sup>1</sup>
  - **Accès** : Via lien "Voir Profil Complet" ou clic sur numero_carte_etudiant.
  - **Objectif** : Présenter de manière exhaustive toutes les informations relatives à un étudiant spécifique.
  - **Structure de la Page** :
        1. En-tête : Nom, prénom, numero_carte_etudiant, photo, statut. Boutons d'action.
        2. Informations Personnelles Détaillées (de etudiant, lecture seule ici).
        3. Informations du Compte Utilisateur (de utilisateur et tables liées : type, groupe, niveau d'accès, dates, 2FA).
        4. Historique des Inscriptions Académiques (tableau de inscrire avec libellés).
        5. Historique des Rapports de Soutenance Soumis (tableau de rapport_etudiant avec statuts).
        6. Historique des Réclamations (tableau de reclamation, si droits admin).
        7. Aperçu des Notes (tableau de evaluer, si droits admin).
  - **Considérations** : Performance (lazy loading pour sections lourdes), autorisations d'affichage par section, navigation (fil d'Ariane).
- **B.1.5. Modification du Profil Étudiant (etudiant) et du Compte Utilisateur (utilisateur) Associé** : <sup>1</sup>
  - **Accès** : Via boutons "Modifier Profil Étudiant" ou "Modifier Compte Utilisateur".
  - **Objectif** : Permettre la correction et la mise à jour des informations.
  - **Structure du Formulaire de Modification** : Onglets ou sections "Informations Personnelles Étudiant" et "Gestion du Compte Utilisateur", pré-remplis.
    - **Partie 1 (Profil etudiant)** : Champs de etudiant modifiables (sauf numero_carte_etudiant).
    - **Partie 2 (Compte utilisateur)** : Champs de utilisateur modifiables (login_utilisateur, email_principal - tous deux avec validation d'unicité), id_groupe_utilisateur, id_niveau_acces_donne, statut_compte, photo_profil. Actions spécifiques : "Réinitialiser le Mot de Passe", "Forcer la Validation de l'Email", "Gérer 2FA".
      - Si email_principal est modifié, utilisateur.email_valide passe à 0, nouveau token_validation_email généré, et email de revalidation envoyé.
  - **Workflow de Soumission (PHP)** : Validation, comparaison valeurs, hachage MDP si changé, UPDATE etudiant, UPDATE utilisateur, journalisation détaillée, notification à l'étudiant si changements critiques.
- **B.1.6. Suppression / Désactivation / Archivage d'un Étudiant** : <sup>1</sup>
  - **Objectif** : Gérer la fin du cycle de vie d'un compte, en privilégiant désactivation/archivage.
  - **B.1.6.1. Désactivation** : UPDATE utilisateur SET statut_compte = 'inactif';. L'étudiant ne peut plus se connecter, données conservées. Journalisation.
  - **B.1.6.2. Archivage** : UPDATE utilisateur SET statut_compte = 'archive';. Peut impliquer anonymisation partielle ou déplacement de documents vers stockage archive. Journalisation.
  - **B.1.6.3. Suppression Physique (EXCEPTIONNELLE)** : Uniquement si compte créé par erreur SANS aucune donnée académique liée, ou pour droit à l'effacement RGPD après analyse.
    - Workflow : Avertissement ultime, vérification intensive des dépendances (inscrire, rapport_etudiant, evaluer, reclamation). Si dépendances, suppression bloquée. Sinon, DELETE transactionnel des données liées (historique_mot_de_passe, pister, recevoir), puis etudiant, puis utilisateur. Journalisation spécifique de la suppression.
      - La préservation de l'intégrité référentielle est ici absolument critique. Supprimer un étudiant ayant des inscriptions ou des rapports soumis corromprait l'historique académique et statistique de l'établissement.
- **B.1.7. Gestion des Inscriptions Administratives et Pédagogiques d'un Étudiant (table inscrire)** : <sup>1</sup>
  - **Accès** : Via bouton "Gérer Inscriptions" pour un étudiant.
  - **Objectif** : Historique des inscriptions, ajout, modification (statut paiement, décision passage), suppression exceptionnelle.
  - **B.1.7.1. Listage des Inscriptions** : Tableau des inscrire pour l'étudiant, avec libellés (annee_academique, niveau_etude, statut_paiement_ref, decision_passage_ref).
  - **B.1.7.2. Ajout Nouvelle Inscription** : Formulaire pour id_annee_academique, id_niveau_etude, montant_inscription, date_inscription, id_statut_paiement, etc.
    - Logique : Validation unicité PK composite (numero_carte_etudiant, id_annee_academique, id_niveau_etude). INSERT INTO inscrire. Journalisation.
  - **B.1.7.3. Modification Inscription Existante** : Formulaire pré-rempli. Modification typique de id_statut_paiement, date_paiement, numero_recu_paiement, id_decision_passage. UPDATE inscrire. Journalisation.
  - **B.1.7.4. Suppression Inscription** : Uniquement si erreur manifeste et aucune donnée académique liée (notes, rapport). Vérification dépendances (evaluer, rapport_etudiant). DELETE FROM inscrire. Journalisation.

##### **B.2. Personnel Administratif (personnel_administratif, utilisateur, et tables de droits associées)** <sup>1</sup>

Cette section est dédiée à la gestion exhaustive des comptes et profils des membres du personnel administratif (Agents de Conformité, Responsables Scolarité, etc.).

- **Objectifs** : Assurer que chaque agent dispose d'un compte sécurisé avec des droits alignés sur ses fonctions. Gérer arrivées, départs, changements de rôle. <sup>1</sup>
- **B.2.1. Listage des Membres du Personnel Administratif** : <sup>1</sup>
  - **Interface** : Tableau paginé et triable des personnel_administratif joint à utilisateur.
  - **Colonnes Essentielles** : numero_personnel_administratif (PK personnel_administratif), nom, prénom, numero_utilisateur, login_utilisateur, email_principal, email_professionnel, libelle_groupe_utilisateur (critique pour le rôle), statut_compte, date_affectation_service, derniere_connexion.
  - **Actions Contextuelles** : "Voir Profil Complet", "Modifier Profil Personnel", "Modifier Compte Utilisateur", "Gérer Permissions/Groupes", "Voir Activités" (logs enregistrer filtrés).
- **B.2.2. Moteur de Filtrage et de Recherche Avancée** : <sup>1</sup>
  - **Champs de Recherche** : numero_personnel_administratif, nom/prénom, numero_utilisateur, login_utilisateur, emails.
  - **Filtres** : statut_compte, id_groupe_utilisateur (essentiel pour isoler par rôle), id_niveau_acces_donne, date_affectation_service.
- **B.2.3. Création d'un Nouveau Membre du Personnel Administratif** : <sup>1</sup>
  - **Interface** : Formulaire "Informations Professionnelles/Personnelles (Profil)" et "Informations du Compte Utilisateur".
  - **Étape 1 (Profil personnel_administratif)** : numero_personnel_administratif (PK, unique), nom, prenom, telephone_professionnel, email_professionnel, date_affectation_service, responsabilites_cles, champs personnels optionnels.
  - **Étape 2 (Compte utilisateur)** : login_utilisateur (unique), email_principal (unique), Mot de Passe Initial, id_groupe_utilisateur (choix critique déterminant les permissions), id_niveau_acces_donne, statut_compte ('actif' ou 'en_attente_validation'), photo_profil.
  - **Logique PHP** : Validation unicité, génération numero_utilisateur (ex: "PERS_ADM_" + UUID), hachage MDP, id_type_utilisateur = 'TYPE_PERS_ADMIN', INSERT transactionnel utilisateur puis personnel_administratif, journalisation, notification email.
- **B.2.4. Vue Détaillée du Profil d'un Membre du Personnel Administratif** : <sup>1</sup>
  - **Structure** : En-tête (nom, matricule, photo, statut), Informations Pro/Perso (de personnel_administratif), Informations Compte (de utilisateur), **Permissions Effectives** (liste des libelle_traitement via rattacher pour le groupe de l'agent), Historique des Actions Significatives (extrait de enregistrer filtré par numero_utilisateur de l'agent).
    - L'affichage des permissions effectives est un élément clé pour que l'administrateur puisse rapidement vérifier et comprendre les droits d'un agent. Cela nécessite une requête joignant traitement et rattacher sur le id_groupe_utilisateur de l'agent.
- **B.2.5. Modification du Profil Personnel et du Compte Utilisateur** : <sup>1</sup>
  - **Champs Modifiables (Profil personnel_administratif)** : Tous sauf PKs.
  - **Champs Modifiables (Compte utilisateur)** : login_utilisateur, email_principal (avec revalidation), **id_groupe_utilisateur (modification très sensible impactant les permissions)**, id_niveau_acces_donne, statut_compte. Actions : Réinit MDP, Gérer 2FA.
  - **Journalisation** : Très détaillée, notamment pour les changements de id_groupe_utilisateur.
- **B.2.6. Désactivation / Archivage d'un Membre du Personnel Administratif** : <sup>1</sup>
  - **Philosophie** : Privilégier désactivation/archivage pour préserver l'historique des actions de l'agent.
  - **Workflow** : Confirmation, **analyse d'impact et réassignation des tâches en cours (processus métier crucial avant action système)**, UPDATE utilisateur.statut_compte ('inactif' ou 'archive'), journalisation.
  - **Suppression Physique** : Extrêmement déconseillée si l'agent a effectué des actions enregistrées (approuver, inscrire, etc.).
- **Tables SQL Primordialement Impliquées pour B.2** : personnel_administratif, utilisateur, type_utilisateur, groupe_utilisateur, niveau_acces_donne, traitement, rattacher, enregistrer, message, recevoir. <sup>1</sup>

##### **B.3. Enseignants (enseignant, utilisateur, et tables d'associations académiques)** <sup>1</sup>

Cette section gère les profils des enseignants. La plupart servent de données de référence, sauf s'ils sont membres de commissions (auquel cas leur compte utilisateur est actif et lié à 'GRP_COMMISSION').

- **Objectifs** : Maintenir une base de données précise des enseignants et de leurs qualifications (grades, fonctions, spécialités) pour les processus administratifs et pédagogiques (notamment pour la Commission). Gérer les comptes des enseignants membres de commissions. <sup>1</sup>
- **B.3.1. Listage des Enseignants** : <sup>1</sup>
  - **Interface** : Tableau paginé et triable des enseignant joint à utilisateur.
  - **Colonnes Essentielles** : numero_enseignant (PK enseignant), nom, prénom, numero_utilisateur, login_utilisateur, email_principal, email_professionnel, "Principale Spécialité" (via specialite et attribuer), "Grade Actuel" (via grade et acquerir), "Fonction Actuelle" (via fonction et occuper), libelle_groupe_utilisateur (pour identifier 'GRP_COMMISSION'), statut_compte.
  - **Actions Contextuelles** : "Voir Profil Complet", "Modifier Profil Enseignant", "Modifier Compte Utilisateur" (pertinent pour membres commission), "Gérer Associations Académiques", "Voir Activités Liées" (consultatif : direction mémoire, votes commission, notes).
- **B.3.2. Filtrage et Recherche Avancée d'Enseignants** : <sup>1</sup>
  - **Champs de Recherche** : numero_enseignant, nom/prénom, numero_utilisateur, login_utilisateur, emails.
  - **Filtres** : statut_compte, id_groupe_utilisateur (pour isoler 'GRP_COMMISSION' ou 'GRP_ENSEIGNANT_REF'), id_specialite, id_grade, id_fonction.
- **B.3.3. Création d'un Nouvel Enseignant** : <sup>1</sup>
  - **Interface** : Formulaire "Informations Profil (enseignant)" et "Informations Compte Utilisateur (utilisateur)".
  - **Étape 1 (Profil enseignant)** : numero_enseignant (PK, unique), nom, prenom, telephone_professionnel, email_professionnel, champs personnels optionnels.
  - **Étape 2 (Compte utilisateur)** : login_utilisateur (unique ; "NO_LOGIN_" + numero_enseignant si pas d'accès direct), email_principal (unique), Mot de Passe Initial (aléatoire non communiqué si pas d'accès), id_type_utilisateur = 'TYPE_ENS', id_groupe_utilisateur ('GRP_COMMISSION' ou 'GRP_ENSEIGNANT_REF'), id_niveau_acces_donne, statut_compte ('actif' pour commission, 'inactif' ou statut "Référentiel" sinon), photo_profil.
  - **Logique PHP** : Validation, génération numero_utilisateur (ex: "ENS_" + UUID), hachage MDP, INSERT transactionnel utilisateur puis enseignant, journalisation, notification si compte actif.
  - **Étape 4 (Post-Création)** : Assignation initiale de grade, fonction, spécialité via B.3.6.
- **B.3.4. Vue Détaillée du Profil d'un Enseignant** : <sup>1</sup>
  - **Affichage** : Infos Perso/Pro (enseignant), Infos Compte (utilisateur), Associations Académiques Actuelles/Historiques (Grades via acquerir, Fonctions via occuper, Spécialités via attribuer), Activités Liées aux Soutenances (direction mémoire via affecter, votes via vote_commission), Permissions Effectives (si membre commission).
- **B.3.5. Modification du Profil Enseignant et du Compte Utilisateur** : <sup>1</sup>
  - **Champs Modifiables (Profil enseignant)** : Contacts, infos pro/perso.
  - **Champs Modifiables (Compte utilisateur)** : login_utilisateur, email_principal, statut_compte, id_groupe_utilisateur (crucial si un enseignant devient/cesse d'être membre de commission). Réinit MDP.
  - **Workflow** : Validation, UPDATE, journalisation.
- **B.3.6. Gestion des Associations Académiques d'un Enseignant** : <sup>1</sup>
  - **Objectif** : Maintenir à jour qualifications et affiliations pour la Commission.
  - **Interface** : Sélection numero_enseignant. Sections pour :
    - **Grades (acquerir)** : CRUD sur les paires (id_grade, date_acquisition) pour l'enseignant.
    - **Fonctions (occuper)** : CRUD sur les triplets (id_fonction, date_debut_occupation, date_fin_occupation).
    - **Spécialités (attribuer)** : Interface type "dual listbox" pour sélectionner/désélectionner des id_specialite. Logique de synchronisation INSERT/DELETE dans attribuer.
  - **Logique** : Opérations transactionnelles et journalisées.
- **B.3.7. Désactivation / Archivage d'un Compte Enseignant** : <sup>1</sup>
  - **Contexte** : Départ, retraite.
  - **Procédure** : Vérifier rôles actifs critiques (directeur mémoire sur rapports en cours de validation finale, votes en attente). UPDATE utilisateur.statut_compte ('inactif' ou 'archive'). Clôturer fonctions actives (occuper.date_fin_occupation). Enregistrements affecter, vote_commission conservés pour historique. Journalisation. Suppression physique déconseillée.
- **Tables SQL Primordialement Impliquées pour B.3** : enseignant, utilisateur, type_utilisateur, groupe_utilisateur, acquerir, grade, occuper, fonction, attribuer, specialite, affecter, statut_jury, vote_commission, validation_pv, evaluer, enregistrer. <sup>1</sup>
- **Considérations Spécifiques** : Différenciation claire enseignant référentiel vs. membre de commission via id_groupe_utilisateur et statut_compte. Les données de qualification sont principalement pour la Commission. <sup>1</sup>

#### **C. Gestion des Habilitations (RBAC)** <sup>1</sup>

Cette section est le cœur de la configuration de la sécurité et du contrôle d'accès. Elle permet à l'Administrateur Système de définir de manière granulaire qui peut faire quoi.

- **Objectif Stratégique** : Mettre en place et maintenir un modèle RBAC robuste, aligné sur les besoins et politiques de sécurité, assurant séparation des tâches et moindre privilège. <sup>1</sup>
- **Objectif Opérationnel** : Fournir les interfaces pour définir types utilisateurs, groupes, niveaux d'accès données, cataloguer fonctionnalités (traitements), et lier fonctionnalités aux groupes. <sup>1</sup>

##### **C.1. Types Utilisateur (Rôles) (type_utilisateur)** <sup>1</sup>

Gère les catégories fondamentales d'utilisateurs (Étudiant, Personnel Admin, etc.). id_type_utilisateur (PK, VARCHAR(50)) est manuel et significatif (ex: 'TYPE_ETUD').

- **C.1.1. Listage des Types Utilisateur** : Tableau id_type_utilisateur, libelle_type_utilisateur, "Nombre d'Utilisateurs Associés". Actions "Modifier", "Supprimer" (conditionnelle). <sup>1</sup>
- **C.1.2. Création Nouveau Type Utilisateur** : Formulaire pour id_type_utilisateur (unique), libelle_type_utilisateur. INSERT INTO type_utilisateur. Journalisation. <sup>1</sup>
- **C.1.3. Modification Type Utilisateur** : id_type_utilisateur en lecture seule. Modification libelle_type_utilisateur. UPDATE type_utilisateur. Journalisation. <sup>1</sup>
- **C.1.4. Suppression Type Utilisateur** : Confirmation forte. Vérification dépendances (SELECT COUNT(\*) FROM utilisateur WHERE id_type_utilisateur =?). Si utilisé, suppression bloquée. Sinon, DELETE FROM type_utilisateur. Journalisation. <sup>1</sup>

##### **C.2. Groupes Utilisateur (groupe_utilisateur)** <sup>1</sup>

Définit des regroupements logiques pour permissions communes. id_groupe_utilisateur (PK, VARCHAR(50)) est manuel et significatif (ex: 'GRP_AGENT_CONF_SCOL').

- **C.2.1. Listage des Groupes Utilisateur** : Tableau id_groupe_utilisateur, libelle_groupe_utilisateur, "Nombre d'Utilisateurs Membres", "Nombre de Permissions Assignées". Actions "Modifier", "Supprimer" (conditionnelle), "Gérer Permissions du Groupe". <sup>1</sup>
- **C.2.2. Création Nouveau Groupe Utilisateur** : Formulaire id_groupe_utilisateur (unique), libelle_groupe_utilisateur. INSERT INTO groupe_utilisateur. Journalisation. <sup>1</sup>
- **C.2.3. Modification Groupe Utilisateur** : id_groupe_utilisateur en lecture seule. Modif libelle_groupe_utilisateur. UPDATE groupe_utilisateur. Journalisation. <sup>1</sup>
- **C.2.4. Suppression Groupe Utilisateur** : Confirmation. Vérification dépendances (utilisateur.id_groupe_utilisateur, rattacher.id_groupe_utilisateur). Si utilisé, suppression bloquée. Sinon, DELETE FROM groupe_utilisateur. Journalisation. <sup>1</sup>
- **Considérations** : Le schéma actuel avec un seul id_groupe_utilisateur par utilisateur est simple mais peut être limitant pour des rôles multiples. Une table de jonction utilisateur_groupe_appartenance offrirait plus de flexibilité (hors périmètre actuel). <sup>1</sup>

##### **C.3. Niveaux d'Accès aux Données (niveau_acces_donne)** <sup>1</sup>

Définit la portée ou la visibilité des données. id_niveau_acces_donne (PK, VARCHAR(50)) est manuel (ex: 'LVL_GLOBAL_ALL'). La logique de filtrage est implémentée en PHP.

- **C.3.1. Listage des Niveaux d'Accès** : Tableau id_niveau_acces_donne, libelle_niveau_acces_donne, "Nombre d'Utilisateurs Associés". Actions "Modifier", "Supprimer" (conditionnelle). <sup>1</sup>
- **C.3.2. Création Nouveau Niveau d'Accès** : Formulaire id_niveau_acces_donne (unique), libelle_niveau_acces_donne. INSERT INTO niveau_acces_donne. Journalisation. <sup>1</sup>
  - La création ici ne fait que définir une étiquette. Le filtrage effectif des données basé sur ces niveaux doit être codé dans l'application PHP. Une coordination étroite avec les développeurs est nécessaire. <sup>1</sup>
- **C.3.3. Modification Niveau d'Accès** : id_niveau_acces_donne en lecture seule. Modif libelle_niveau_acces_donne. UPDATE niveau_acces_donne. Journalisation. <sup>1</sup>
- **C.3.4. Suppression Niveau d'Accès** : Confirmation. Vérification dépendances (utilisateur.id_niveau_acces_donne). Si utilisé, suppression bloquée. Sinon, DELETE FROM niveau_acces_donne. Journalisation. <sup>1</sup>
  - La suppression d'un niveau d'accès utilisé sans mise à jour du code PHP qui s'y réfère peut entraîner des erreurs ou un comportement inattendu (accès total ou nul).

##### **C.4. Permissions (Fonctionnalités) (gestion des tables traitement et rattacher)** <sup>1</sup>

Cœur de l'attribution des droits d'action. id_traitement (PK, VARCHAR(50)) est manuel et significatif (ex: 'TRAIT_ETUD_CREATE_NEW'), utilisé dans le code PHP.

- **C.4.1. Sous-Section : Gestion des Fonctionnalités / Traitements (traitement)** <sup>1</sup>
  - **Objectif** : Maintenir un dictionnaire des opérations système contrôlables.
  - **C.4.1.1. Listage des Traitements** : Tableau id_traitement, libelle_traitement, "Nombre de Groupes Ayant cette Permission". Actions "Modifier", "Supprimer" (très conditionnel). <sup>1</sup>
  - **C.4.1.2. Création Nouveau Traitement** : Formulaire id_traitement (unique, convention de nommage claire), libelle_traitement. INSERT INTO traitement. Journalisation. <sup>1</sup>
  - **C.4.1.3. Modification Traitement** : id_traitement en lecture seule (ne JAMAIS modifier si utilisé dans le code). Modif libelle_traitement. UPDATE traitement. Journalisation. <sup>1</sup>
  - **C.4.1.4. Suppression Traitement** : Confirmation forte. Vérification dépendances (rattacher, pister). Si utilisé, suppression bloquée. Préférer dépréciation (champ est_actif dans traitement) à suppression physique. <sup>1</sup>
- **C.4.2. Sous-Section : Assignation des Permissions aux Groupes Utilisateur (gestion de rattacher)** <sup>1</sup>
  - **Objectif** : Créer les liens entre groupe_utilisateur et traitement.
  - **Interface d'Assignation (Mode "par Groupe")** :
        1. Sélection du id_groupe_utilisateur.
        2. Affichage de deux listes (type "Dual Listbox") : "Permissions Assignées" et "Permissions Disponibles".
        3. Mécanisme de transfert (boutons "Ajouter >>", "<< Retirer").
        4. Bouton "Enregistrer les Modifications".
  - **Logique PHP de Sauvegarde** : Algorithme de synchronisation pour rattacher (comparaison liste soumise vs. base, puis INSERT/DELETE ciblés). Journalisation globale et détaillée des permissions ajoutées/retirées. <sup>1</sup>
- **Workflow Typique de Configuration des Droits pour un Nouveau Rôle** : <sup>1</sup>
    1. (C.1) Création type_utilisateur si besoin.
    2. (C.2) Création groupe_utilisateur (ex: "GRP_SUPPORT_ETUD").
    3. (C.4.1) Vérif/Création traitement nécessaires (ex: "TRAIT_ETUD_VIEW_PROFILE").
    4. (C.4.2) Assignation des traitements au groupe "GRP_SUPPORT_ETUD".
    5. (B.x) Assignation des utilisateurs au id_groupe_utilisateur "GRP_SUPPORT_ETUD".
- **Considérations Générales pour Habilitations** : Principe du moindre privilège, granularité des traitements, conventions de nommage, revue périodique des droits, pas de droits directs aux utilisateurs (permissions via groupes). <sup>1</sup>

#### **D. Configuration Système** <sup>1</sup>

Regroupe les fonctionnalités de paramétrage du comportement global et des données de base.

- **Objectif Stratégique** : Assurer que la plateforme fonctionne avec des données de référence correctes, que les processus sont configurés aux besoins, et que les communications sont professionnelles. <sup>1</sup>
- **Objectif Opérationnel** : CRUD des référentiels, ajustement paramètres workflow, gestion modèles documents/notifications. <sup>1</sup>

##### **D.1. Gestion des Référentiels (Paramètres Généraux)** <sup>1</sup>

Interface centralisée pour le CRUD de toutes les listes de valeurs standardisées (tables \_ref). La suppression d'une entrée est conditionnée à sa non-utilisation par une clé étrangère.

- **D.1.1. Années Académiques (annee_academique)** : CRITIQUE. id_annee_academique (PK), libelle_annee_academique, date_debut, date_fin, est_active (un seul à 1). Interface spécifique pour gérer est_active (désactivation de l'ancienne lors de l'activation d'une nouvelle). <sup>1</sup>
- **D.1.2. Niveaux d'Étude (niveau_etude)** : id_niveau_etude (PK), libelle_niveau_etude. <sup>1</sup>
- **D.1.3. Spécialités (specialite)** : id_specialite (PK), libelle_specialite, numero_enseignant_specialite (FK optionnel). <sup>1</sup>
- **D.1.4. Fonctions (fonction)** : id_fonction (PK), libelle_fonction. <sup>1</sup>
- **D.1.5. Grades (grade)** : id_grade (PK), libelle_grade, abreviation_grade. <sup>1</sup>
- **D.1.6. Unités d'Enseignement (UE) (ue)** : id_ue (PK), libelle_ue, credits_ue. <sup>1</sup>
- **D.1.7. Éléments Constitutifs d'UE (ECUE) (ecue)** : id_ecue (PK), libelle_ecue, id_ue (FK), credits_ecue. <sup>1</sup>
- **D.1.8. Entreprises (entreprise)** : id_entreprise (PK), libelle_entreprise, secteur_activite, etc. <sup>1</sup>
- **D.1.9. Niveaux d'Approbation (niveau_approbation)** : id_niveau_approbation (PK), libelle_niveau_approbation, ordre_workflow. <sup>1</sup>
- **D.1.10. Statuts/Rôles Jury (statut_jury)** : id_statut_jury (PK), libelle_statut_jury. <sup>1</sup>
- **D.1.11. Types d'Action Système (action)** : id_action (PK), libelle_action, categorie_action. <sup>1</sup>
- **D.1.12. Modèles de Message (message)** : id_message (PK), sujet_message, type_message. Contenu géré en D.3.2. <sup>1</sup>
- **D.1.13. Types de Notification (notification)** : id_notification (PK), libelle_notification. <sup>1</sup>
- **D.1.14. à D.1.22. Autres Référentiels de Statuts et Décisions** : statut_conformite_ref, statut_paiement_ref, statut_pv_ref, statut_rapport_ref, statut_reclamation_ref, decision_passage_ref, decision_validation_pv_ref, decision_vote_ref, type_document_ref. Chacun avec id_...\_ref (PK) et libelle_...\_ref. <sup>1</sup>

##### **D.2. Paramètres Applicatifs & Workflow** <sup>1</sup>

Configuration des règles métier globales, seuils, comportements. Stockage via fichier de conf (ex: .env) ou table systeme_parametres (non dans DDL).

- **D.2.1. Configuration des Délais et Dates Limites** : Date limite soumission rapports (par année/niveau), délai resoumission après corrections (conformité/commission), durée validité tokens (reset MDP, validation email). <sup>1</sup>
- **D.2.2. Règles de Validation de Conformité des Rapports** : Documents requis (via type_document_ref.requis_ou_non), formats fichiers autorisés, taille max fichiers, nombre pages min/max. <sup>1</sup>
- **D.2.3. Paramètres des Alertes Système et Notifications Automatiques** : Délai alerte rapport en attente (conformité/commission), délai alerte vote commission en attente, activation/désactivation notifications auto. Tâches CRON pour déclenchement. <sup>1</sup>
- **D.2.4. Paramètres du Processus de Vote en Ligne (Commission)** : Nombre max tours de vote, délai par tour, visibilité des votes, quorum/majorité requise. <sup>1</sup>
- **D.2.5. Options du Chat Intégré** : Politique rétention messages, création auto groupes discussion commission, autoriser partage fichiers, notifications chat. <sup>1</sup>
- **Sauvegarde des Paramètres** : Bouton "Enregistrer". Logique PHP met à jour fichier config ou BDD. Journalisation. <sup>1</sup>

##### **D.3. Modèles de Documents & Notifications** <sup>1</sup>

Personnalisation des gabarits pour documents PDF et communications.

- **D.3.1. Gestion des Modèles de Documents PDF** : Attestations, PV, reçus, bulletins. <sup>1</sup>
  - **Interface** : Listage types documents gérables. Pour chaque type : affichage modèle actif, action "Modifier/Téléverser Modèle" (upload fichier template HTML/DOCX ou éditeur riche WYSIWYG), prévisualisation, réinitialisation au défaut.
  - **Stockage Modèles** : Fichiers sur serveur, table modeles_pdf_config (conceptuelle) pour lier ID modèle au chemin.
  - **Logique ServiceDocumentGenerator** : Récupère template, données, fusionne, convertit en PDF (TCPDF).
- **D.3.2. Gestion des Modèles de Notifications (Courriel et Internes Plateforme) (message)** : <sup>1</sup>
  - **Interface** : CRUD sur message. Listage modèles (id_message, sujet_message, type_message).
  - **Création/Modification** : Formulaire pour id_message (unique), sujet_message (email), libelle_message (corps du message, éditeur riche, placeholders {VARIABLE}), type_message ('EMAIL', 'NOTIFICATION_PLATEFORME'). Prévisualisation.
  - **Logique d'Envoi (ServiceNotification, ServiceEmail)** : Identifie id_message, récupère template, remplace placeholders, envoie (email via ServiceEmail, notif interne via INSERT recevoir).
- **Considérations** : Placeholders robustes, internationalisation (i18n) si besoin (hors DDL actuel), test emails. <sup>1</sup>

#### **E. Gestion Académique & Administrative (Configuration & Supervision)** <sup>1</sup>

Supervision et configuration des processus académiques. L'Admin a un rôle de configuration, supervision et intervention exceptionnelle.

- **Objectif Stratégique** : Assurer structure correcte des processus académiques, cohérence et fiabilité des données. <sup>1</sup>
- **Objectif Opérationnel** : Consultation globale données académiques, configuration paramètres, modifications/corrections privilégiées, gestion liens structurels enseignants. <sup>1</sup>

##### **E.1. Inscriptions Administratives et Pédagogiques (inscrire)** <sup>1</sup>

Vue d'ensemble inscriptions, configuration règles, intervention.

- **E.1.1. Consultation Globale et Recherche d'Inscriptions** : Tableau paginé et triable de inscrire (jointures etudiant, annee_academique, niveau_etude, statut_paiement_ref, decision_passage_ref). Filtres et recherche. Action "Modifier Inscription". <sup>1</sup>
- **E.1.2. Configuration des Paramètres d'Inscription** : Règles cohérence cursus, gestion frais (potentielle table tarifs_scolarite), délais de paiement. <sup>1</sup>
- **E.1.3. Intervention de Niveau Administrateur sur Inscriptions** : Formulaire modif pré-rempli. Modification de tous les champs de inscrire (avec prudence pour PKs), justification requise pour audit. Journalisation détaillée. Suppression exceptionnelle (voir B.1.7.4). <sup>1</sup>

##### **E.2. Évaluations / Notes des Étudiants (evaluer)** <sup>1</sup>

Supervision notes, configuration processus évaluation, intervention exceptionnelle.

- **E.2.1. Consultation Globale et Recherche des Notes** : Tableau paginé et triable de evaluer (jointures etudiant, ecue, ue, enseignant, et potentiellement annee_academique via inscription). Filtres et recherche. Action "Modifier Note". <sup>1</sup>
- **E.2.2. Configuration Paramètres Processus Évaluation** : Périodes de saisie des notes (potentielle table periodes_saisie_notes), droits de saisie/modif (via traitement), règles calcul moyenne (informatif), affichage notes aux étudiants (date publication). <sup>1</sup>
- **E.2.3. Intervention Niveau Administrateur sur Notes** : Formulaire modif pré-rempli. Modification note, date_evaluation (PKs non modifiables). Motif admin obligatoire. Journalisation détaillée. Suppression exceptionnelle (très risquée). <sup>1</sup>
- **Considérations** : Intégrité notes validées, traçabilité modifications. <sup>1</sup>

##### **E.3. Stages (faire_stage, entreprise)** <sup>1</sup>

Vue d'ensemble stages, gestion référentiel entreprises, configuration, intervention.

- **E.3.1. Consultation Globale et Recherche Stages Enregistrés** : Tableau faire_stage (jointures etudiant, entreprise). Filtres et recherche. Action "Modifier Données du Stage". <sup>1</sup>
- **E.3.2. Gestion Référentiel Entreprises (entreprise)** : Redirection vers D.1.8 pour CRUD entreprise. <sup>1</sup>
- **E.3.3. Configuration Paramètres Relatifs aux Stages** : Prérequis stage pour accès plateforme, documents justificatifs (informatif pour RS), périodes min/max stage, règles validation sujet (processus externe). <sup>1</sup>
- **E.3.4. Intervention Niveau Administrateur sur Données de Stage** : Formulaire modif pré-rempli. Modification champs faire_stage (avec prudence pour PKs). Motif admin. Journalisation détaillée. Suppression exceptionnelle (si pas de rapport lié / compte activé). <sup>1</sup>
- **Considérations** : Rôle RS pour saisie courante. Impact sur accès étudiant. Lien logique avec rapport soutenance. <sup>1</sup>

##### **E.4. Associations Enseignants (acquerir, occuper, attribuer)** <sup>1</sup>

Gestion qualifications et fonctions des enseignants (référence pour Commission).

- **Interface** : Sélection enseignant, puis sections pour Grades, Fonctions, Spécialités.
- **E.4.1. Gestion Associations Enseignant-Grade (acquerir)** : CRUD sur paires (id_grade, date_acquisition) pour l'enseignant. <sup>1</sup>
- **E.4.2. Gestion Associations Enseignant-Fonction (occuper)** : CRUD sur triplets (id_fonction, date_debut_occupation, date_fin_occupation). <sup>1</sup>
- **E.4.3. Gestion Associations Enseignant-Spécialité (attribuer)** : Interface "dual listbox" pour sélectionner/désélectionner id_specialite. Logique de synchronisation INSERT/DELETE dans attribuer. <sup>1</sup>
- **Tables SQL** : enseignant, grade, acquerir, fonction, occuper, specialite, attribuer, enregistrer. <sup>1</sup>

#### **F. Supervision & Maintenance** <sup>1</sup>

Centre de contrôle opérationnel et technique.

- **Objectif Stratégique** : Garantir performance, stabilité, sécurité, conformité. <sup>1</sup>
- **Objectif Opérationnel** : Outils pour surveiller workflows, gérer documents finaux, contrôler volume logs/notifs, auditer, import/export, maintenance technique. <sup>1</sup>

##### **F.1. Suivi des Workflows et des Processus** <sup>1</sup>

Vue d'ensemble dynamique avancement validation rapports.

- **F.1.1. Tableau de Bord Supervision Rapports** : Widgets visuels (filtre par id_annee_academique).
  - Widget 1 : Répartition rapports par statut actuel (diagramme). <sup>1</sup>
  - Widget 2 : Délais moyens traitement par étape (calculs complexes, idéalement via table historique_statut_rapport). <sup>1</sup>
  - Widget 3 : Rapports en retard/bloqués (basé sur délais configurés en D.2.3). <sup>1</sup>
  - Widget 4 : Charge de travail (approximation pour Agents Conformité, Commission, Rédacteurs PV). <sup>1</sup>

##### **F.2. Gestion des Procès-Verbaux (Admin) (compte_rendu)** <sup>1</sup>

Accès centralisé PV, gestion archivage officiel, éligibilité diffusion.

- **F.2.1. Listage et Consultation Tous les PV** : Tableau compte_rendu. Filtres. Actions : Voir/Télécharger PDF, Modifier Statut PV (ex: 'PV_ARCHIVE_OFFICIEL'), Marquer pour Publication Externe. <sup>1</sup>
- **F.2.2. Archivage Officiel des PV** : Sélection PV 'PV_VALID', action "Archiver Officiellement" -> UPDATE id_statut_pv. <sup>1</sup>
- **F.2.3. Gestion Éligibilité Publication Externe** : UPDATE rapport_etudiant.publication_autorisee (nouvelle colonne) ou compte_rendu.publication_externe_ok (nouvelle colonne). <sup>1</sup>

##### **F.3. Gestion des Notifications Système (recevoir, notification, message)** <sup>1</sup>

Gestion volumétrie notifications, supervision envoi.

- **F.3.1. Supervision Notifications et Communications** : Indicateurs (nb total recevoir, répartition par type/statut, temps moyen lecture, état file emails). <sup>1</sup>
- **F.3.2. Archivage et Purge Notifications Utilisateurs (recevoir)** : Formulaire options purge (notifications lues > N mois, toutes notifs > M mois pour comptes inactifs/archivés). DELETE FROM recevoir. Journalisation. <sup>1</sup>
- **F.3.3. Gestion Modèles Message et Notification (Redirection)** : Raccourcis vers D.3.2, D.1.13. Affichage stats utilisation modèles. <sup>1</sup>

##### **F.4. Journaux d'Audit (enregistrer, pister)** <sup>1</sup>

Accès complet et recherche avancée logs. Non modifiables via interface.

- **F.4.1. Consultation Détaillée Journal Actions Utilisateurs (enregistrer)** : Tableau détaillé enregistrer (jointures utilisateur, action). Filtres (date, auteur, type action, entité, IP). Export CSV. Champ details_action (JSON) crucial. <sup>1</sup>
- **F.4.2. Consultation Détaillée Traçabilité Accès Fonctionnalités (pister)** : Tableau pister (jointures utilisateur, traitement). Filtres (date, utilisateur, fonctionnalité, accès accordé/refusé). <sup>1</sup>
- **Considérations** : Intégrité/Immutabilité logs. Volume (rotation, archivage, purge). Performance recherches (indexation). <sup>1</sup>

##### **F.5. Outils d'Import/Export Données** <sup>1</sup>

Réservé Admin Système droits élevés.

- **F.5.1. Fonctionnalité d'Import de Données** : Création/MAJ masse (profils utilisateurs, référentiels). <sup>1</sup>
  - Interface : Étapes (Sélection type données, Upload CSV + Options doublons/simulation, Mapping colonnes, Validation/Prévisualisation, Exécution, Rapport).
  - Logique PHP : Parse fichier, génère IDs VARCHAR, INSERT/UPDATE transactionnels, journalisation.
  - Sécurité : Validation rigoureuse, sauvegardes BDD avant, mode simulation.
- **F.5.2. Fonctionnalité d'Export de Données** : Extraction pour sauvegarde, analyse, migration. <sup>1</sup>
  - Interface : Étapes (Sélection type données/tables, Filtres optionnels, Sélection colonnes optionnelle, Choix format CSV/XML/SQL, Génération/Téléchargement).
  - Logique PHP : Construit requête, récupère données, formate, initie téléchargement.

##### **F.6. Maintenance Technique** <sup>1</sup>

Opérations bas niveau, diagnostic, sauvegarde/restauration. Prudence extrême.

- **F.6.1. Outils Maintenance Base de Données** : Boutons pour OPTIMIZE TABLE, ANALYZE TABLE, CHECK TABLE, REPAIR TABLE. Nettoyage données temporaires (sessions, tokens expirés). <sup>1</sup>
- **F.6.2. Gestion Sauvegardes et Procédures Restauration** : <sup>1</sup>
  - Déclencher sauvegarde manuelle (mysqldump via script serveur). Lister sauvegardes.
  - Procédure restauration : Très délicate. Interface limitée (documentation procédure CLI). Application en mode maintenance.
- **F.6.3. Application Mises à Jour Applicatives** : Pour MAJ mineures/patchs. Affichage version actuelle, vérif MAJ, appli MAJ (si géré par app). Outils externes (Composer, scripts déploiement) pour MAJ majeures. <sup>1</sup>
- **F.6.4. Informations de Diagnostic Système et Serveur** : Lecture seule : Version PHP/extensions, SGBD, config PHP pertinente, permissions répertoires, test connexion BDD. Lien phpinfo() (protégé). <sup>1</sup>
- **Considérations** : Droits stricts. Mode maintenance applicatif. Documentation procédures. Accès logs serveur. <sup>1</sup>

#### **G. Reporting & Analytique** <sup>1</sup>

Transformation données opérationnelles en informations structurées pour aide à la décision.

- **Objectif Stratégique** : Support décision pour amélioration continue processus. <sup>1</sup>
- **Objectif Opérationnel** : Outils pour générer rapports stats avancés, configurer/visualiser dashboards analytiques. <sup>1</sup>

##### **G.1. Génération de Rapports Statistiques Avancés** <sup>1</sup>

Création à la demande de rapports tabulaires/agrégés, exportables.

- **Interface Génération Rapports** : Étapes (Sélection domaine/sujet, Indicateurs/Mesures, Dimensions groupement, Filtres, Options formatage/export CSV/Excel/PDF). Option sauvegarde config rapport. <sup>1</sup>
- **G.1.1. Exemples Rapports Prédéfinis/Configurables** : <sup>1</sup>
  - **Processus Validation Rapports** : Taux conformité, Taux validation commission, Délais moyens traitement (nécessite historique_statut_rapport ou analyse enregistrer), Performance acteurs (anonymisation optionnelle).
  - **Contenus et Corrections** : Tendances thématiques (rapport_etudiant.theme), Analyse commentaires (NLP si structurés), Nombre moyen versions (document_soumis.version).
  - **Inscriptions et Notes** : Rapports basés sur données de la section E.
- **G.1.2. Personnalisation et Planification Rapports (Avancé)** : Query Builder graphique, sauvegarde vues, planification envoi emails (CRON). <sup>1</sup>

##### **G.2. Configuration et Visualisation de Tableaux de Bord Analytiques (Dashboards)** <sup>1</sup>

Interface visuelle et interactive pour KPIs clés.

- **G.2.1. Bibliothèque de Widgets/Graphiques Prédéfinis** : Pour KPIs (Taux Validation, Délai Moyen, etc.). Chaque widget alimenté par requête SQL agrégation. <sup>1</sup>
- **G.2.2. Interface Création/Personnalisation Tableau de Bord** : Nommer dashboard, grille mise en page, choix widgets, config options widget. Stockage config dans dashboard_configurations (JSON, nouvelle table). <sup>1</sup>
- **G.2.3. Visualisation Tableaux de Bord** : Sélection dashboard, chargement dynamique widgets, graphiques interactifs (Chart.js, ApexCharts). <sup>1</sup>
- **G.2.4. Filtrage Global Tableaux de Bord** : Filtres (année, niveau) s'appliquant à tous les widgets. <sup>1</sup>
- **Considérations** : Performance (indexation, agrégats précalculés/data marts), définition KPIs, capacités export, sécurité accès données. <sup>1</sup>

## **Partie II : Module Personnel Administratif** <sup>1</sup>

Le Module Personnel Administratif de "GestionMySoutenance" est l'interface de travail spécifiquement conçue pour les membres du personnel de l'établissement chargés des opérations administratives et du suivi du processus de soutenance des étudiants.

### **A. Introduction et Objectifs du Module**

L'objectif général de ce module est de fournir des outils adaptés et spécifiques aux différents rôles administratifs pour leur permettre de gérer efficacement leurs tâches quotidiennes. Il vise à assurer le respect des procédures de l'établissement concernant la conformité des informations des rapports, la gestion des dossiers étudiants, les inscriptions, et la génération des comptes utilisateurs. De plus, il facilite la communication et la coordination avec les étudiants et les autres instances, comme la commission de validation, tout en garantissant une traçabilité complète et sécurisée des actions administratives effectuées. <sup>1</sup>

**Rôles Clés et Accès** <sup>1</sup>

Ce module s'adresse principalement à deux types de rôles, chacun ayant des responsabilités et des accès distincts, déterminés par leur utilisateur.id_groupe_utilisateur et les permissions associées via la table rattacher:

1. **Agent de Contrôle de Conformité (Ex: id_groupe_utilisateur = 'GRP_AGENT_CONF')**:
    - Est responsable de la vérification administrative et réglementaire des informations et du contenu des rapports, qui sont saisis textuellement par les étudiants.
    - Prend la décision sur la conformité des soumissions avant leur transmission à la commission pédagogique.
    - Communique les motifs de non-conformité aux étudiants.
2. **Responsable Scolarité (Ex: id_groupe_utilisateur = 'GRP_GEST_SCOL')**:
    - Gère les dossiers administratifs des étudiants (informations personnelles, inscriptions, statuts de paiement).
    - Enregistre et valide les informations de stage des étudiants. Ces informations sont basées sur des justificatifs physiques ou des procédures externes au système, puis sont saisies manuellement dans la plateforme.
    - Est responsable de la génération des comptes utilisateurs pour les étudiants qui remplissent les prérequis.
    - Peut être impliqué dans la saisie des notes (si habilité par un traitement spécifique) et la génération de documents PDF officiels pour les étudiants.
    - Traite certaines réclamations étudiantes, notamment celles liées aux informations de stage ou aux prérequis d'accès à la plateforme.

L'accès au module est sécurisé par le service ServiceAuthentification.php. Chaque agent se connecte avec son login_utilisateur et son mot_de_passe personnels. Les fonctionnalités visibles et accessibles dépendront du groupe auquel il appartient et des traitement (permissions) qui lui sont rattacher. Il est important de noter qu'aucun fichier (rapport, attestation de stage physique, etc.) n'est téléversé par les étudiants ou par le personnel administratif via ce module pour constituer le dossier de rapport. Les informations des rapports sont saisies et stockées sous forme textuelle. Les documents officiels (attestations, bulletins) sont générés par le système au format PDF à partir des données en base. <sup>1</sup>

### **B. Interface Utilisateur Principale**

**1\. Header Proposé** <sup>1</sup>

L'en-tête du Module Personnel Administratif est conçu pour identifier clairement la section et personnaliser l'expérience de l'agent.

- **Intitulé** : "Espace Administratif MySoutenance - \\ - \[Nom Prénom de l'Agent\]".
- **Affichage** : Permanent en haut de chaque page du module.
- **Fonctionnalités associées au header** :
  - **Logo de l'Institution / Application**.
  - **Nom et Prénom de l'agent connecté** : Récupérés depuis personnel_administratif.nom, prenom via la liaison utilisateur.numero_utilisateur -> personnel_administratif.numero_utilisateur.
  - **Lien/Icône vers "Mon Profil"** : Permet à l'agent de gérer son propre compte utilisateur (mot de passe, photo_profil s'il souhaite en ajouter une).
  - **Indicateur de Notifications Non Lues** : Un badge avec un nombre sur une icône de cloche, basé sur recevoir.lue = 0 pour le numero_utilisateur de l'agent.
  - **Bouton/Lien de Déconnexion Sécurisée** : Appelle ServiceAuthentification.detruireSessionUtilisateur(), action loguée dans la table enregistrer.
  - **Affichage discret de l'Année Académique Active** : annee_academique.libelle_annee_academique où est_active = 1, récupérée via ServiceConfigurationSysteme.

**2\. Sidebar Dynamique** <sup>1</sup>

La barre latérale de navigation s'adapte en fonction du rôle spécifique de l'agent connecté (utilisateur.id_groupe_utilisateur).

- **2.1. Sidebar pour l'Agent de Contrôle de Conformité (GRP_AGENT_CONF)** <sup>1</sup>
  - **A. Tableau de Bord (Conformité)** : Libellé "Tableau de Bord", Icône Maison ou Graphique.
  - **B. Rapports à Vérifier** : Libellé "Rapports à Vérifier", Icône Dossier avec loupe.
  - **C. Historique des Vérifications** : Libellé "Historique Vérifications", Icône Archive ou Liste.
  - **D. Messagerie Interne (commun)** : Libellé "Messagerie", Icône Enveloppe ou Bulles de chat.
  - **E. Mon Profil (commun)** : Libellé "Mon Profil", Icône Utilisateur ou Engrenage.
- **2.2. Sidebar pour le Responsable Scolarité (GRP_GEST_SCOL)** <sup>1</sup>
  - **A_SCOL. Tableau de Bord (Scolarité)** (distinct du Tableau de Bord Conformité) : Libellé "Tableau de Bord Scolarité", Icône Maison ou Graphique.
  - **F. Gestion des Étudiants** : Libellé "Étudiants", Icône Groupe d'utilisateurs.
  - **G. Inscriptions** : Libellé "Inscriptions", Icône Formulaire ou Calendrier.
  - **H. Gestion des Stages** : Libellé "Gestion des Stages", Icône Mallette.
  - **I. Génération Comptes Étudiants** : Libellé "Comptes Étudiants", Icône Clé ou Utilisateur avec +.
  - **J. Notes et Évaluations (si habilité par traitement)** : Libellé "Notes & Évaluations", Icône Crayon ou Diplôme.
  - **K. Génération de Documents PDF** : Libellé "Documents Officiels PDF", Icône Imprimante ou PDF.
  - **D. Messagerie Interne (commun)**.
  - **E. Mon Profil (commun)**.

### **C. Fonctionnalités Détaillées par Rôle et Onglet**

#### **Partie I : Agent de Contrôle de Conformité (GRP_AGENT_CONF)** <sup>1</sup>

##### **A. Onglet: Tableau de Bord (Conformité)** <sup>1</sup>

- **Objectif** : Fournir à l'Agent de Conformité un aperçu rapide de sa charge de travail et des indicateurs clés relatifs à la conformité des rapports.
- **Contenu et Widgets** :
  - **A.1. Nombre de Rapports en Attente de Vérification** :
    - **Affichage** : Chiffre clé en grand.
    - **Logique SQL** : SELECT COUNT(r.id_rapport_etudiant) FROM rapport_etudiant r JOIN inscrire i ON r.numero_carte_etudiant = i.numero_carte_etudiant WHERE r.id_statut_rapport = 'RAP_SOUMIS' AND i.id_annee_academique = (SELECT id_annee_academique FROM annee_academique WHERE est_active = 1 LIMIT 1); Cette requête compte les rapports soumis (RAP_SOUMIS) pour l'année académique active.
    - **Lien** : Vers l'onglet "Rapports à Vérifier" (B).
  - **A.2. Rapports Vérifiés Récemment par l'Agent (ex: 5 derniers)** :
    - **Affichage** : Liste concise : Titre du rapport, Nom étudiant, Date de vérification, Statut de conformité donné.
    - **Logique SQL** : SELECT r.id_rapport_etudiant, r.libelle_rapport_etudiant, e.nom AS nom_etudiant, e.prenom AS prenom_etudiant, s.libelle_statut_conformite, a.date_verification_conformite FROM approuver a JOIN rapport_etudiant r ON a.id_rapport_etudiant = r.id_rapport_etudiant JOIN statut_conformite_ref s ON a.id_statut_conformite = s.id_statut_conformite JOIN etudiant e ON r.numero_carte_etudiant = e.numero_carte_etudiant WHERE a.numero_personnel_administratif = '' ORDER BY a.date_verification_conformite DESC LIMIT 5; Cette requête récupère les actions de vérification les plus récentes effectuées par l'agent connecté.
  - **A.3. Alertes (Optionnel, si configuré par Admin Système en D.2.3 du Module Admin)** :
    - Liste des rapports en attente de vérification depuis plus de X jours (X étant un systeme_parametres.param_value).
  - **A.4. Raccourcis** : Bouton "Vérifier le prochain rapport en attente".

##### **B. Onglet: Rapports à Vérifier** <sup>1</sup>

- **Objectif** : Lister tous les rapports étudiants dont les informations ont été soumises (saisies textuellement) et sont en attente du contrôle de conformité par l'agent.
- **Contenu et Fonctionnalités** :
  - **B.1. Tableau des Rapports en Attente de Vérification de Conformité** :
    - **Colonnes** : id_rapport_etudiant (PK), numero_carte_etudiant (de rapport_etudiant), Nom & Prénom Étudiant (jointure avec etudiant), libelle_rapport_etudiant (titre du rapport), rapport_etudiant.date_soumission.
    - **Tri** : Par date_soumission (le plus ancien en premier par défaut, pour traiter en FIFO), par nom d'étudiant.
    - **Pagination**.
    - **Logique SQL** : SELECT r.id_rapport_etudiant, r.numero_carte_etudiant, etu.nom, etu.prenom, r.libelle_rapport_etudiant, r.date_soumission FROM rapport_etudiant r JOIN etudiant etu ON r.numero_carte_etudiant = etu.numero_carte_etudiant JOIN inscrire i ON r.numero_carte_etudiant = i.numero_carte_etudiant WHERE r.id_statut_rapport = 'RAP_SOUMIS' AND i.id_annee_academique = (SELECT id_annee_academique FROM annee_academique WHERE est_active = 1 LIMIT 1) ORDER BY r.date_soumission ASC LIMIT,; Cette requête sélectionne tous les rapports ayant le statut 'RAP_SOUMIS' pour l'année académique active.
  - **B.2. Action par Ligne: "Vérifier ce Rapport"** :
    - Mène à l'interface détaillée de vérification de conformité (décrite ci-dessous). L'id_rapport_etudiant est passé en paramètre.

##### **C. Onglet: Historique des Vérifications** <sup>1</sup>

- **Objectif** : Permettre à l'agent de consulter l'historique de toutes les vérifications de conformité qu'il a personnellement effectuées.
- **Contenu et Fonctionnalités** :
  - **C.1. Tableau des Rapports Vérifiés par l'Agent Connecté** :
    - **Colonnes** : id_rapport_etudiant, Nom & Prénom Étudiant, libelle_rapport_etudiant, date_verification_conformite (de approuver), libelle_statut_conformite (de statut_conformite_ref), commentaire_conformite (extrait de approuver.commentaire_conformite).
    - **Filtres** : Par période (date_verification_conformite), par id_statut_conformite ('CONF_OK', 'CONF_NOK').
    - **Pagination**.
    - **Logique SQL** : SELECT r.id_rapport_etudiant, etu.nom, etu.prenom, r.libelle_rapport_etudiant, a.date_verification_conformite, sc.libelle_statut_conformite, SUBSTRING(a.commentaire_conformite, 1, 150) AS commentaire_extrait FROM approuver a JOIN rapport_etudiant r ON a.id_rapport_etudiant = r.id_rapport_etudiant JOIN statut_conformite_ref sc ON a.id_statut_conformite = sc.id_statut_conformite JOIN etudiant etu ON r.numero_carte_etudiant = etu.numero_carte_etudiant WHERE a.numero_personnel_administratif = '' ORDER BY a.date_verification_conformite DESC LIMIT,; Cette requête récupère l'historique des vérifications pour l'agent spécifique.
  - **C.2. Action par Ligne: "Voir Détails de la Vérification"** :
    - Affiche une vue en lecture seule de toutes les informations de la vérification (similaire à l'interface du workflow de conformité mais non modifiable), y compris le contenu du rapport tel qu'il était au moment de la vérification et le commentaire complet de conformité.

##### **Workflow : Processus de Vérification de Conformité d'un Rapport (Interface et Logique)** <sup>1</sup>

Ce workflow détaille les étapes et fonctionnalités lorsque l'Agent de Conformité examine un rapport étudiant soumis.

- **Accès** : Via l'action "Vérifier ce Rapport" sur une ligne de l'onglet B. L'id_rapport_etudiant est transmis en paramètre.
- **Interface Détaillée de Vérification** :
  - **Section 1 : En-tête Récapitulatif du Rapport et de l'Étudiant** : <sup>1</sup>
    - Affiche les données de rapport_etudiant : id_rapport_etudiant, libelle_rapport_etudiant, theme, resume, numero_attestation_stage (si pertinent), nombre_pages (déclaré par l'étudiant), date_soumission.
    - Affiche les données de etudiant (via rapport_etudiant.numero_carte_etudiant) : numero_carte_etudiant, Nom & Prénom.
    - Affiche les informations d'inscription pour l'année active (via inscrire et rapport_etudiant.numero_carte_etudiant, jointure avec annee_academique et niveau_etude) : libelle_niveau_etude, libelle_annee_academique.
  - **Section 2 : Consultation du Contenu du Rapport Soumis par l'Étudiant (TEXTUEL)** : <sup>1</sup>
    - Pour chaque document_soumis lié à cet id_rapport_etudiant (filtré par la dernière version pour chaque id_type_document) :
      - Affichage du type_document_ref.libelle_type_document (ex: "Résumé du Rapport", "Corps Principal", "Bibliographie").
      - Affichage du document_soumis.contenu_textuel dans une zone de texte en lecture seule (potentiellement avec un rendu HTML simple si l'éditeur de l'étudiant a permis un formatage de base).
    - Aucun fichier à télécharger ou à ouvrir. L'agent lit le contenu directement dans l'interface.
  - **Section 3 : Checklist de Conformité (basée sur les règles de ServiceConfigurationSysteme)** : <sup>1</sup>
    - Affichage des critères de conformité définis par l'Admin Système (via D.2.2 du Module Admin) :
      - Liste des type_document_ref.libelle_type_document (interprétés comme des sections d'information) qui sont marqués requis_ou_non = 1. L'agent coche manuellement une case "Présent et Conforme" ou "Absent/Non Conforme" pour chaque section requise après avoir lu le contenu dans la Section 2.
    - Rappel du nombre de pages min/max attendu. L'agent compare avec rapport_etudiant.nombre_pages (déclaré) et évalue la plausibilité par rapport au volume de contenu_textuel visible.
    - **Vérification du Statut Administratif de l'Étudiant** : Le système affiche un indicateur clair (ex: "Scolarité: PAYÉE", "Stage: ENREGISTRÉ") basé sur les données de inscrire.id_statut_paiement et l'existence d'un faire_stage pour l'étudiant et l'année académique active. L'agent confirme visuellement ces prérequis.
  - **Section 4 : Décision de Conformité et Commentaires** : <sup>1</sup>
    - **Choix de la Décision (Boutons Radio obligatoires)** :
      - Option 1 : "Conforme" (correspond à id_statut_conformite = 'CONF_OK').
      - Option 2 : "Incomplet / Non Conforme" (correspond à id_statut_conformite = 'CONF_NOK').
    - **Champ commentaire_conformite (TEXT, dans la table approuver)** :
      - Ce champ est obligatoire si la décision est "Incomplet / Non Conforme".
      - L'agent doit y détailler de manière claire et constructive les points de non-conformité et les corrections attendues par l'étudiant (ex: "La section 'Bibliographie' est manquante.", "Le résumé dépasse la longueur autorisée de X mots.", "Le contenu de la section 'Méthodologie' est insuffisant.").
      - L'interface peut proposer une liste de motifs de non-conformité standards (pré-configurés par l'Admin Système) que l'agent peut sélectionner, en complément d'un champ de texte libre pour des précisions.
  - **Section 5 : Bouton d'Action: "Enregistrer la Décision de Conformité"** <sup>1</sup>
- **Workflow de Traitement (appel à ServiceConformite.traiterVerificationConformite)** : <sup>1</sup>
    1. L'Agent de Conformité soumet le formulaire de décision après avoir examiné toutes les sections.
    2. **Données d'Entrée pour le service** : id_rapport_etudiant, numero_personnel_administratif (de l'agent connecté, récupéré de la session PHP), id_statut_conformite (la valeur 'CONF_OK' ou 'CONF_NOK' correspondant au choix), commentaire_conformite (si 'CONF_NOK', sinon NULL ou chaîne vide).
    3. **Le service exécute la logique suivante (en utilisant une transaction de base de données)** :
        - INSERT INTO approuver (numero_personnel_administratif, id_rapport_etudiant, id_statut_conformite, commentaire_conformite, date_verification_conformite) VALUES (?,?,?,?, NOW());
        - **Détermination du nouveau id_statut_rapport pour la table rapport_etudiant** :
            - Si id_statut_conformite était 'CONF_OK', alors id_nouveau_statut_rapport = 'RAP_CONF' (Conforme, transmis à la commission).
            - Si id_statut_conformite était 'CONF_NOK', alors id_nouveau_statut_rapport = 'RAP_NON_CONF' (Non conforme, retourné à l'étudiant pour corrections).
        - UPDATE rapport_etudiant SET id_statut_rapport = \[id_nouveau_statut_rapport\] WHERE id_rapport_etudiant =?;
        - **Journalisation de l'action dans enregistrer** : id_action = 'ACTION_VERIF_CONF_RAP', type_entite_concernee = 'RAPPORT_ETUDIANT', id_entite_concernee = id_rapport_etudiant, details_action (JSON) contenant { "decision_conformite": "CONF_OK/CONF_NOK", "commentaire": "..." }.
        - Commit de la transaction. Si une erreur survient, un rollback est effectué et un message d'erreur est présenté à l'agent.
    4. **Notifications Post-Traitement (déclenchées par ServiceConformite via ServiceNotification, qui peut appeler ServiceEmail)** : <sup>1</sup>
        - **Notification à l'Étudiant (recevoir et email)** :
            - Si 'CONF_OK' : Message type "Félicitations, les informations de votre rapport '\[libelle_rapport_etudiant\]' ont été jugées conformes et ont été transmises à la commission pédagogique pour évaluation."
            - Si 'CONF_NOK' : Message type "Les informations de votre rapport '\[libelle_rapport_etudiant\]' ont été jugées non conformes. Motifs et corrections attendues: \[contenu de approuver.commentaire_conformite\]. Veuillez apporter les modifications nécessaires directement sur la plateforme et resoumettre le contenu de votre rapport avant le ."
        - **Notification à la Commission (au groupe GRP_COMMISSION via recevoir, si 'CONF_OK')** : Message type "Un nouveau rapport '\[libelle_rapport_etudiant\]' soumis par l'étudiant \[Nom Prénom Étudiant\] est maintenant disponible pour évaluation par la commission."
    5. L'agent est redirigé vers la liste "Rapports à Vérifier" (onglet B), qui est actualisée (le rapport traité n'y figure plus). Ce rapport apparaît désormais dans son "Historique des Vérifications" (onglet C).

#### **Partie II : Responsable Scolarité (GRP_GEST_SCOL)** <sup>1</sup>

##### **A_SCOL. Onglet: Tableau de Bord (Scolarité)** <sup>1</sup>

- **Objectif** : Fournir au Responsable Scolarité un aperçu de ses tâches principales et des indicateurs clés de gestion des étudiants.
- **Contenu et Widgets** :
  - **A_SCOL.1. Nombre d'Étudiants Actifs** (pour l'année académique en cours annee_academique.est_active = 1) :
    - **Logique SQL** : SELECT COUNT(DISTINCT e.numero_carte_etudiant) FROM etudiant e JOIN inscrire i ON e.numero_carte_etudiant = i.numero_carte_etudiant WHERE i.id_annee_academique = (SELECT id_annee_academique FROM annee_academique WHERE est_active = 1 LIMIT 1);
  - **A_SCOL.2. Étudiants Éligibles en Attente de Génération de Compte Utilisateur** :
    - **Affichage** : Nombre d'étudiants pour lesquels inscrire.id_statut_paiement est 'PAIE_OK' (ou équivalent "Payé/Exonéré") pour l'année active ET un faire_stage est enregistré pour l'année active, MAIS pour lesquels etudiant.numero_utilisateur est NULL OU le utilisateur lié (via etudiant.numero_utilisateur) a un statut_compte indiquant une création non finalisée (ex: 'creation_en_attente_par_RS').
    - **Logique applicative complexe** pour identifier ces cas.
    - **Lien** : Vers l'onglet "Génération Comptes Étudiants" (I).
  - **A_SCOL.3. Inscriptions Récentes / Mises à Jour de Paiement (ex: 7 derniers jours)** :
    - Liste des dernières opérations sur inscrire (créations ou modifications de id_statut_paiement à 'PAIE_OK').
  - **A_SCOL.4. Stages Récemment Enregistrés (ex: 7 derniers jours)** :
    - Liste des derniers faire_stage créés/modifiés par ce RS.
  - **A_SCOL.5. Réclamations Étudiantes Assignées ou Non Traitées** (celles concernant la scolarité, les stages, ou les demandes de reprise de processus) :
    - Si le RS traite certains type_reclamation_ref.
    - **Logique SQL** : SELECT COUNT(\*) FROM reclamation WHERE id_statut_reclamation IN ('RECLAM_RECUE', 'RECLAM_EN_COURS') AND (numero_personnel_traitant IS NULL OR numero_personnel_traitant = ''); (si un système d'assignation de réclamation est en place).
  - **A_SCOL.6. Raccourcis** : Vers "Gestion des Étudiants" (F), "Inscriptions" (G), "Gestion des Stages" (H), "Génération Comptes Étudiants" (I).

##### **F. Onglet: Gestion des Étudiants** <sup>1</sup>

- **Objectif** : Permettre au RS de consulter, rechercher, et créer ou modifier les profils de base des étudiants. La suppression physique est réservée à l'Admin Système.
- **Interface et Fonctionnalités** (similaires au Module Administration B.1, avec des droits adaptés pour le RS) :
  - **F.1. Listage des Étudiants** :
    - Tableau affichant numero_carte_etudiant, nom, prenom, login_utilisateur (si compte utilisateur existe et est lié), statut_compte (du compte utilisateur), dernière année/niveau d'inscription.
    - Filtres et Recherche : Par numero_carte_etudiant, nom/prénom, id_annee_academique d'inscription, id_niveau_etude.
  - **F.2. Consultation du Profil Détaillé d'un Étudiant** :
    - Vue consolidée des informations de etudiant, utilisateur (si existe et lié), historique des inscrire, faire_stage. Accès en lecture aux informations des rapport_etudiant (métadonnées et statuts) et evaluer (notes) pour cet étudiant.
  - **F.3. Création d'un Nouveau Profil Étudiant (par le RS)** :
    - **Contexte** : Pour des inscriptions tardives ou des cas non couverts par l'import initial de l'Admin Système.
    - **Formulaire** : Saisie des informations de la table etudiant (numero_carte_etudiant unique, nom, prenom, date_naissance, adresse, contacts, etc.). Le champ etudiant.numero_utilisateur n'est pas saisi ici ; il sera lié lors de la génération du compte.
    - **Logique** (appel à une méthode de ServiceAuthentification ou service dédié, ex: creerProfilEtudiantSeul) :
      - Validation des données (unicité numero_carte_etudiant).
      - INSERT INTO etudiant (numero_carte_etudiant, nom, prenom,..., numero_utilisateur) VALUES (?,?,..., NULL);
      - Journalisation dans enregistrer (id_action = 'ACTION_CREATE_PROFIL_ETUD_RS', type_entite_concernee = 'ETUDIANT', id_entite_concernee = numero_carte_etudiant).
    - **Note** : Cette action par le RS crée uniquement le profil etudiant. Le compte utilisateur sera généré séparément via l'onglet I une fois tous les prérequis (scolarité à jour ET stage enregistré) remplis.
  - **F.4. Modification des Informations Administratives d'un Étudiant** :
    - Le RS peut modifier la plupart des champs de etudiant (ex: adresse_postale, telephone, contact_urgence_nom, email_contact_secondaire). La modification du nom, prenom, date_naissance, numero_carte_etudiant est généralement réservée à l'Admin Système ou nécessite une procédure de validation plus stricte avec justificatifs.
    - **Logique SQL** : UPDATE etudiant SET... WHERE numero_carte_etudiant =?;. Journalisation détaillée dans enregistrer.

##### **G. Onglet: Inscriptions** <sup>1</sup>

- **Objectif** : Gérer le processus d'inscription administrative et pédagogique des étudiants pour chaque année académique.
- **Interface et Fonctionnalités** (similaires au Module Administration E.1 et B.1.7) :
  - **G.1. Sélection de l'Étudiant** : Champ de recherche pour trouver un etudiant par numero_carte_etudiant ou nom/prénom.
  - **G.2. Affichage de l'Historique des Inscriptions de l'Étudiant Sélectionné** :
    - Tableau listant ses inscriptions passées et actuelles (depuis inscrire), avec libelle_annee_academique, libelle_niveau_etude, date_inscription, montant_inscription, libelle_statut_paiement, date_paiement, numero_recu_paiement (unique si renseigné), libelle_decision_passage.
  - **G.3. Ajout d'une Nouvelle Inscription (pour l'étudiant sélectionné)** :
    - **Formulaire** :
      - Choix id_annee_academique (liste déroulante des annee_academique, souvent l'année active par défaut).
      - Choix id_niveau_etude (liste déroulante des niveau_etude).
      - Saisie montant_inscription (DECIMAL).
      - date_inscription (DATETIME, aujourd'hui par défaut).
      - Choix id_statut_paiement (VARCHAR(50) FK vers statut_paiement_ref, souvent 'PAIE_NOK' ou un statut "En attente de paiement" par défaut).
      - Champs optionnels : date_paiement (DATETIME), numero_recu_paiement (VARCHAR(50), doit être unique dans la table inscrire si renseigné), id_decision_passage (VARCHAR(50) FK vers decision_passage_ref, pour les réinscriptions).
    - **Logique** (via ServiceGestionAcademique.creerInscriptionAdministrative) :
      - Validation (pas de double inscription au même niveau/année pour le même étudiant ; unicité de numero_recu_paiement si fourni).
      - INSERT INTO inscrire. Journalisation dans enregistrer.
  - **G.4. Modification d'une Inscription Existante** :
    - Principalement pour mettre à jour id_statut_paiement (ex: de 'PAIE_NOK' à 'PAIE_OK quand le paiement est confirmé par le RS), date_paiement, numero_recu_paiement.

\* Enregistrer/modifier id_decision_passage en fin d'année.

\* Logique (via ServiceGestionAcademique.mettreAJourInscriptionAdministrative) : UPDATE inscrire SET... WHERE numero_carte_etudiant =? AND id_niveau_etude =? AND id_annee_academique =?;. Journalisation.

\* Impact : La mise à jour de id_statut_paiement à 'PAIE_OK' (ou un équivalent "Payé/Exonéré") pour l'année académique active est l'un des prérequis, avec le stage enregistré, pour que le Responsable Scolarité puisse générer le compte utilisateur de l'étudiant via l'onglet I. 1

##### H. Onglet: Gestion des Stages <sup>1</sup>

- **Objectif** : Enregistrer et valider les informations de stage des étudiants. Cet enregistrement est un des prérequis pour l'accès à la plateforme et la soumission du contenu du rapport. Les informations sont basées sur des justificatifs physiques fournis par l'étudiant (ex: convention de stage signée) et saisies manuellement par le RS.
- **Interface et Fonctionnalités** :
  - **H.1. Sélection de l'Étudiant** :
    - **Interface** : Champ de recherche (texte libre ou auto-complétion) pour trouver l'étudiant par numero_carte_etudiant ou nom/prénom.
    - **Interaction** : Une fois l'étudiant sélectionné, son nom et numéro de carte sont affichés en en-tête, et le tableau des stages (H.2) est filtré.
  - **H.2. Affichage des Stages Enregistrés pour l'Étudiant Sélectionné** :
    - **Interface** : Tableau des faire_stage de l'étudiant.
    - **Colonnes** : libelle_entreprise (via id_entreprise et jointure sur entreprise), date_debut_stage, date_fin_stage, sujet_stage (extrait), nom_tuteur_entreprise.
    - **Actions par Ligne** : "Modifier ce Stage", "Supprimer ce Stage".
  - **H.3. Ajout/Enregistrement d'un Nouveau Stage (par le RS)** :
    - **Déclenchement** : Bouton "Ajouter un Nouveau Stage".
    - **Interface du Formulaire** :
      - id_entreprise (VARCHAR(50) FK vers entreprise) : Liste déroulante des entreprise.libelle_entreprise. Si l'entreprise n'existe pas, le RS doit demander à l'Admin Système de l'ajouter (via D.1.8 du Module Admin). Le RS ne crée pas d'entreprise. Validation : Sélection obligatoire. <sup>1</sup>
      - date_debut_stage (DATE) : Sélecteur de date. Validation : Obligatoire. <sup>1</sup>
      - date_fin_stage (DATE, optionnel si en cours) : Sélecteur de date. Validation : Si renseignée, doit être > date_debut_stage. <sup>1</sup>
      - sujet_stage (TEXT) : Zone de texte. Validation : Obligatoire. <sup>1</sup>
      - nom_tuteur_entreprise (VARCHAR(100)) : Champ texte. Validation : Obligatoire. <sup>1</sup>
    - **Logique Algorithmique/SQL** (via ServiceGestionAcademique.enregistrerInformationsStage) :
            1. Validation des données (cohérence dates, étudiant inscrit pour l'année du stage).
            2. INSERT INTO faire_stage (id_entreprise, numero_carte_etudiant, date_debut_stage, date_fin_stage, sujet_stage, nom_tuteur_entreprise) VALUES (?,?,?,?,?,?);
            3. Journalisation dans enregistrer (id_action = 'ACTION_ENREG_STAGE_RS').
            4. Message de succès/erreur. Rafraîchissement du tableau H.2.
    - **Impact** : Cet enregistrement valide le prérequis "Stage Effectué" pour la génération du compte étudiant. <sup>1</sup>
  - **H.4. Modification des Informations d'un Stage** :
    - **Déclenchement** : Clic sur "Modifier ce Stage" (H.2).
    - **Interface** : Formulaire similaire à H.3, pré-rempli.
    - **Champs Modifiables** : Dates, sujet, tuteur, entreprise (si erreur de saisie).
    - **Logique Algorithmique/SQL** (via ServiceGestionAcademique.mettreAJourInformationsStage) :
            1. Validation des modifications.
            2. UPDATE faire_stage SET... WHERE id_entreprise =? AND numero_carte_etudiant =?; (clause WHERE basée sur PK composite).
            3. Journalisation détaillée dans enregistrer (id_action = 'ACTION_MODIF_STAGE_RS', anciennes/nouvelles valeurs).
            4. Message et rafraîchissement.
  - **H.5. Suppression d'un Enregistrement de Stage (Fonctionnalité Conditionnelle)** :
    - **Cas d'Usage** : Uniquement si stage enregistré par erreur manifeste et SANS impact sur compte étudiant déjà activé ou rapport soumis.
    - **Déclenchement** : Bouton "Supprimer ce Stage".
    - **Workflow** :
            1. Confirmation forte.
            2. Vérification des dépendances serveur : rapport_etudiant lié à l'année du stage, utilisateur.statut_compte de l'étudiant (si déjà activé grâce à ce stage).
            3. Si dépendances, suppression bloquée.
            4. Logique SQL : DELETE FROM faire_stage WHERE id_entreprise =? AND numero_carte_etudiant =?;. Journalisation (id_action = 'ACTION_SUPPR_STAGE_RS').
            5. Message et rafraîchissement.

##### I. Onglet: Génération Comptes Étudiants <sup>1</sup>

- **Objectif** : Permettre au RS de générer les comptes utilisateurs (utilisateur) pour les étudiants qui remplissent les conditions d'accès : scolarité à jour ET stage enregistré.
- **Interface et Fonctionnalités** :
  - **I.1. Liste des Étudiants Éligibles à la Création/Activation de Compte** :
    - **Interface** : Tableau listant les étudiants (numero_carte_etudiant, nom, prenom) remplissant les critères.
    - **Logique de Requête (Complexe)** :

            1. Inscription active (annee_academique.est_active = 1).
            2. Statut de paiement OK (inscrire.id_statut_paiement = 'PAIE_OK').
            3. Stage enregistré (faire_stage pour l'année active/pertinente).
            4. etudiant.numero_utilisateur est NULL OU utilisateur.statut_compte lié indique une création non finalisée (ex: 'creation_en_attente_par_RS').

      - _Exemple SQL simplifié_ :  
                SQL  
                SELECT e.numero_carte_etudiant, e.nom, e.prenom  
                FROM etudiant e  
                JOIN inscrire i ON e.numero_carte_etudiant = i.numero_carte_etudiant  
                JOIN annee_academique aa ON i.id_annee_academique = aa.id_annee_academique  
                JOIN faire_stage fs ON e.numero_carte_etudiant = fs.numero_carte_etudiant  
                WHERE aa.est_active = 1 AND i.id_statut_paiement = 'PAIE_OK'  
                AND fs.date_debut_stage <= CURDATE() -- Stage commencé  
                AND (e.numero_utilisateur IS NULL OR  
                (SELECT u.statut_compte FROM utilisateur u WHERE u.numero_utilisateur = e.numero_utilisateur)  
                IN ('creation_en_attente_par_RS', 'jamais_connecte_apres_creation_profil'))  
                GROUP BY e.numero_carte_etudiant, e.nom, e.prenom;  

    - **Interaction** : Case à cocher par ligne ou bouton "Générer Compte".
  - **I.2. Action par Ligne ou en Masse: "Générer et Activer Compte Utilisateur"** :
    - **Déclenchement** : Sélection et clic sur bouton "Générer et Activer Compte(s) Utilisateur".
    - **Workflow Algorithmique/SQL** (appel à ServiceAuthentification.genererEtActiverCompteEtudiantPourRS) :
            1. Confirmation par le RS.
            2. Pour chaque étudiant sélectionné :
                - Re-vérification finale des prérequis. Si non remplis, ignorer et loguer.
                - **Gestion numero_utilisateur** :

Si etudiant.numero_utilisateur est NULL : Générer numero_utilisateur unique (ex: "USR_ETU_" + UUID). UPDATE etudiant SET numero_utilisateur =? WHERE numero_carte_etudiant =?;.

Sinon, utiliser etudiant.numero_utilisateur existant.

- - - - - Générer login_utilisateur unique (ex: prenom.nom, avec résolution de conflits).
                - Assigner utilisateur.email_principal (ex: etudiant.email_contact_secondaire).
                - Générer mot de passe initial sécurisé (haché).
                - **Préparation données utilisateur** : id_type_utilisateur = 'TYPE_ETUD', id_groupe_utilisateur = 'GRP_ETUDIANT', id_niveau_acces_donne (défaut étudiant), statut_compte = 'actif' (ou 'en_attente_validation' si validation email requise), email_valide (0 ou 1), token_validation_email (si email_valide=0), date_creation = NOW().
                - **Opération BDD** :

Si compte utilisateur existant (finalisation) : UPDATE utilisateur SET... WHERE numero_utilisateur =?;.

Sinon (nouveau compte) : INSERT INTO utilisateur (...) VALUES (...);.

- - - - - Journalisation dans enregistrer (id_action = 'ACTION_GEN_COMPTE_ETUD_RS').
                - Envoi email d'activation/bienvenue (via ServiceEmail appelé par ServiceNotification) avec login, MDP (ou lien de définition), URL. Création recevoir pour notif interne.

            1. Message de succès global au RS.
            2. Actualisation de la liste I.1.

##### J. Onglet: Notes et Évaluations <sup>1</sup>

- **Objectif** : Permettre au RS de saisir des notes (si habilité, ex: pour évaluations spécifiques ou en cas d'absence d'enseignant) ou de consulter les notes pour vérifications administratives ou préparation de documents. L'habilitation est contrôlée par traitement.
- **Interface et Fonctionnalités** :
  - **J.1. Sélection Étudiant / ECUE / Année Académique** :
    - **Interface** : Listes déroulantes/champs de recherche pour cibler la note.
  - **J.2. Formulaire de Saisie/Modification de Note (evaluer.note)** :
    - **Déclenchement** : Bouton "Saisir Nouvelle Note" ou "Modifier Note".
    - **Interface Formulaire** : numero_carte_etudiant (lecture seule), id_ecue (sélectionnable), numero_enseignant évaluateur (liste déroulante), date_evaluation (sélecteur date/heure), note (numérique, 0-20).
    - **Logique Algorithmique/SQL** (via ServiceGestionAcademique.enregistrerNoteEcue ou MàJ) :
            1. Validation des données.
            2. Vérification unicité (pour nouvelle note) sur PK composite (numero_carte_etudiant, numero_enseignant, id_ecue).
            3. Vérification période de saisie des notes (si configurée en E.2.2 du Module Admin).
            4. Transaction BDD : INSERT INTO evaluer ou UPDATE evaluer. Journalisation rigoureuse dans enregistrer (id_action = 'ACTION_SAISIE_NOTE_RS' ou ACTION_MODIF_NOTE_RS).
            5. Message et rafraîchissement.
  - **J.3. Consultation des Notes d'un Étudiant** :
    - **Interface** : Tableau des notes de l'étudiant (filtré par année/UE).
    - **Colonnes** : libelle_ecue, libelle_ue, note, date_evaluation, nom_evaluateur.
    - **Calculs (Optionnel)** : Moyennes par UE/générale.
    - **Action par Ligne** : "Modifier cette Note".

##### K. Onglet: Génération de Documents PDF Officiels <sup>1</sup>

- **Objectif** : Permettre au RS de générer à la demande des documents administratifs courants pour les étudiants (attestations de scolarité, reçus de paiement, relevés de notes) au format PDF.
- **Interface et Fonctionnalités** :
  - **K.1. Sélection de l'Étudiant** :
    - **Interface** : Champ de recherche (numero_carte_etudiant ou nom/prénom).
  - **K.2. Sélection du Type de Document PDF à Générer** :
    - **Interface** : Liste déroulante des modèles de documents pertinents pour le RS (habilitations via traitement et rattacher).
    - **Exemples** : "Attestation de Scolarité (Année Active)", "Relevé de Notes (par Année/Semestre)", "Reçu de Paiement Frais d'Inscription".
  - **K.3. Bouton "Générer et Télécharger le Document PDF"** :
    - **Déclenchement** : Clic après sélections.
    - **Logique Algorithmique/SQL** (appel à ServiceDocumentGenerator.genererDocumentPDF) :
            1. Appel du service avec type de document (code modèle) et numero_carte_etudiant (et année si contextuel).
            2. Récupération du template HTML/CSS (configuré par Admin Système en D.3.1).
            3. Collecte des données dynamiques (etudiant, inscrire, evaluer, etc.) via services métier.
            4. Fusion données et template (remplacement placeholders).
            5. Génération PDF via librairie (Dompdf, TCPDF).
            6. Téléchargement proposé au RS.
            7. Stockage optionnel du PDF généré (document_officiel_genere) et journalisation dans enregistrer (id_action = 'ACTION_GEN_DOC_PDF_RS').

#### Partie IV : Fonctionnalités Communes au Personnel Administratif (Référence) <sup>1</sup>

Les fonctionnalités suivantes sont accessibles de manière similaire par l'Agent de Contrôle de Conformité et le Responsable Scolarité, avec un contexte adapté à leur rôle.

##### D. Messagerie Interne <sup>1</sup>

- **Objectif** : Faciliter la communication et la coordination avec les étudiants, les autres membres du personnel, et potentiellement les membres de la commission.
- **Interface et Fonctionnalités** (gérées par ServiceMessagerie.php) :
  - **D.1. Liste des Conversations** : Affiche les conversations (conversation) où l'agent est participant_conversation. Tri par date dernier message. Indicateur de messages non lus.
  - **D.2. Interface de Chat pour une Conversation Sélectionnée** :
    - Affichage des message_chat (avec contenu_message, numero_utilisateur_expediteur, date_envoi).
    - Champ de saisie pour envoyer un nouveau message.
    - Marquage automatique des messages comme lus (recevoir.lue = 1) lors de l'ouverture de la conversation.
  - **D.3. Démarrer une Nouvelle Conversation** :
    - Recherche d'utilisateurs (utilisateur) pour initier une conversation directe ou créer un groupe.
- **Logique** : Implique les tables conversation, participant_conversation, message_chat, recevoir. Les actions sont journalisées.

##### E. Mon Profil <sup>1</sup>

- **Objectif** : Permettre à l'agent de consulter et de modifier ses propres informations de compte et de profil.
- **Interface et Fonctionnalités** :
  - **E.1. Consultation des Informations Personnelles et Professionnelles** (issues de personnel_administratif) :
    - Champs en lecture seule : numero_personnel_administratif, nom, prenom, date_affectation_service.
    - Champs modifiables : telephone_professionnel, email_professionnel (avec revalidation si email_principal est lié), adresse_postale, telephone_personnel.
  - **E.2. Gestion du Compte Utilisateur** (issues de utilisateur) :
    - login_utilisateur (lecture seule).
    - email_principal (modifiable, avec revalidation).
    - Modification du mot de passe (formulaire : ancien MDP, nouveau MDP, confirmation). Logique via ServiceAuthentification.modifierMotDePasseUtilisateur.
    - Gestion photo_profil.
    - Préférences de notification (si utilisateur.preferences_notifications JSON).
    - Gestion 2FA (activation/désactivation, codes de secours).
- **Logique** : UPDATE personnel_administratif ou UPDATE utilisateur. Journalisation dans enregistrer.

#### Tables SQL Primordialement Impliquées pour le Module Personnel Administratif (Synthèse) <sup>1</sup>

- **Profils et Comptes Agents** : personnel_administratif, utilisateur. <sup>1</sup>
- **Droits et Rôles Agents** : groupe_utilisateur, rattacher, traitement. <sup>1</sup>
- **Gestion Conformité (Agent Conformité)** : rapport_etudiant, statut_rapport_ref, approuver, statut_conformite_ref, etudiant, document_soumis (pour lire contenu_textuel), type_document_ref. <sup>1</sup>
- **Gestion Étudiants (RS)** : etudiant, utilisateur. <sup>1</sup>
- **Gestion Inscriptions (RS)** : inscrire, annee_academique, niveau_etude, statut_paiement_ref, decision_passage_ref. <sup>1</sup>
- **Gestion Stages (RS)** : faire_stage, entreprise. <sup>1</sup>
- **Gestion Notes (RS, si habilité)** : evaluer, ecue, ue, enseignant. <sup>1</sup>
- **Communication** : conversation, message_chat, participant_conversation, recevoir, notification. <sup>1</sup>
- **Audit** : enregistrer. <sup>1</sup>
- **Référentiels Consultés** : Nombreuses tables \_ref. <sup>1</sup>
- **Génération PDF** : (Indirectement) modeles_pdf_config (conceptuelle), et toutes les tables sources de données. <sup>1</sup>

## Partie III : Module Étudiant <sup>1</sup>

Le Module Étudiant de "GestionMySoutenance" est l'interface personnalisée et sécurisée pour chaque étudiant engagé dans le processus de rédaction et de validation de son rapport.

### A. Introduction et Objectifs du Module Étudiant <sup>1</sup>

- **Objectif Général** : Centraliser informations et actions relatives au parcours de l'étudiant (saisie/soumission du contenu du rapport, suivi, communication, accès aux ressources et documents PDF). <sup>1</sup>
- **Conditions d'Accès** : Compte utilisateur généré par le Responsable Scolarité après vérification de prérequis stricts : scolarité à jour (inscrire.id_statut_paiement = 'Payé/Exonéré' pour l'année active) ET stage effectué et enregistré (faire_stage validé). <sup>1</sup>
- **Processus de Génération de Compte** : Le RS initie la création. ServiceAuthentification crée l'enregistrement utilisateur (id_type_utilisateur = 'TYPE_ETUD'), met à jour etudiant.numero_utilisateur. Email envoyé à utilisateur.email_principal avec identifiants/lien de définition MDP. <sup>1</sup>
- **Environnement Fermé** : L'étudiant ne téléverse aucun fichier pour son rapport. Tout le contenu (texte, résumé, bibliographie) est saisi via des formulaires et éditeurs de texte enrichi. <sup>1</sup>

### B. Interface Utilisateur Principale (Header, Sidebar) <sup>1</sup>

- **Header Proposé** : "Mon Espace MySoutenance - \[Nom Prénom Étudiant\]". Affiche logo, nom étudiant, lien "Mon Profil", indicateur notifications non lues, bouton déconnexion, année académique active. <sup>1</sup>
- **Sidebar Dynamique** :
  - A. Tableau de Bord
  - B. Mon Profil
  - C. Mon Rapport
  - D. Mes Documents PDF
  - E. Mes Réclamations
  - F. Ressources & Aide <sup>1</sup>

### C. Fonctionnalités Détaillées par Onglet

#### A. Onglet: Tableau de Bord Étudiant <sup>1</sup>

- **Objectif** : Vue d'ensemble immédiate des informations pertinentes et actions requises.
- **Contenu et Widgets** :
  - **A.1. Statut Actuel de Mon Rapport** : Affiche libelle_statut_rapport (de rapport_etudiant via statut_rapport_ref) pour l'année active. Lien vers "Mon Rapport" (C). <sup>1</sup>
  - **A.2. Notifications Récentes Non Lues** : Liste des 3-5 dernières recevoir.lue = 0 (avec notification.libelle_notification, recevoir.date_reception). Lien "Voir toutes les notifications". <sup>1</sup>
  - **A.3. Alertes et Actions Requises** : Messages contextuels basés sur rapport_etudiant.id_statut_rapport (ex: "Corrections demandées. Date limite : \[date\]"). <sup>1</sup>
  - **A.4. Raccourcis Rapides (Optionnel)** : "Soumettre mon rapport", "Consulter mes notes (PDF)", "Faire une réclamation". <sup>1</sup>

#### B. Onglet: Mon Profil <sup>1</sup>

- **Objectif** : Consulter et modifier (si autorisé) les informations personnelles et de compte.
- **Contenu et Fonctionnalités** :
  - **B.1. Consultation des Informations Personnelles (etudiant)** :
    - Affichage (lecture seule pour la plupart) : numero_carte_etudiant, nom, prenom, date_naissance, lieu_naissance, pays_naissance, nationalite, sexe, adresse_postale, ville, code_postal.
    - Champs Modifiables par l'Étudiant : telephone, email_contact_secondaire (format email), contact_urgence_nom, contact_urgence_telephone, contact_urgence_relation. <sup>1</sup>
  - **B.2. Gestion du Compte Utilisateur (utilisateur)** :
    - login_utilisateur (lecture seule).
    - email_principal (modifiable, avec revalidation obligatoire : utilisateur.email_valide -> 0, nouveau token_validation_email généré, email de validation envoyé).
    - Modification Mot de Passe : Formulaire (Ancien MDP, Nouveau MDP, Confirmer Nouveau MDP). Logique via ServiceAuthentification.modifierMotDePasseUtilisateur. Enregistrement dans historique_mot_de_passe.
    - Gestion photo_profil (affichage, upload, suppression).
    - Préférences de Notification (si utilisateur.preferences_notifications JSON). <sup>1</sup>
  - **Workflow de Modification** : Validation client/serveur. UPDATE etudiant ou UPDATE utilisateur. Enregistrement dans enregistrer. Confirmation. <sup>1</sup>

#### C. Onglet: Mon Rapport <sup>1</sup>

- **Objectif** : Interface centrale pour la saisie, soumission, suivi et gestion des corrections du contenu du rapport.
- **État Initial (si aucun rapport soumis)** : Message "Vous n'avez pas encore soumis de rapport...". Bouton "Soumettre Mon Rapport de Stage" (actif si prérequis remplis). Affichage des directives de soumission. <sup>1</sup>
- **C.1. Soumission Initiale du Contenu du Rapport** :
  - **Déclenchement** : Bouton "Soumettre Mon Rapport de Stage".
  - **Interface Formulaire (Saisie Textuelle)** :
    - Champs Métadonnées (rapport_etudiant) : libelle_rapport_etudiant (titre), theme, resume (éditeur riche), numero_attestation_stage, nombre_pages (déclaré). id_annee_academique (auto, non modifiable).
    - Champs Contenu Rapport (document_soumis.contenu_textuel) : Pour chaque type_document_ref requis (ex: 'DOC_RAP_MAIN', 'DOC_INTRO'), une zone de texte avec éditeur riche.
    - Case à cocher "Je confirme que ces informations sont mon travail original...". <sup>1</sup>
  - **Règles Métier & Validations** : Champs obligatoires, contenu non vide pour sections requises, nombre_pages positif. Pas de soumission multiple pour l'année active (sauf si reprise après refus). <sup>1</sup>
  - **Logique Algorithmique/SQL** (via ServiceRapport.creerEtSoumettreRapportTextuel) :
        1. Validation serveur.
        2. Génération id_rapport_etudiant unique.
        3. INSERT INTO rapport_etudiant (id_statut_rapport = 'RAP_SOUMIS', date_soumission = NOW()).
        4. Pour chaque section de contenu : INSERT INTO document_soumis (id_rapport_etudiant lié, id_type_document, contenu_textuel, version = 1, date_soumission_version = NOW(), numero_utilisateur_soumission).
        5. Journalisation (enregistrer, id_action = "SOUMISSION_CONTENU_RAPPORT").
        6. Transaction BDD. <sup>1</sup>
  - **Interactions & Post-Soumission** : Interface de soumission verrouillée. Notifications à l'étudiant (accusé) et à l'Agent de Conformité. <sup>1</sup>
- **C.2. Suivi du Processus de Validation (si rapport soumis)** :
  - **Interface** : Statut actuel détaillé (libelle_statut_rapport). Historique des statuts (si historique_statut_rapport existe). Commentaires des validateurs (approuver.commentaire_conformite si 'RAP_NON_CONF', compte_rendu.libelle_compte_rendu si 'RAP_CORRECT' par commission). Contenu soumis (lecture seule des document_soumis.contenu_textuel, dernière version). <sup>1</sup>
- **C.3. Gestion des Corrections du Contenu (si id_statut_rapport = 'RAP_NON_CONF' ou 'RAP_CORRECT')** :
  - **Interface** : Affichage des motifs/commentaires. Formulaire similaire à C.1, pré-rempli avec contenu_textuel version actuelle. Champ "Note expliquant les modifications apportées". <sup>1</sup>
  - **Logique Algorithmique/SQL** (via ServiceRapport.soumettreCorrectionsRapportTextuel) :
        1. Validation.
        2. Pour chaque section modifiée : INSERT INTO document_soumis (même id_rapport_etudiant, id_type_document, mais version incrémentée et nouveau contenu_textuel).
        3. UPDATE rapport_etudiant (métadonnées, date_derniere_modif = NOW(), id_statut_rapport -> 'RAP_CORRECT_SOUMISES_CONF' ou 'RAP_CORRECT_SOUMISES_COMM').
        4. Note explicative stockée (ex: document_soumis type 'DOC_NOTE_CORRECTION').
        5. Journalisation. Notification à l'instance concernée. Interface verrouillée. <sup>1</sup>
- **C.4. Cas: Rapport Non Validé par la Commission (id_statut_rapport = 'RAP_REFUSE')** :
  - **Interface** : Affichage décision refus et motifs/recommandations du PV.
    - Option 1 : "Modifier le contenu de mon rapport actuel et le resoumettre." -> Interface C.3 active. id_statut_rapport -> 'RAP_REFUSE_MODIF_EN_COURS'.
    - Option 2 : "Reprendre tout le processus de soumission (implique un nouveau stage ou revalidation)." -> Message : "Pour reprendre..., veuillez soumettre une réclamation via 'Mes Réclamations'...". rapport_etudiant.id_statut_rapport (refusé) -> 'RAP_REFUSE_ARCHIVE'. Interface C.1 verrouillée jusqu'à traitement réclamation et validation nouveau faire_stage par RS. <sup>1</sup>
- **C.5. Cas: Rapport Validé par la Commission (id_statut_rapport = 'RAP_VALID')** :
  - **Interface** : Message de félicitations. Affichage du PV. Lien vers "Mes Documents PDF" (D). Verrouillage total des actions de soumission/modification. <sup>1</sup>

#### D. Onglet: Mes Documents PDF <sup>1</sup>

- **Objectif** : Permettre à l'étudiant de télécharger les documents PDF officiels générés par le système le concernant.
- **Interface et Fonctionnalités** :
  - **D.1. Liste des Documents PDF Disponibles** : Tableau "Nom du Document", "Date de Génération", "Action". Exemples : "Attestation de Dépôt de Rapport", "Procès-Verbal de Validation", "Bulletin de Notes", "Attestation de Scolarité". <sup>1</sup>
  - **Logique** : Documents générés par ServiceDocumentGenerator (appelé par autres services/Admin/RS). Accès lecture seule. Stockés dans document_officiel_genere ou générés à la volée. <sup>1</sup>
  - **D.2. Téléchargement** : Bouton "Télécharger (PDF)". <sup>1</sup>

#### E. Onglet: Mes Réclamations <sup>1</sup>

- **Objectif** : Canal formel pour requêtes, signalements, ou demande de reprise de processus avec nouveau stage.
- **Interface et Fonctionnalités** (gérées par ServiceReclamation) :
  - **E.1. Soumission d'une Nouvelle Réclamation** :
    - Bouton "Faire une Nouvelle Réclamation".
    - Formulaire : sujet_reclamation\*, id_type_reclamation\* (liste déroulante : "Problème Technique", "Question Statut Rapport", "Demande Reprise Processus Rapport (Nouveau Stage)", etc.), description_reclamation\* (éditeur de texte).
    - Section Spécifique si id_type_reclamation = "DEM_REPRISE_STAGE" : Case à cocher "Je confirme vouloir reprendre... avec nouveau stage"\*. Options : "En ligne (infos préliminaires)" (champs : nouvelle entreprise, dates, sujet) OU "En présentiel uniquement". L'étudiant ne téléverse PAS de convention. <sup>1</sup>
    - **Workflow Soumission Réclamation** :
            1. Validation. INSERT INTO reclamation (statut 'RECLAM_RECUE').
            2. Si "DEM_REPRISE_STAGE" et option "présentiel" : ServiceReclamation peut notifier ServiceAuthentification pour changer utilisateur.statut_compte à 'SUSPENDU_ATTENTE_RS_STAGE' (bloque C.1).
            3. Journalisation. Notification à l'étudiant (accusé) et au service concerné (RS pour "DEM_REPRISE_STAGE"). <sup>1</sup>
  - **E.2. Suivi des Réclamations Soumises** : Tableau des reclamation (id_reclamation, sujet_reclamation, date_soumission, libelle_statut_reclamation, date_reponse). Action "Voir Détails" (affiche description_reclamation, reponse_reclamation). <sup>1</sup>

#### F. Onglet: Ressources & Aide <sup>1</sup>

- **Objectif** : Fournir documents utiles (guides rédaction, modèles plan rapport texte/markdown), FAQ, contacts.
- **Contenu** :
  - **F.1. Guides et Modèles** : Guide officiel rédaction (HTML ou lien PDF externe). Modèles plan, page de garde (texte structuré). Critères d'évaluation (texte). <sup>1</sup>
  - **F.2. Foire Aux Questions (FAQ)**. <sup>1</sup>
  - **F.3. Contacts Utiles**. <sup>1</sup>

## Partie IV : Module Commission de Validation <sup>1</sup>

Le Module Commission de Validation est l'interface sécurisée pour les membres de la commission pédagogique, leur permettant d'évaluer le contenu des rapports étudiants, de délibérer, de prendre des décisions collectives, de formaliser l'encadrement et de produire les procès-verbaux (PV) officiels. <sup>1</sup>

### A. Introduction et Objectifs du Module Commission <sup>1</sup>

- **Objectif Général** : Permettre l'évaluation approfondie du contenu des rapports (après vérification de conformité), faciliter la délibération et la prise de décision, formaliser l'encadrement, et assurer la production des PV, garantissant rigueur, transparence et traçabilité. <sup>1</sup>
- **Rôles et Accès** : Membres de la commission (enseignants avec id_groupe_utilisateur = 'GRP_COMMISSION'). Le Président peut avoir des droits étendus (planification sessions, validation finale PV). Accès sécurisé par ServiceAuthentification.php. <sup>1</sup>
- **Contexte du Processus** : Intervient après que le rapport (contenu textuel et métadonnées) a été jugé conforme par l'Agent de Contrôle de Conformité. <sup>1</sup>

### B. Interface Utilisateur Principale (Header, Sidebar) <sup>1</sup>

- **Header Proposé** : "Espace Commission MySoutenance - \[Nom Commission si applicable\] - \[Nom Prénom Membre\]". Affiche logo, nom membre, lien "Mon Profil", indicateur notifications non lues, bouton déconnexion, année académique active. <sup>1</sup>
- **Sidebar Dynamique** :
  - A. Tableau de Bord Commission
  - B. Rapports à Traiter/Évaluer
  - C. Gestion des Procès-Verbaux (PV)
  - D. Gestion des Corrections (Post-Commission)
  - E. Communication & Concertation
  - F. Historique & Archives (Commission)
  - G. Mon Profil (commun) <sup>1</sup>

### C. Fonctionnalités Détaillées par Onglet

#### A. Onglet: Tableau de Bord Commission <sup>1</sup>

- **Objectif** : Aperçu personnalisé des tâches en attente, rapports nécessitant attention, notifications pertinentes.
- **Contenu et Widgets** :
  - **A.1. Rapports en Attente d'Examen/Vote pour Moi** : Nombre de rapport_etudiant assignés (si assignation individuelle) ou en attente de vote par la commission et pour lesquels le membre n'a pas encore voté. Lien vers "Rapports à Évaluer" (B). <sup>1</sup>
    - _Logique SQL (simplifiée)_ : SELECT COUNT(DISTINCT r.id_rapport_etudiant) FROM rapport_etudiant r JOIN affecter aff ON r.id_rapport_etudiant = aff.id_rapport_etudiant LEFT JOIN vote_commission vc ON r.id_rapport_etudiant = vc.id_rapport_etudiant AND vc.numero_enseignant = WHERE r.id_statut_rapport = 'RAP_EN_COMM' AND i.id_annee_academique = AND aff.numero_enseignant = AND vc.id_vote IS NULL; <sup>1</sup>
  - **A.2. Procès-Verbaux (PV) en Attente de Ma Validation/Action** : Nombre de compte_rendu soumis à validation pour lesquels le membre n'a pas encore enregistré sa décision (si vote sur PV), ou PV qu'il doit rédiger. Lien vers "Procès-Verbaux" (C). <sup>1</sup>
    - _Logique SQL (pour PV à valider)_ : SELECT COUNT(DISTINCT cr.id_compte_rendu) FROM compte_rendu cr LEFT JOIN validation_pv vp ON cr.id_compte_rendu = vp.id_compte_rendu AND vp.numero_enseignant = WHERE cr.id_statut_pv = 'PV_SOUMIS_VALID' AND vp.id_decision_validation_pv IS NULL; <sup>1</sup>
  - **A.3. Notifications Récentes de la Commission** : Liste des 3-5 dernières recevoir pour les membres de la commission ou cet utilisateur. <sup>1</sup>
  - **A.4. Mes Tâches Spécifiques (si applicable)** : Si rôle particulier (Président, Rapporteur désigné, Rédacteur PV désigné). Ex: "PV à rédiger: X". <sup>1</sup>

#### B. Onglet: Rapports à Évaluer <sup>1</sup>

- **Objectif** : Interface principale pour consulter les rapports soumis à la commission, participer au vote, formaliser l'encadrement.
- **Contenu et Fonctionnalités** :
  - **B.1. Liste des Rapports Transmis à la Commission** :
    - **Interface** : Tableau paginé des rapport_etudiant avec id_statut_rapport = 'RAP_CONF' ou 'RAP_EN_COMM'.
    - **Colonnes** : id_rapport_etudiant, Nom & Prénom Étudiant, libelle_rapport_etudiant (titre), theme, date_soumission, date transmission commission. État du vote pour ce rapport.
    - **Filtres** : Par année académique, statut de vote.
    - _Logique SQL_ : SELECT r.\*, etu.nom, etu.prenom, srr.libelle_statut_rapport FROM rapport_etudiant r JOIN etudiant etu ON r.numero_carte_etudiant = etu.numero_carte_etudiant JOIN statut_rapport_ref srr ON r.id_statut_rapport = srr.id_statut_rapport JOIN inscrire i ON r.numero_carte_etudiant = i.numero_carte_etudiant WHERE r.id_statut_rapport IN ('RAP_CONF', 'RAP_EN_COMM') AND i.id_annee_academique = ORDER BY r.date_soumission ASC; <sup>1</sup>
  - **B.2. Action par Ligne: "Consulter et Évaluer le Rapport"** : Mène à une interface détaillée (WORKFLOW_EVALUATION_RAPPORT). <sup>1</sup>
- **Workflow: Évaluation d'un Rapport et Processus de Vote (WORKFLOW_EVALUATION_RAPPORT)** <sup>1</sup>
  - **Accès** : Via action "Consulter et Évaluer le Rapport". id_rapport_etudiant en paramètre.
  - **Interface Détaillée d'Évaluation** :
    - **Section 1 : Informations du Rapport et de l'Étudiant** : Données de rapport_etudiant et etudiant. <sup>1</sup>
    - **Section 2 : Consultation du Contenu du Rapport (TEXTUEL)** : Affichage contenu_textuel de chaque document_soumis (dernière version). Les membres lisent directement. <sup>1</sup>
    - **Section 3 : Espace de Vote en Ligne** (si dématérialisé) :
      - Affichage État du Vote Actuel : Qui a voté, leur vote (si visible), commentaires de vote (vote_commission.commentaire_vote), tour de vote actuel (vote_commission.tour_vote). <sup>1</sup>
      - Interface de Vote pour Membre Connecté (s'il n'a pas voté pour ce tour) :
        - Options Décision (Boutons Radio, issues de decision_vote_ref) : 'DV_APPROUVE', 'DV_REFUSE', 'DV_CORRECTIONS' (à ajouter à decision_vote_ref), 'DV_DISCUSSION'. <sup>1</sup>
        - Champ commentaire_vote (TEXT, dans vote_commission) : Obligatoire si vote non 'DV_APPROUVE'. <sup>1</sup>
        - Bouton "Soumettre mon Vote". <sup>1</sup>
      - **Logique Soumission Vote** (appel à ServiceCommission.enregistrerVotePourRapport) :
                1. INSERT INTO vote_commission (...) VALUES (...);.
                2. Journalisation (enregistrer).
                3. Vérification Consensus (ServiceCommission) : Si tous ont voté pour ce tour :

Unanimité "Approuvé" : rapport_etudiant.id_statut_rapport -> 'RAP_ATTENTE_PV_VALID'. Enregistrement décision finale (rapport_etudiant.decision_finale_commission, recommandations_commission_prelim). Notification pour rédaction PV.

Unanimité "Refusé" ou "Corrections" : Statut et décision similaires.

Divergence/Demande Discussion : rapport_etudiant.id_statut_rapport -> 'RAP_COMM_DISCUSSION'. Notification membres. Concertation (Messagerie onglet E). Président peut initier nouveau tour_vote. Gestion max tours (paramètre ServiceConfigurationSysteme). Escalade si pas consensus. <sup>1</sup>

- - - **Section 4 : Formalisation de l'Encadrement (Directeur de Mémoire et Encadreur Pédagogique)** :
            - Interface : Affichage directeurs/encadreurs proposés. Listes déroulantes pour sélectionner/confirmer enseignants (filtrables par specialite, grade). Bouton "Valider l'Encadrement". <sup>1</sup>
            - **Logique** (ServiceCommission.confirmerEncadrementRapport) : UPDATE rapport_etudiant SET directeur_memoire_confirme_par_commission =?, encadreur_pedagogique_confirme_par_commission =?. Met à jour/crée entrées affecter avec id_statut_jury approprié ('ROLEJURY_DIR_MEMOIRE', 'ROLEJURY_ENC_PEDAGO'). Journalisation. <sup>1</sup>
      - **Section 5 : Planification de Session Présentielle (si habilité, ex: Président)** :
        - Interface pour créer session_commission (date, heure, lieu, ordre du jour). Associer id_rapport_etudiant à id_session_commission (via pv_session_rapport ou rapport_session_commission). <sup>1</sup>

#### C. Onglet: Gestion des Procès-Verbaux (PV) <sup>1</sup>

- **Objectif** : Permettre la rédaction, soumission, consultation et validation des PV de la commission.
- **Contenu et Fonctionnalités** :
  - **C.1. Liste des PV (Brouillons, En Attente de Validation, Validés)** :
    - **Interface** : Tableau (id_compte_rendu, type_pv, libelle_rapport_etudiant si individuel, id_session_commission si session, date_creation_pv, libelle_statut_pv, id_redacteur).
    - **Filtres** : Par type_pv, id_statut_pv, id_annee_academique (via rapport), id_redacteur.
    - **Actions** : "Rédiger/Modifier PV", "Soumettre pour Validation", "Valider ce PV", "Voir/Télécharger PDF". <sup>1</sup>
  - **C.2. Workflow de Rédaction et Validation de PV** :
    - **Étape 1 : Rédaction du PV (par Rédacteur désigné)** :
      - Interface : Formulaire avec éditeur riche pour compte_rendu.libelle_compte_rendu. Champs pour lier à id_rapport_etudiant (si individuel) ou id_session_commission (si session).
      - Logique (ServiceCommission.redigerOuMettreAJourPv) : INSERT ou UPDATE compte_rendu avec id_statut_pv = 'PV_BROUILLON'. Journalisation. <sup>1</sup>
    - **Étape 2 : Soumission du PV pour Validation** :
      - Action "Soumettre pour Validation" par le rédacteur.
      - Logique (ServiceCommission.soumettrePvPourValidation) : UPDATE compte_rendu SET id_statut_pv = 'PV_SOUMIS_VALID'. Journalisation. Notification aux autres membres. <sup>1</sup>
    - **Étape 3 : Validation du PV par les Membres de la Commission** :
      - Interface : Consultation du PV. Options "Approuver le PV" (id_decision_validation_pv = 'DV_PV_APPROUVE') ou "Demander Modification" (id_decision_validation_pv = 'DV_PV_MODIF') avec champ commentaire_validation_pv obligatoire si modif.
      - Logique (ServiceCommission.validerOuRejeterPv) : INSERT INTO validation_pv. Journalisation. Vérification consensus (configurable via ServiceConfigurationSysteme).
        - Si validé : UPDATE compte_rendu SET id_statut_pv = 'PV_VALID'. Appel ServiceRapport.finaliserStatutApresPVValide (pour chaque rapport concerné). Appel ServiceDocumentGenerator.genererDocumentPDF pour PV. Notification étudiant et scolarité.
        - Si modif demandée : UPDATE compte_rendu SET id_statut_pv = 'PV_MODIF_REQ'. Notification rédacteur. <sup>1</sup>

#### D. Onglet: Gestion des Corrections (Post-Commission) <sup>1</sup>

- **Objectif** : Suivre et statuer sur les corrections demandées aux étudiants par la commission.
- **Interface et Fonctionnalités** :
  - **D.1. Liste des Rapports en Attente de Corrections Validées** : Tableau des rapport_etudiant avec id_statut_rapport = 'RAP_CORRECT_SOUMISES_COMM'.
  - **D.2. Interface d'Examen des Corrections** :
    - Consultation de la version corrigée (document_soumis avec version > 1) et de la note explicative de l'étudiant.
    - Rappel des recommandations initiales du PV.
    - Options pour la commission : "Valider les Corrections", "Refuser les Corrections (Maintenir Décision Initiale)", "Demander Nouvelles Modifications". Champ commentaire. <sup>1</sup>
  - **Logique** (ServiceCommission.statuerSurCorrectionsRapport) :
    - Validation. Enregistrement décision.
    - UPDATE rapport_etudiant.id_statut_rapport (vers 'RAP_VALID', 'RAP_REFUSE', ou retour à 'RAP_CORRECT').
    - Journalisation. Si corrections validées, mise à jour/addendum PV via ServiceDocumentGenerator. Notification étudiant. <sup>1</sup>

#### E. Onglet: Communication & Concertation <sup>1</sup>

- **Objectif** : Faciliter les discussions et la délibération entre les membres de la commission, notamment pour les rapports nécessitant une concertation.
- **Interface et Fonctionnalités** (gérées par ServiceMessagerie.php) :
  - Similaire à D. Messagerie Interne du Module Personnel Administratif.
  - Possibilité de groupes de discussion créés automatiquement ou manuellement pour chaque rapport en discussion (rapport_etudiant.id_statut_rapport = 'RAP_COMM_DISCUSSION'). <sup>1</sup>

#### F. Onglet: Historique & Archives (Commission) <sup>1</sup>

- **Objectif** : Fournir un accès consultatif aux archives des activités passées de la commission.
- **Interface et Fonctionnalités** :
  - **F.1. Consultation des Rapports Traités Antérieurement** : Tableau des rapport_etudiant avec statuts finaux ('RAP_VALID', 'RAP_REFUSE_ARCHIVE'). Accès aux PV associés.
  - **F.2. Consultation des PV Archivés** : Liste des compte_rendu avec id_statut_pv = 'PV_VALID' ou 'PV_ARCHIVE_OFFICIEL'.
  - **F.3. Historique des Votes et Décisions** (si pertinent et droits suffisants) : Consultation des vote_commission et validation_pv passés. <sup>1</sup>

#### G. Onglet: Mon Profil (commun) <sup>1</sup>

- **Objectif** : Permettre au membre de la commission de gérer ses propres informations de compte.
- **Interface et Fonctionnalités** : Similaire à E. Mon Profil du Module Personnel Administratif, mais pour un enseignant lié à un utilisateur. Modification email_principal, mot de passe, photo_profil, préférences de notification. <sup>1</sup>

## Partie V : Services Transversaux (Synthèse)

### ServiceAuthentification.php <sup>1</sup>

- **Rôle** : Gère connexion, déconnexion, gestion de session, création/activation de comptes (appelé par RS pour étudiants), réinitialisation MDP, validation email, gestion 2FA. <sup>1</sup>
- **Méthodes Clés** : detruireSessionUtilisateur(), genererEtActiverCompteEtudiantPourRS(), modifierMotDePasseUtilisateur(). <sup>1</sup>
- **Interactions** : Tables utilisateur, etudiant, personnel_administratif, enseignant, enregistrer, historique_mot_de_passe. Appelle ServiceEmail (via ServiceNotification). <sup>1</sup>

### ServiceNotification.php et ServiceEmail.php <sup>1</sup>

- **Rôle** : ServiceNotification orchestre toutes les communications (internes et emails), gère les templates (message), détermine les destinataires. ServiceEmail gère l'envoi technique des emails. <sup>1</sup>
- **Déclenchement** : Par les services métier (ServiceConformite, ServiceAuthentification, ServiceRapport, ServiceCommission) et les tâches CRON. <sup>1</sup>
- **Types de Notifications/Emails** : Bienvenue, validation compte/email, reset MDP, décisions de conformité/commission, soumission/resoumission rapport, alertes, rappels. <sup>1</sup>
- **Gestion Templates** : Via table message (ID, sujet, corps avec placeholders, type). <sup>1</sup>
- **Interactions** : ServiceEmail appelé par ServiceNotification. Tables recevoir, utilisateur, message, notification, enregistrer. <sup>1</sup>

### ServiceDocumentGenerator.php <sup>1</sup>

- **Rôle** : Génération centralisée et automatisée de documents PDF officiels (attestations, PV, relevés). <sup>1</sup>
- **Principe** : Basé sur templates (HTML/CSS), peuplés avec données dynamiques, convertis en PDF via librairie (TCPDF, Dompdf). <sup>1</sup>
- **Sources Données** : etudiant, inscrire, rapport_etudiant, compte_rendu, evaluer, etc. <sup>1</sup>
- **Invocation** : Par Module Personnel Administratif (RS pour attestations), Module Commission (pour PV), Module Admin (pour gestion modèles). <sup>1</sup>

### ServiceConfigurationSysteme.php <sup>1</sup>

- **Rôle** : Centralise gestion et fourniture des paramètres système globaux (délais, règles validation, seuils alertes, paramètres vote, options chat). <sup>1</sup>
- **Stockage Paramètres** : Fichiers de conf (ex: .env) ou table systeme_parametres (clé-valeur). <sup>1</sup>
- **Consommation** : Autres services/modules appellent des méthodes de ce service pour récupérer les configurations. Cache interne recommandé. <sup>1</sup>

### Autres Services (implicites ou mentionnés)

- **ServiceRapport.php** : Gère cycle de vie des rapports (soumission, corrections). <sup>1</sup>
- **ServiceConformite.php** : Gère processus de vérification de conformité. <sup>1</sup>
- **ServiceCommission.php** : Gère processus d'évaluation par la commission (vote, PV). <sup>1</sup>
- **ServiceGestionAcademique.php** : Gère données académiques (inscriptions, stages, notes). <sup>1</sup>
- **ServiceReclamation.php** : Gère réclamations étudiants. <sup>1</sup>
- **ServiceMessagerie.php** : Gère messagerie interne. <sup>1</sup>
- **PermissionService (conceptuel)** : Vérifie droits utilisateurs. <sup>1</sup>
- **AuditService (conceptuel)** : Centralise enregistrement logs dans enregistrer. <sup>1</sup>

## Conclusion Architecturale <sup>1</sup>

Le système "GestionMySoutenance" est fondé sur des principes architecturaux robustes :

- **Architecture MVC** : Clairement implémentée via la structure des répertoires (Controller, Model, Views) et la séparation des responsabilités. Les Contrôleurs gèrent les requêtes, les Modèles la logique métier et l'accès aux données, les Vues la présentation. <sup>1</sup>
- **Gestion Textuelle des Rapports** : Les étudiants saisissent le contenu de leur rapport directement dans des éditeurs de texte intégrés ; aucun fichier n'est téléversé pour le corps du rapport. Le contenu est stocké dans document_soumis.contenu_textuel. <sup>1</sup>
- **Génération Centralisée de PDF** : ServiceDocumentGenerator.php utilise des templates pour produire tous les documents PDF officiels, assurant cohérence et professionnalisme. <sup>1</sup>
- **Sécurité RBAC (Role-Based Access Control)** : Implémentée via type_utilisateur, groupe_utilisateur, traitement (fonctionnalités granulaires), et rattacher (liaison groupe-traitement). Un PermissionService centralise la vérification des droits. <sup>1</sup>
- **Audit Détaillé** : La table enregistrer, alimentée par un AuditService, logue toutes les actions significatives avec utilisateur, date, type d'action, entité concernée et détails JSON, assurant une traçabilité complète. <sup>1</sup>
- **Architecture Modulaire** : Le système est divisé en modules fonctionnels (Étudiant, Personnel Administratif, Commission, Administration), chacun avec ses propres contrôleurs, vues, et potentiellement services, facilitant le développement et la maintenance. <sup>1</sup>
- **Services Centralisés pour Logique Transversale** : Des services dédiés (Authentification, Notification, Email, Génération Document, Configuration Système, etc.) encapsulent la logique métier complexe ou partagée, favorisant la réutilisabilité et la cohérence. <sup>1</sup>

Ces principes concourent à un système structuré, sécurisé, maintenable et apte à gérer la complexité du processus de soutenance.