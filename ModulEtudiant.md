# GestionMySoutenance : Analyse Fonctionnelle et Conception

# Détaillée du Système

## 1. Introduction Générale du Système "GestionMySoutenance"

**Présentation du Système**
"GestionMySoutenance" est une application web dynamique conçue pour orchestrer
et numériser l'intégralité du processus de gestion des rapports de soutenance – qu'il
s'agisse de rapports de stage, de mémoires de fin d'études ou d'autres travaux
académiques similaires – au sein d'un établissement d'enseignement supérieur. La
plateforme a pour vocation de structurer et de rationaliser les interactions complexes
entre les différents acteurs impliqués : les étudiants, le personnel administratif (chargé
du contrôle de conformité et de la gestion de la scolarité), la commission
pédagogique responsable de la validation des rapports, et les administrateurs
techniques du système.
Développée en s'appuyant sur le langage PHP en version 8.2, "GestionMySoutenance"
adopte une architecture Modèle-Vue-Contrôleur (MVC) pour une meilleure
organisation et maintenabilité du code. L'application est également conçue pour un
déploiement flexible et moderne via la technologie de conteneurisation Docker,
facilitant ainsi son installation et sa gestion dans divers environnements serveur.
**Objectifs Généraux du Système**
Le système "GestionMySoutenance" vise à atteindre plusieurs objectifs stratégiques
et opérationnels pour l'établissement :

1. **Centralisation et Sécurisation des Données :** Regrouper en un point unique
    toutes les informations et les documents (sous forme textuelle) relatifs aux
    soutenances, en garantissant la confidentialité, l'intégrité et la pérennité des
    données.
2. **Fluidification et Traçabilité des Workflows :** Optimiser et rendre transparents
    les processus de soumission, de vérification de conformité, d'évaluation par la
    commission, et de gestion des corrections, en assurant une traçabilité complète
    de chaque étape.
3. **Interfaces Utilisateur Adaptées :** Fournir à chaque catégorie d'utilisateur
    (étudiant, agent administratif, membre de commission, administrateur) une
    interface dédiée, ergonomique et spécifiquement conçue pour répondre à ses
    besoins et responsabilités.
4. **Assurance de la Conformité :** Mettre en place des mécanismes pour garantir la
    conformité administrative et réglementaire des rapports soumis par les étudiants,


```
ainsi que le respect des procédures pédagogiques de l'établissement.
```
5. **Facilitation de la Communication :** Offrir des outils de communication intégrés
    (messagerie, notifications) pour améliorer la coordination et les échanges
    d'informations entre les différents acteurs du processus de soutenance.
6. **Audit Détaillé :** Permettre un suivi exhaustif et une journalisation de toutes les
    actions significatives réalisées sur la plateforme et des accès au système, à des
    fins de sécurité, de contrôle et d'analyse.
**Principes Architecturaux et de Conception Clés**
La conception de "GestionMySoutenance" repose sur plusieurs principes
architecturaux et choix de conception fondamentaux qui façonnent son
fonctionnement et sa structure :
● **Architecture MVC (Modèle-Vue-Contrôleur) :** La structure des répertoires du
projet, notamment avec des dossiers distincts tels que src/Backend/Controller,
src/Backend/Model, et src/Frontend/views, témoigne de l'adoption du patron de
conception MVC. Cette séparation des préoccupations – la logique métier et
l'accès aux données (Modèle), la présentation à l'utilisateur (Vue), et la gestion
des requêtes et la coordination (Contrôleur) – est un gage de maintenabilité, de
testabilité et d'évolutivité du code. 1
● Gestion Exclusivement Textuelle des Rapports : Une caractéristique distinctive et
structurante du système est l'absence de téléversement (upload) de fichiers
binaires (comme des.docx ou.pdf) pour le contenu principal des rapports par les
étudiants ou le personnel. Au lieu de cela, les étudiants saisissent directement le
contenu de leurs rapports (résumé, introduction, corps du texte, bibliographie,
etc.) via des formulaires équipés d'éditeurs de texte enrichi (WYSIWYG) intégrés à
l'application. Ces informations sont ensuite stockées en base de données sous
forme textuelle, vraisemblablement dans des champs de type LONGTEXT au sein
de la table document_soumis (attribut contenu_textuel). 1, 1, 1, 1
Ce choix de conception a des implications notables. D'une part, il simplifie
considérablement la gestion des fichiers sur le serveur : pas de problématiques
complexes de stockage de fichiers volumineux, de gestion de versions de fichiers
binaires, de détection de virus, ou de compatibilité des formats. La consultation
du contenu par les évaluateurs est également facilitée, se faisant directement
dans l'interface web sans nécessiter de logiciels tiers. D'autre part, cette
approche peut limiter la richesse du formatage que les étudiants peuvent
appliquer à leurs travaux et compliquer la soumission d'annexes graphiques ou de
contenus non textuels complexes. Elle reporte également la complexité sur la
capacité de la base de données à stocker et à restituer efficacement de grandes


quantités de texte, ainsi que sur la robustesse des éditeurs de texte enrichi
fournis. La décision de privilégier une gestion textuelle est probablement motivée
par des impératifs de sécurité (minimisation des risques liés aux uploads de
fichiers) et de simplicité de développement pour le cœur du système, tout en
assurant une consultation directe et universelle du contenu.
● **Génération Centralisée de Documents PDF :** Tous les documents officiels
produits par le système – tels que les attestations de dépôt, les procès-verbaux
de soutenance, les relevés de notes, ou les attestations de scolarité – sont
générés dynamiquement au format PDF. Cette tâche est dévolue à un service
spécialisé, ServiceDocumentGenerator.php, qui s'appuie sur des bibliothèques
PHP dédiées comme TCPDF (mentionnée dans composer.json) ou potentiellement
DomPDF. 1 , 1 , 1 , 1 Ce service utilise des modèles (templates), probablement
HTML/CSS, qui sont ensuite peuplés avec les données extraites de la base,
garantissant ainsi l'uniformité, la charte graphique de l'établissement et l'intégrité
des informations présentées.
● **Sécurité Basée sur les Rôles (RBAC - Role-Based Access Control) :** Le
système met en œuvre un mécanisme d'habilitation granulaire et sophistiqué. Il
s'appuie sur un ensemble de tables de base de données (utilisateur,
type_utilisateur, groupe_utilisateur, niveau_acces_donne, traitement, et la table de
liaison rattacher) pour définir avec précision les actions que chaque utilisateur est
autorisé à effectuer et les données auxquelles il peut accéder. 1 Ce modèle RBAC
permet une gestion fine des droits, alignée sur les responsabilités de chaque rôle
au sein de l'institution.
● **Audit Détaillé et Traçabilité :** Une piste d'audit complète est assurée par la
journalisation systématique de toutes les actions significatives (créations,
modifications, suppressions, changements de statut, connexions, etc.) dans la
table enregistrer. 1 Chaque enregistrement d'audit contient des informations
cruciales telles que l'identifiant de l'utilisateur auteur de l'action, la date et l'heure,
le type d'action, l'entité concernée, et des détails spécifiques à l'action (souvent
stockés en format JSON pour plus de flexibilité). Ce mécanisme est fondamental
pour la sécurité, la redevabilité et l'analyse post-incident.
● **Architecture Modulaire :** L'application est structurée en modules fonctionnels
distincts, chacun correspondant à un espace utilisateur ou à un ensemble de
responsabilités spécifiques : Module Étudiant, Module Personnel Administratif
(avec ses sous-rôles), Module Commission de Validation, et Module
Administration. 1 , 1 Chaque module dispose de ses propres contrôleurs, vues, et
interagit avec les modèles et services métiers partagés, favorisant une meilleure
organisation du code et une plus grande autonomie des composants.
● **Services Applicatifs Centralisés :** La logique métier complexe, les opérations


transversales (comme l'envoi de notifications ou la gestion de l'authentification)
et les interactions avec des systèmes externes (comme l'envoi d'emails) sont
encapsulées au sein de classes de service dédiées (par exemple,
ServiceAuthentification.php, ServiceNotification.php, ServiceEmail.php,
ServiceRapport.php, etc.). 1 Cette approche favorise la réutilisabilité du code, la
séparation claire des préoccupations (SoC), et facilite les tests unitaires et
d'intégration.
**Technologies et Dépendances Clés**
L'analyse du fichier composer.json et des descriptions fonctionnelles révèle
l'utilisation des technologies et bibliothèques suivantes, qui constituent le socle
technique de "GestionMySoutenance" :
● **Langage de Programmation et Environnement :**
○ PHP version 8.2 ou supérieure.
○ Extensions PHP essentielles : ext-pdo et ext-mysqli (pour l'accès aux bases
de données), ext-mbstring (pour la manipulation de chaînes multi-octets),
ext-ctype (fonctions de vérification de type de caractère), ext-json (pour la
manipulation de données JSON, notamment dans la table enregistrer), ext-intl
(pour l'internationalisation, si applicable), ext-gd (pour la manipulation
d'images, potentiellement pour les photos de profil ou les QR codes), ext-zip
(pour la gestion d'archives ZIP, dont l'usage n'est pas immédiatement
apparent mais pourrait être lié à des exports/imports futurs).
● **Gestion des Dépendances :**
○ Composer (implicite par la présence de composer.json et composer.lock).
● **Gestion des Variables d'Environnement :**
○ vlucas/phpdotenv (version ^5.6) : Utilisé pour charger les variables
d'environnement (identifiants de base de données, clés API, etc.) à partir d'un
fichier .env, ce qui est une bonne pratique pour la configuration et la sécurité.
● **Routage des Requêtes HTTP :**
○ nikic/fast-route (version ^1.3) : Une bibliothèque de routage légère et
performante, permettant de mapper les URLs des requêtes HTTP aux
méthodes des contrôleurs appropriés.
● **Envoi d'Emails :**
○ phpmailer/phpmailer (version ^6.9) : Une bibliothèque populaire et robuste
pour l'envoi d'emails, utilisée par ServiceEmail.php.
● **Authentification à Deux Facteurs (2FA) :**
○ robthree/twofactorauth (version ^2.1) : Fournit la logique pour générer et
vérifier les codes TOTP (Time-based One-Time Password).


○ bacon/bacon-qr-code (version ^2.0.8) : Utilisé pour générer les codes QR que
les utilisateurs scannent avec leurs applications d'authentification pour
configurer la 2FA.
● **Génération de Documents :**
○ tecnickcom/tcpdf (version ^6.7) : Une bibliothèque puissante pour la
génération de documents PDF en PHP, utilisée par
ServiceDocumentGenerator.php.
○ phpoffice/phpspreadsheet (version ^3.1.2) : Permet la création et la
manipulation de fichiers de tableur (Excel, CSV, etc.), probablement utilisée
pour les fonctionnalités d'export de données du Module Administration.
● **Conteneurisation et Déploiement :**
○ Docker (mentionné dans la requête utilisateur, présence de
docker-compose.yml et Dockerfile) : Utilisé pour créer des environnements de
développement, de test et de production reproductibles et isolés.
○ Apache (mentionné dans apache-vhost.conf) : Serveur web configuré pour
servir l'application PHP.
● **Base de Données :**
○ MySQL (implicite par ext-mysqli et le dump SQL mysoutenance.sql). La
version du serveur MySQL est 8.3.0. 1
Ces choix technologiques indiquent une approche moderne du développement PHP,
axée sur des composants éprouvés et des bonnes pratiques en matière de
configuration, de sécurité et de gestion des dépendances.

## 2. Module Étudiant

**Objectif Global**
Le Module Étudiant de la plateforme "GestionMySoutenance" est conçu comme un
espace personnalisé et sécurisé, dédié à chaque étudiant engagé dans le processus
de rédaction et de validation de son rapport de soutenance. 1 L'objectif principal de
ce module est de centraliser toutes les informations et actions relatives au parcours
de l'étudiant, depuis la saisie et la soumission du contenu de son rapport jusqu'à la
consultation de ses résultats et des documents PDF officiels générés par le système. Il
vise à faciliter la saisie et la soumission du contenu du rapport et des éventuelles
corrections via des formulaires et des éditeurs de texte intégrés, à offrir une visibilité
claire et en temps réel sur l'avancement de son dossier à travers les différentes étapes
de validation (conformité, commission), à permettre la communication avec
l'administration via un système de réclamations structuré, et à fournir un accès aux


ressources (guides, modèles) et aux documents PDF générés par le système
(bulletins, attestations). 1
**Accès, Authentification et Prérequis**
L'accès au Module Étudiant est strictement conditionné par la création préalable d'un
compte utilisateur. Ce processus est initié et géré exclusivement par le Responsable
Scolarité et est soumis à des prérequis rigoureux. 1

1. **Prérequis pour la Génération du Compte :** 1
    ○ **Scolarité à Jour :** L'étudiant doit être administrativement inscrit pour l'année
       académique en cours (identifiée par annee_academique.est_active = 1) et son
       statut de paiement des droits de scolarité doit être en règle. Le Responsable
       Scolarité vérifie et met à jour cette information dans la table inscrire (le
       champ inscrire.id_statut_paiement doit correspondre à un libellé "Payé" ou
       "Exonéré" de la table de référence statut_paiement_ref).
    ○ **Stage Effectué et Enregistré :** L'étudiant doit avoir effectué un stage
       pertinent pour son cursus, et ce stage doit avoir été officiellement enregistré
       et validé dans le système par le Responsable Scolarité. Cela se traduit par un
       enregistrement complet et validé dans la table faire_stage pour l'étudiant et
       l'année académique concernée.
2. **Processus de Génération du Compte par le Responsable Scolarité (via son**
    **propre module) :** 1
       ○ Le Responsable Scolarité vérifie que les deux conditions ci-dessus sont
          remplies pour un étudiant donné (en consultant les tables inscrire et
          faire_stage).
       ○ Si, et seulement si, les deux conditions sont validées, le Responsable Scolarité
          peut utiliser une fonctionnalité de son module pour générer le compte
          utilisateur de l'étudiant.
       ○ Cette action déclenche (via ServiceAuthentification.php et potentiellement
          ServiceGestionAcademique.php) :
             ■ La création d'un enregistrement dans la table utilisateur avec
                id_type_utilisateur = 'TYPE_ETUD'. Le statut_compte initial peut être 'actif'
                ou 'en_attente_validation' (si une validation de l'email par l'étudiant est
                requise après cette création). Un numero_utilisateur unique est généré.
             ■ La mise à jour de etudiant.numero_utilisateur avec l'identifiant du compte
                utilisateur nouvellement créé, liant ainsi le profil étudiant au compte
                d'accès.
       ○ Le système (via ServiceAuthentification.php et ServiceEmail.php) envoie
          ensuite un email à l'adresse utilisateur.email_principal (qui peut être


```
initialement renseignée à partir de etudiant.email_contact_secondaire ou d'un
email institutionnel) contenant :
■ Son identifiant de connexion (utilisateur.login_utilisateur).
■ Un mot de passe initial sécurisé (généré par le système) ou un lien unique
permettant à l'étudiant de définir son mot de passe.
■ L'URL d'accès à la plateforme "GestionMySoutenance".
■ Des instructions pour la première connexion et, le cas échéant, pour la
validation de son adresse email.
```
3. **Authentification de l'Étudiant :** 1
    ○ Lors de sa première connexion, l'étudiant utilise les identifiants fournis. Il peut
       être invité à changer son mot de passe initial et à valider son adresse email si
       utilisateur.email_valide = 0.
    ○ Les tentatives de connexion ultérieures sont gérées par
       ServiceAuthentification.php.
**Environnement Fermé (Gestion Textuelle des Rapports)**
Une caractéristique fondamentale du système "GestionMySoutenance" est son
environnement fermé en ce qui concerne la soumission des rapports. L'étudiant ne
téléverse (upload) aucun fichier pour le contenu de son rapport (corps du texte,
résumé, bibliographie) ni pour les attestations. Toutes ces informations sont saisies
directement via des formulaires dédiés et des éditeurs de texte enrichi (WYSIWYG)
intégrés à la plateforme. 1 Les "documents" mentionnés pour la soumission font
référence à ces ensembles d'informations structurées et textuelles. Seul
l'Administrateur Système a la capacité d'importer des données en masse (listes
d'étudiants, etc.) ou de gérer les modèles de documents PDF qui seront ensuite
générés par le système. Cette approche de gestion textuelle des rapports simplifie la
gestion des fichiers sur le serveur et la sécurité, mais reporte la complexité sur la
gestion du contenu textuel riche et sa restitution. 1
**Header Proposé**
L'en-tête du Module Étudiant est conçu pour offrir une identification claire et un accès
rapide aux fonctionnalités essentielles. 1
● **Intitulé :** "Mon Espace MySoutenance - [Nom Prénom de l'Étudiant]"
○ **Objectif :** Identifier clairement l'espace personnel de l'étudiant et le
personnaliser.
○ **Affichage :** Permanent en haut de chaque page du Module Étudiant.
● **Fonctionnalités associées au header :**
○ Logo de l'Institution / Application.


○ Nom et Prénom de l'étudiant connecté (issus de etudiant.nom, prenom).
○ Lien/Icône vers "Mon Profil" (accès rapide à l'onglet B).
○ Indicateur de Notifications Non Lues : Un badge numérique sur une icône de
cloche, basé sur le nombre d'entrées où recevoir.lue = 0 pour le
numero_utilisateur de l'étudiant.
○ Bouton/Lien de Déconnexion Sécurisée : Appelle
ServiceAuthentification.detruireSessionUtilisateur(), l'action étant journalisée
dans la table enregistrer.
○ Affichage discret de l'Année Académique Active :
annee_academique.libelle_annee_academique où est_active = 1.
**Sidebar Dynamique**
La barre latérale de navigation (sidebar) est le principal moyen pour l'étudiant de
naviguer au sein de son module. Sa nature dynamique se manifeste par l'activation ou
la désactivation de certaines actions en fonction de l'état d'avancement de son
processus de rapport. 1
● **Éléments de la Sidebar (correspondant aux onglets principaux) :**
○ **A. Tableau de Bord :** Libellé "Tableau de Bord", Icône Maison/Tableau de
bord.
○ **B. Mon Profil :** Libellé "Mon Profil", Icône Utilisateur/Engrenage.
○ **C. Mon Rapport :** Libellé "Mon Rapport", Icône Document/Dossier.
○ **D. Mes Documents PDF :** Libellé "Mes Documents PDF", Icône Fichiers
PDF/Téléchargement.
○ **E. Mes Réclamations :** Libellé "Mes Réclamations", Icône Point
d'interrogation/Bulle de dialogue.
○ **F. Ressources & Aide :** Libellé "Ressources & Aide", Icône Livre/Bouée de
sauvetage.
**Fonctionnalités Détaillées par Onglet
A. Onglet: Tableau de Bord (Frontend/views/Etudiant/dashboard_etudiant.php)**
● **Objectif :** Fournir une vue d'ensemble immédiate des informations les plus
pertinentes et des actions requises pour l'étudiant. 1
● **Interface Utilisateur et Widgets :**
○ **A.1. Statut Actuel de Mon Rapport :** 1
■ **Affichage :** Un encadré proéminent indiquant le libelle_statut_rapport
actuel (issu de la jointure entre rapport_etudiant et statut_rapport_ref)
pour l'année académique active. Exemples de statuts : "Aucun rapport
soumis", "Rapport Soumis - En attente de vérification de conformité",


"Rapport Conforme - Transmis à la commission", "Corrections Demandées
(Conformité)", "Rapport Validé par la Commission", "Processus de reprise
de rapport en cours".
■ **Interaction :** Un lien mène vers l'onglet "Mon Rapport" (C) pour plus de
détails.
■ **Logique Algorithmique/SQL :** Récupère le dernier rapport_etudiant pour
le numero_carte_etudiant de l'étudiant connecté et
l'id_annee_academique active.
SQL
SELECT srr.libelle_statut_rapport
FROM rapport_etudiant r
JOIN statut_rapport_ref srr ON r.id_statut_rapport = srr.id_statut_rapport
JOIN inscrire i ON r.numero_carte_etudiant = i.numero_carte_etudiant
WHERE r.numero_carte_etudiant = :numero_carte_etudiant_connecte
AND i.id_annee_academique = (SELECT id_annee_academique FROM
annee_academique WHERE est_active = 1 LIMIT 1 )
ORDER BY r.date_soumission DESC
LIMIT 1 ;
○ **A.2. Notifications Récentes Non Lues :** 1
■ **Affichage :** Une liste des 3 à 5 dernières notifications non lues (où
recevoir.lue = 0) pour cet étudiant, affichant
notification.libelle_notification et recevoir.date_reception.
■ **Interaction :** Un lien "Voir toutes les notifications" mène à une vue dédiée
des notifications.
■ **Logique Algorithmique/SQL :**
SQL
SELECT r.id_reception, r.date_reception, n.libelle_notification
FROM recevoir r
JOIN notification n ON r.id_notification = n.id_notification
WHERE r.numero_utilisateur = :numero_utilisateur_connecte AND r.lue = 0
ORDER BY r.date_reception DESC
LIMIT 5 ;
○ **A.3. Alertes et Actions Requises :** 1
■ **Affichage :** Des messages contextuels basés sur
rapport_etudiant.id_statut_rapport ou utilisateur.statut_compte.
■ Exemple si id_statut_rapport = 'RAP_NON_CONF' : "Votre rapport a été
retourné pour corrections (Conformité). Date limite de resoumission :


[date_limite_calculée]."
■ Exemple si id_statut_rapport = 'RAP_CORRECT' (par la commission,
interprété selon la nouvelle contrainte) : "La commission a émis des
recommandations concernant votre rapport. Veuillez consulter le PV
pour plus de détails." (Pas de resoumission à la commission).
■ Exemple si utilisateur.statut_compte =
'SUSPENDU_ATTENTE_RS_STAGE' : "Votre accès à la soumission de
rapport est suspendu. Veuillez contacter le Responsable Scolarité
pour régulariser votre situation de stage."
■ **Règles Métier :** Le calcul de la [date_limite_calculée] pour la
resoumission (conformité) se base sur un paramètre système (défini en
D.2.1 du Module Admin, ex: X jours après la date de retour) et la date
effective de retour du rapport.
■ **Logique Algorithmique :** Interprétation du statut actuel et application
des règles métier pour générer le message approprié.
○ **A.4. Raccourcis Rapides (Optionnel) :** 1
■ **Affichage :** Boutons ou liens directs tels que "Soumettre mon rapport" (si
éligible et aucun rapport en cours), "Consulter mes documents PDF",
"Faire une réclamation".
● **Services Impliqués :** ServiceRapport (pour l'état du rapport), ServiceNotification
(pour les notifications et les messages d'alerte), ServiceConfigurationSysteme
(pour les délais).
● **Validations :** Aucune validation d'entrée utilisateur ici, il s'agit d'un affichage
d'informations.
**B. Onglet: Mon Profil (Frontend/views/Etudiant/profil_etudiant.php)**
● **Objectif :** Permettre à l'étudiant de consulter ses informations personnelles et de
compte, et de modifier celles qui sont autorisées. 1
● **Interface Utilisateur et Fonctionnalités :**
○ **B.1. Consultation des Informations Personnelles (issues de la table
etudiant) :** 1
■ **Affichage :** Champs majoritairement en lecture seule :
numero_carte_etudiant, nom, prenom, date_naissance, lieu_naissance,
pays_naissance, nationalite, sexe, adresse_postale, ville, code_postal.
■ **Champs Modifiables par l'Étudiant :**
■ telephone (VARCHAR(20)).
■ email_contact_secondaire (VARCHAR(255)) : Un email personnel
alternatif.
■ contact_urgence_nom (VARCHAR(100)), contact_urgence_telephone


(VARCHAR(20)), contact_urgence_relation (VARCHAR(50)).
■ **Logique Algorithmique/SQL (Consultation) :**
SQL
SELECT * FROM etudiant WHERE numero_utilisateur =
:numero_utilisateur_connecte;
■ **Logique Algorithmique/SQL (Modification) :**
SQL
UPDATE etudiant
SET telephone = :telephone, email_contact_secondaire =
:email_contact_secondaire,
contact_urgence_nom = :contact_urgence_nom,
contact_urgence_telephone = :contact_urgence_telephone,
contact_urgence_relation = :contact_urgence_relation
WHERE numero_utilisateur = :numero_utilisateur_connecte;
■ **Validations (Frontend et Backend) :**
■ Format du telephone.
■ Format de email_contact_secondaire (doit être une adresse email
valide).
■ Longueurs maximales des champs texte.
○ **B.2. Gestion du Compte Utilisateur (issues de la table utilisateur) :** 1
■ **Affichage/Modification :**
■ login_utilisateur : Affiché en lecture seule.
■ email_principal : Modifiable par l'étudiant.
■ **Règle Métier (Modification email_principal) :** Si modifié,
utilisateur.email_valide doit passer à 0. Un token_validation_email
unique doit être généré et stocké. Un email de validation contenant
un lien avec ce token est envoyé à la _nouvelle_ adresse email.
L'ancienne adresse peut être notifiée du changement. L'accès à
certaines fonctionnalités de la plateforme (ou la connexion
elle-même) pourrait être restreint tant que la nouvelle adresse
n'est pas validée.
■ **Validations :** Format email valide. L'unicité de cet email est gérée
par une contrainte de base de données et doit être vérifiée par le
service avant la mise à jour.
■ **Modification du Mot de Passe :**
■ **Interface :** Formulaire avec les champs "Ancien Mot de Passe",
"Nouveau Mot de Passe", "Confirmer Nouveau Mot de Passe".


```
■ Règles Métier & Validations :
■ L'ancien mot de passe doit correspondre à celui stocké (après
hachage de la saisie utilisateur et comparaison avec
utilisateur.mot_de_passe).
■ Le nouveau mot de passe doit respecter les politiques de
complexité (longueur minimale, présence de majuscules,
minuscules, chiffres, caractères spéciaux – définies par
ServiceConfigurationSysteme).
■ Le nouveau mot de passe et sa confirmation doivent être
identiques.
■ Le nouveau mot de passe ne doit pas être identique à un
certain nombre de mots de passe précédents (vérification
dans historique_mot_de_passe).
■ Logique Algorithmique
(ServiceAuthentification.modifierMotDePasseUtilisateur) :
```
1. Vérifier l'ancien mot de passe.
2. Valider la complexité et la confirmation du nouveau mot de
    passe.
3. Hacher le nouveau mot de passe (ex: password_hash()).
4. UPDATE utilisateur SET mot_de_passe = :nouveau_mdp_hache
    WHERE numero_utilisateur = :numero_utilisateur_connecte;
5. INSERT INTO historique_mot_de_passe (numero_utilisateur,
    mot_de_passe_hache, date_changement) VALUES
    (:numero_utilisateur_connecte, :nouveau_mdp_hache, NOW());
■ **Gestion de la Photo de Profil (utilisateur.photo_profil) :**
■ **Affichage :** Affiche la photo actuelle si elle existe.
■ **Interaction :** Bouton pour téléverser une nouvelle photo ou
supprimer l'existante.
■ **Validations (Frontend/Backend) :** Type de fichier (jpg, png), taille
maximale du fichier (paramètre système).
■ **Logique (ServiceAuthentification ou service dédié) :**
Sauvegarde du fichier sur le serveur (chemin sécurisé et unique),
mise à jour de utilisateur.photo_profil avec le chemin relatif.
Suppression de l'ancien fichier si remplacement.
■ **Préférences de Notification (si
utilisateur.preferences_notifications est un champ JSON) :**
■ **Affichage :** Cases à cocher pour différents types de notifications
par email (ex: "Notification de nouveau message interne", "Rappel
de date limite").


```
■ Logique : Met à jour le champ JSON preferences_notifications.
ServiceNotification consultera ces préférences avant d'envoyer un
email.
■ Workflow de Modification Général :
```
1. Validation des données côté client (JavaScript) pour une meilleure
    expérience utilisateur.
2. Soumission au serveur.
3. Validation rigoureuse côté serveur (PHP) pour tous les champs
    modifiés.
4. Appel aux méthodes des services concernés (ServiceAuthentification
    pour le compte, directement le modèle Etudiant ou un service pour le
    profil).
5. Mise à jour des tables etudiant et/ou utilisateur.
6. Journalisation de chaque modification significative dans la table
    enregistrer (id_action = "MODIF_PROFIL_ETUD" ou
    "MODIF_COMPTE_UTIL_ETUD", details_action contenant les champs
    modifiés avec anciennes/nouvelles valeurs si pertinent).
7. Affichage d'un message de confirmation à l'étudiant.
● **Services Impliqués :** ServiceAuthentification (modification MDP, gestion email
principal, photo), ServiceNotification (pour email de re-validation).
● **Tables SQL Principales :** etudiant, utilisateur, historique_mot_de_passe,
enregistrer.
**C. Onglet: Mon Rapport (Frontend/views/Etudiant/Rapport/)**
● **Objectif :** Interface centrale pour la saisie, la soumission, le suivi et la gestion des
corrections (si retournées par la conformité) du contenu du rapport. 1
● **État Initial (si aucun rapport_etudiant pour l'étudiant connecté et
l'id_annee_academique active) :** 1 , 1
○ **Affichage :** Message "Vous n'avez pas encore soumis de rapport pour l'année
académique [Libellé Année Active]."
○ **Interaction :** Un bouton "Soumettre Mon Rapport de Stage" est visible et actif
_uniquement si_ les conditions d'accès initiales (scolarité à jour ET stage
enregistré, vérifiées par le système avant d'afficher le module) sont toujours
remplies ET qu'aucun rapport validé ou en cours de traitement n'existe pour
l'année.
○ **Affichage des Consignes :** Types d'informations requises (issues de
type_document_ref où requis_ou_non = 1), nombre de pages attendu
(information issue de ServiceConfigurationSysteme).
● **C.1. Soumission Initiale du Contenu du Rapport**


**(Frontend/views/Etudiant/Rapport/soumettre_rapport.php)**
○ **Objectif :** Permettre à l'étudiant de saisir et de soumettre pour la première
fois le contenu textuel et les métadonnées de son rapport. 1
○ **Déclenchement :** Clic sur le bouton "Soumettre Mon Rapport de Stage".
○ **Règle Métier :** L'interface de soumission est verrouillée après une première
soumission réussie pour l'année académique en cours, sauf si le rapport est
explicitement retourné à l'étudiant pour corrections par le service de
conformité. 1
○ **Interface du Formulaire de Soumission (Saisie d'Informations Textuelles)
:** 1 , 1
■ **Champs pour les métadonnées du rapport (table rapport_etudiant) :**
■ libelle_rapport_etudiant (Titre du rapport) : Champ texte simple,
obligatoire.
■ theme (Thème principal) : Champ texte simple (VARCHAR(255)),
obligatoire.
■ resume (Résumé/Abstract) : Éditeur de texte enrichi simple (TEXT),
optionnel ou obligatoire selon configuration.
■ numero_attestation_stage (Numéro d'attestation de stage) : Champ
texte simple (VARCHAR(100)). L'attestation physique est gérée hors
système par le Responsable Scolarité.
■ nombre_pages (Nombre de pages) : Champ numérique déclaratif,
obligatoire.
■ id_annee_academique : Automatiquement l'année active, non
modifiable par l'étudiant.
■ **Champs pour le contenu du rapport (stocké dans document_soumis
avec contenu_textuel) :**
■ Pour chaque type_document_ref pertinent pour la soumission initiale
(ex: 'DOC_RAP_MAIN' pour le corps principal, 'DOC_INTRO',
'DOC_CONCLU', 'DOC_BIBLIO', etc., où requis_ou_non = 1), un grand
champ de texte (TEXT ou LONGTEXT) est fourni, équipé d'un éditeur
de texte enrichi (WYSIWYG) permettant un formatage de base (gras,
italique, listes, titres simples).
■ La table document_soumis est adaptée pour stocker ce contenu :
id_document (PK), id_rapport_etudiant (FK), id_type_document (FK),
contenu_textuel (LONGTEXT), version (INT), date_soumission_version
(DATETIME), numero_utilisateur_soumission (FK).
■ **Case à cocher de Confirmation :** "Je confirme que ces informations sont
mon travail original et respectent les directives de l'établissement."
Obligatoire.


○ **Règles Métier & Validations (Frontend et Backend) :** 1
■ Tous les champs de métadonnées marqués comme obligatoires doivent
être remplis.
■ Les champs de contenu textuel correspondant aux type_document_ref où
requis_ou_non = 1 ne doivent pas être vides.
■ nombre_pages doit être un entier positif.
■ La case de confirmation doit être cochée.
■ Le système vérifie (côté serveur) qu'aucun rapport n'est déjà soumis et en
cours de traitement pour l'étudiant et l'année active, sauf si un workflow
spécifique de resoumission après refus (via réclamation) est enclenché.
○ **Logique Algorithmique/SQL (appel à
ServiceRapport.creerEtSoumettreRapportTextuel) :** 1

1. Validation serveur de toutes les données saisies.
2. Si validation échoue, retour au formulaire avec messages d'erreur.
3. Si validation réussie, début d'une transaction de base de données.
4. Génération d'un id_rapport_etudiant unique (VARCHAR(50)).
5. INSERT INTO rapport_etudiant (id_rapport_etudiant,
    numero_carte_etudiant, id_annee_academique, libelle_rapport_etudiant,
    theme, resume, numero_attestation_stage, nombre_pages,
    date_soumission, id_statut_rapport) VALUES (:id_rapport, :num_etudiant,
    :annee_active, :libelle, :theme, :resume, :num_attest, :nb_pages, NOW(),
    'RAP_SOUMIS');
6. Pour chaque section de contenu textuel fournie par l'étudiant :
    ■ INSERT INTO document_soumis (id_rapport_etudiant,
       id_type_document, contenu_textuel, version, date_soumission_version,
       numero_utilisateur_soumission) VALUES (:id_rapport,
       :id_type_doc_section, :contenu_section, 1, NOW(),
       :num_utilisateur_etudiant);
7. Journalisation de l'action dans enregistrer : id_action =
    "SOUMISSION_CONTENU_RAPPORT", type_entite_concernee =
    "RAPPORT_ETUDIANT", id_entite_concernee = id_rapport_etudiant
    généré.
8. Commit de la transaction. Si une erreur survient, rollback.
○ **Interactions & Post-Soumission :** 1
■ **Verrouillage :** L'interface de soumission initiale est désactivée. L'étudiant
ne peut plus soumettre un _nouveau_ rapport pour cette année, mais pourra
modifier celui-ci s'il est retourné.
■ **Notifications :**
■ Une notification d'accusé de réception est envoyée à l'étudiant (via


ServiceNotification -> recevoir et email).
■ Une notification est envoyée au service de conformité (Agents du
groupe 'GRP_AGENT_CONF') pour les informer qu'un nouveau rapport
est en attente de vérification.
○ **Services Impliqués :** ServiceRapport (pour la création et soumission),
ServiceAuthentification (pour l'identité de l'étudiant), ServiceNotification
(pour l'envoi des notifications), ServiceConfigurationSysteme (pour les types
de documents requis).
● **C.2. Suivi du Processus de Validation
(Frontend/views/Etudiant/Rapport/suivi_rapport.php) (si un rapport est
soumis)**
○ **Objectif :** Fournir à l'étudiant une visibilité claire et en temps réel sur le statut
actuel de son rapport et son avancement dans le workflow de validation. 1
○ **Interface Utilisateur :** 1
■ **Statut Actuel Détaillé :** Affichage proéminent du libelle_statut_rapport
(ex: "En attente de vérification de conformité", "Transmis à la commission",
"Validé").
■ **Historique des Statuts (Optionnel) :** Si une table
historique_statut_rapport est implémentée et alimentée par les services
lors des changements de statut, un historique chronologique des statuts
précédents du rapport peut être affiché.
■ **Commentaires des Validateurs :**
■ Si rapport_etudiant.id_statut_rapport = 'RAP_NON_CONF' (retourné
par la conformité) : Affichage du approuver.commentaire_conformite
correspondant à la dernière vérification de conformité pour ce
rapport.
■ Si rapport_etudiant.id_statut_rapport = 'RAP_REFUSE' ou 'RAP_VALID'
(décision de la commission) : Affichage des recommandations ou de la
décision finale issue du compte_rendu.libelle_compte_rendu (le PV) lié
à ce rapport. _Clarification : si 'RAP_CORRECT' vient de la commission,
le PV contiendra les recommandations, mais il n'y aura pas de
resoumission à la commission._
■ **Contenu Soumis :** Affichage en lecture seule du contenu_textuel de
chaque document_soumis (dernière version pour chaque
id_type_document).
○ **Logique Algorithmique/SQL :** 1
■ Récupération du rapport_etudiant de l'étudiant pour l'année active.
■ Jointure avec statut_rapport_ref pour obtenir libelle_statut_rapport.
■ Si id_statut_rapport = 'RAP_NON_CONF', SELECT commentaire_conformite


FROM approuver WHERE id_rapport_etudiant = :id_rapport ORDER BY
date_verification_conformite DESC LIMIT 1;
■ Si id_statut_rapport = 'RAP_VALID' ou 'RAP_REFUSE', SELECT
libelle_compte_rendu FROM compte_rendu WHERE id_rapport_etudiant =
:id_rapport AND id_statut_pv = 'PV_VALID' ORDER BY date_creation_pv
DESC LIMIT 1;
■ Pour le contenu soumis :
SQL
SELECT ds.contenu_textuel, td.libelle_type_document
FROM document_soumis ds
JOIN type_document_ref td ON ds.id_type_document =
td.id_type_document
WHERE ds.id_rapport_etudiant = :id_rapport
AND ds.version = (SELECT MAX(v.version)
FROM document_soumis v
WHERE v.id_rapport_etudiant = ds.id_rapport_etudiant
AND v.id_type_document = ds.id_type_document);
○ **Services Impliqués :** ServiceRapport (pour l'état et le contenu du rapport),
ServiceConformite (pour les commentaires de conformité),
ServiceCommission (pour les commentaires/PV de la commission).
● **C.3. Gestion des Corrections du Contenu
(Frontend/views/Etudiant/Rapport/soumettre_corrections.php) (si
id_statut_rapport = 'RAP_NON_CONF')**
○ **Objectif :** Permettre à l'étudiant de modifier le contenu et les métadonnées
de son rapport lorsque celui-ci a été retourné pour non-conformité par
l'Agent de Contrôle de Conformité. 1
○ **Déclenchement :** L'interface devient active si
rapport_etudiant.id_statut_rapport = 'RAP_NON_CONF'.
○ **Interface Utilisateur :** 1
■ Affichage clair des motifs de non-conformité et des commentaires de
l'agent (approuver.commentaire_conformite).
■ Formulaire similaire à celui de la soumission initiale (C.1), mais pré-rempli
avec le contenu_textuel de la version actuelle du rapport (la plus récente
dans document_soumis).
■ Champ texte pour "Note expliquant les modifications apportées"
(obligatoire ou fortement recommandé).
○ **Règles Métier & Validations :** 1
■ L'étudiant doit adresser les points de non-conformité soulevés.


```
■ La "Note expliquant les modifications" est souvent requise pour aider
l'agent de conformité lors de la nouvelle vérification.
■ Les validations standards sur le contenu et les métadonnées s'appliquent.
○ Logique Algorithmique/SQL (appel à
ServiceRapport.soumettreCorrectionsRapportTextuel) : 1
```
1. Validation serveur des champs modifiés.
2. Pour chaque section de contenu_textuel modifiée :
    ■ Récupérer la MAX(version) actuelle pour ce id_rapport_etudiant et
       id_type_document.
    ■ INSERT INTO document_soumis avec la version incrémentée et le
       nouveau contenu_textuel. Cela conserve l'historique des versions.
3. UPDATE rapport_etudiant SET... (pour les métadonnées modifiées),
    date_derniere_modif = NOW(), et id_statut_rapport passe à
    'RAP_CORRECT_SOUMISES_CONF' (indiquant que les corrections pour la
    conformité ont été resoumises).
4. La "Note expliquant les modifications apportées" est stockée, par
    exemple, comme une nouvelle entrée dans document_soumis avec un
    id_type_document spécifique (ex: 'DOC_NOTE_CORRECTION_CONF').
5. Journalisation de l'action dans enregistrer (id_action =
    "RESUMISSION_CORRECTIONS_CONFORMITE").
6. Transaction DB.
○ **Interactions & Post-Resoumission :** 1
■ L'interface de modification est à nouveau verrouillée.
■ Notification à l'Agent de Contrôle de Conformité que les corrections ont
été resoumises.
○ **Services Impliqués :** ServiceRapport, ServiceNotification.
● **C.4. Cas : Rapport Non Validé par la Commission (id_statut_rapport =
'RAP_REFUSE')**
○ **Objectif :** Informer l'étudiant du refus de son rapport par la commission et lui
présenter les options possibles. 1
○ **Interface Utilisateur :** 1
■ Affichage clair de la décision de refus et des raisons/recommandations
issues du PV de la commission (compte_rendu.libelle_compte_rendu).
■ **Option 1 (Modification du rapport actuel - si autorisé par le
règlement de l'établissement pour un refus) :** "Modifier le contenu de
mon rapport actuel et le resoumettre pour une nouvelle évaluation de
conformité (puis commission)."
■ Si cette option est choisie (et permise), l'interface C.3 (Gestion des
Corrections) pourrait devenir active. Le statut id_statut_rapport


pourrait passer à un état intermédiaire comme
'RAP_REFUSE_MODIF_EN_COURS'. La resoumission suivrait le flux
normal (conformité puis commission). _Cette option semble moins
probable compte tenu de la clarification sur les corrections de la
commission._
■ **Option 2 (Reprise du processus avec un nouveau rapport/stage -
voie privilégiée après un refus ferme) :**
■ **Message :** "Votre rapport a été refusé par la commission. Pour
soumettre un nouveau rapport (ce qui peut impliquer un nouveau
stage ou une revalidation de votre stage actuel), veuillez initier une
'Demande de Reprise de Processus Rapport' via l'onglet 'Mes
Réclamations'."
■ **Action Système :** Le rapport_etudiant actuel (refusé) voit son statut
mis à jour à 'RAP_REFUSE_ARCHIVE' (un statut terminal indiquant un
refus archivé). 1
○ **Règles Métier :** 1
■ Un refus par la commission est une décision majeure.
■ La reprise du processus est conditionnée par une réclamation formelle et
une validation par le Responsable Scolarité (notamment pour le nouveau
stage).
■ L'interface de soumission initiale (C.1) reste verrouillée pour un nouveau
rapport tant que la réclamation n'est pas traitée et qu'un nouveau
faire_stage (si requis) n'est pas validé par le RS. Ce dernier point est
crucial : la validation par le RS d'un nouveau contexte de stage (ou la
revalidation de l'ancien pour une nouvelle tentative) "débloque" la
possibilité pour l'étudiant de faire une nouvelle soumission.
○ **Services Impliqués :** ServiceRapport (pour archiver le rapport refusé),
ServiceReclamation (pour la demande de reprise).
● **C.5. Cas : Rapport Validé par la Commission (id_statut_rapport =
'RAP_VALID')**
○ **Objectif :** Informer l'étudiant du succès de la validation de son rapport et lui
donner accès au document officiel de validation (PV). 1
○ **Interface Utilisateur :** 1
■ Message de félicitations proéminent.
■ Affichage (ou résumé) du contenu du PV validé
(compte_rendu.libelle_compte_rendu).
■ Lien clair vers l'onglet "Mes Documents PDF" (D) où le PV officiel au
format PDF peut être téléchargé.
○ **Règles Métier :** Ceci est un statut terminal pour le workflow de validation du


rapport. Toutes les actions de soumission/modification pour ce rapport sont
définitivement verrouillées. 1
○ **Services Impliqués :** ServiceRapport (pour l'affichage du statut),
ServiceDocumentGenerator (indirectement, car le PDF du PV est généré par
le module commission/admin et rendu accessible).
**D. Onglet: Mes Documents PDF (Frontend/views/Etudiant/mes_documents.php)**
● **Objectif :** Fournir à l'étudiant un emplacement centralisé et sécurisé pour
accéder et télécharger tous les documents PDF officiels générés par le système
le concernant. 1
● **Interface Utilisateur :** 1
○ **Liste des Documents :** Un tableau avec les colonnes : "Nom du Document",
"Date de Génération", "Action".
○ **Exemples de Documents :** "Attestation de Dépôt de Rapport -",
"Procès-Verbal de Validation -", "Bulletin de Notes - Année", "Attestation de
Scolarité - Année", "Reçu de Paiement des Frais d'Inscription".
○ **Interaction :** Un bouton "Télécharger (PDF)" pour chaque document listé.
● **Règles Métier & Validations :** 1
○ Les documents sont générés par les modules Administration ou Personnel
Administratif (via ServiceDocumentGenerator).
○ L'accès est en lecture seule pour l'étudiant.
○ L'accès à un document est strictement limité à l'étudiant qu'il concerne.
● **Logique Algorithmique/SQL :** 1
○ Les documents peuvent être stockés physiquement sur le serveur avec leurs
métadonnées dans une table document_officiel_genere (PK id_doc_off,
numero_utilisateur_concerne FK, type_doc_officiel, chemin_fichier_pdf,
date_generation, genere_par_num_user FK). Si cette table existe :
SQL
SELECT id_doc_off, type_doc_officiel, date_generation, chemin_fichier_pdf
FROM document_officiel_genere
WHERE numero_utilisateur_concerne = :numero_utilisateur_connecte
ORDER BY date_generation DESC;
○ Alternativement, certains documents pourraient être générés à la volée si les
données sources sont statiques et finalisées (ex: un PV validé).
○ Lors du clic sur "Télécharger", le serveur récupère le fichier PDF (depuis
chemin_fichier_pdf ou le génère) et l'envoie avec les en-têtes HTTP
appropriés pour le téléchargement.
● **Services Impliqués :** ServiceDocumentGenerator (pour la génération initiale par


d'autres rôles), ServiceAuthentification (pour le contexte utilisateur et
l'autorisation d'accès aux documents).
**E. Onglet: Mes Réclamations (Frontend/views/Etudiant/Reclamation/)**
● **Objectif :** Offrir un canal formel et structuré pour que les étudiants puissent
soumettre des requêtes, signaler des problèmes, ou demander formellement la
reprise d'un processus (par exemple, la soumission d'un rapport après un refus,
impliquant potentiellement un nouveau stage). 1
● **Interface Utilisateur :**
○ **E.1. Soumission d'une Nouvelle Réclamation
(Frontend/views/Etudiant/Reclamation/soumettre_reclamation.php) :** 1
■ Bouton "Faire une Nouvelle Réclamation".
■ **Formulaire de Soumission :**
■ sujet_reclamation (Sujet de la réclamation) : Champ texte, obligatoire.
■ id_type_reclamation (Type de réclamation) : Liste déroulante peuplée
depuis type_reclamation_ref (ex: "Problème Technique", "Question sur
le Statut du Rapport", "Demande de Reprise du Processus Rapport
(Nouveau Stage)", "Erreur sur le Bulletin de Notes"), obligatoire.
■ description_reclamation (Description de la réclamation) : Éditeur de
texte enrichi, obligatoire.
■ **Section Spécifique si id_type_reclamation =
"DEM_REPRISE_STAGE" (Demande de Reprise de Processus
Rapport avec Nouveau Stage) :** 1
■ Case à cocher : "Je confirme vouloir reprendre le processus de
soumission de rapport pour l'année académique [Année Active] en
utilisant un nouveau stage (différent de celui associé à mon
précédent rapport refusé)." (Obligatoire si ce type est
sélectionné).
■ Question : "Comment souhaitez-vous procéder pour la mise à jour
de vos informations de stage?"
■ **Option 1 : "En ligne (informations préliminaires) :** Je vais
fournir ci-dessous des informations sur mon nouveau stage. Je
comprends que je devrai ensuite rencontrer le Responsable
Scolarité avec les justificatifs (convention signée) pour
validation finale avant que mon compte ne soit réactivé pour
une nouvelle soumission."
■ Champs supplémentaires (facultatifs à ce stade, mais
utiles) : Nom de la nouvelle entreprise, dates
prévisionnelles du stage, sujet envisagé.


■ **Option 2 : "En présentiel uniquement :** Je contacterai
directement le Responsable Scolarité pour discuter de mon
nouveau stage et fournir les documents."
■ **Règle Métier :** L'étudiant NE TÉLÉVERSE PAS de convention de
stage ici. Il fournit des informations textuelles préliminaires ou
indique un contact direct.
○ **E.2. Suivi des Réclamations Soumises
(Frontend/views/Etudiant/Reclamation/suivi_reclamations.php) :** 1
■ Tableau affichant les réclamations soumises par l'étudiant avec les
colonnes : id_reclamation, sujet_reclamation, date_soumission,
libelle_statut_reclamation (via jointure avec statut_reclamation_ref),
date_reponse (si traitée).
■ Action "Voir Détails" par ligne : Affiche la description_reclamation
complète et la reponse_reclamation (si disponible).
● **Règles Métier & Validations :** 1
○ Tous les champs obligatoires du formulaire de réclamation doivent être
remplis.
○ Si le type "DEM_REPRISE_STAGE" est sélectionné, la case de confirmation est
obligatoire.
○ Le système n'autorise pas le téléversement de fichiers pour les réclamations.
● **Logique Algorithmique/SQL (appel à ServiceReclamation.creerReclamation)
:** 1

1. Validation serveur de tous les champs du formulaire.
2. INSERT INTO reclamation (numero_carte_etudiant, sujet_reclamation,
    id_type_reclamation, description_reclamation, date_soumission,
    id_statut_reclamation) VALUES (:num_etudiant, :sujet, :id_type, :description,
    NOW(), 'RECLAM_RECUE'); (Le numero_carte_etudiant est celui de l'étudiant
    connecté).
3. **Logique Spécifique pour "DEM_REPRISE_STAGE" :**
    ■ Si l'option "En présentiel uniquement" est choisie, ServiceReclamation
       peut notifier ServiceAuthentification pour potentiellement changer
       utilisateur.statut_compte à 'SUSPENDU_ATTENTE_RS_STAGE'. Ce statut
       doit être ajouté à l'ENUM de utilisateur.statut_compte et la logique d'accès
       au module de soumission de rapport (C.1) doit vérifier ce statut pour
       bloquer l'accès si nécessaire.
4. Journalisation de l'action dans enregistrer.
5. Transaction DB.
● **Services Impliqués :** ServiceReclamation (pour la création et le suivi),
ServiceNotification (pour les accusés de réception et alertes au personnel),


ServiceAuthentification (pour la gestion potentielle du statut du compte
utilisateur).
● **Interactions :** 1
○ L'étudiant reçoit une notification d'accusé de réception de sa réclamation.
○ Le service administratif concerné (ex: Responsable Scolarité pour
"DEM_REPRISE_STAGE") est notifié de la nouvelle réclamation.
○ Si le compte est suspendu, l'accès de l'étudiant à la soumission de rapport est
bloqué jusqu'à ce que le Responsable Scolarité traite la réclamation et
réactive le compte.
**F. Onglet: Ressources & Aide (Frontend/views/Etudiant/ressources_etudiant.php)**
● **Objectif :** Mettre à disposition des étudiants des documents utiles, des guides,
une FAQ, et des informations de contact pour les accompagner durant le
processus de rédaction et de soumission de leur rapport. 1
● **Interface Utilisateur :** 1
○ **F.1. Guides et Modèles (Contenu Textuel ou Liens Externes) :**
■ Guide officiel de rédaction des rapports (affiché en contenu HTML
directement dans l'interface ou lien vers un PDF externe géré par
l'Administrateur Système).
■ Modèles de plan de rapport, modèles de page de garde (fournis sous
forme de texte structuré que les étudiants peuvent copier et adapter).
■ Critères d'évaluation des rapports (description textuelle).
○ **F.2. Foire Aux Questions (FAQ) :** Une liste des questions fréquemment
posées et leurs réponses, potentiellement avec une fonction de recherche.
○ **F.3. Contacts Utiles :** Coordonnées des services pertinents (ex: Scolarité,
Support Technique, Conseillers Pédagogiques).
● **Règles Métier & Validations :** Le contenu est en lecture seule pour les étudiants.
1
● **Logique Algorithmique/SQL :** 1
○ Le contenu peut être stocké dans une table de gestion de contenu simple (ex:
ressources_aide (id_ressource VARCHAR(50) PK, titre VARCHAR(255),
contenu TEXT, type_contenu ENUM('guide', 'faq', 'contact'))) ou géré comme
des fichiers HTML statiques sur le serveur, accessibles via des liens.
● **Services Impliqués :** Aucun service spécifique pour l'interaction étudiante,
principalement récupération de contenu.
● **Interactions :** Fournit un support passif et des informations aux étudiants.
**Clarification sur les Corrections Demandées par la Commission et Impact sur le
Module Étudiant**


Conformément à la demande, si les "corrections" mentionnées par la commission
concernent uniquement le PV et n'impliquent _pas_ un retour du rapport à l'étudiant
pour resoumission à la commission :
● **Impact sur C.2 (Suivi du Processus) :** Si rapport_etudiant.id_statut_rapport
devient 'RAP_CORRECT' (ou un statut équivalent signifiant "Validé avec
réserves/recommandations"), le commentaire affiché à l'étudiant proviendra
toujours du compte_rendu.libelle_compte_rendu (PV). Ce commentaire listera les
points à améliorer pour une version future ou pour archivage, mais n'appellera
pas à une resoumission _à la commission_.
● **Impact sur C.3 (Gestion des Corrections) :** Cette section ne serait activée que
si id_statut_rapport = 'RAP_NON_CONF' (retour par le service de conformité). Elle
ne le serait _pas_ pour un statut 'RAP_CORRECT' émanant de la commission.
● **Impact sur C.4 (Cas de Refus) :** Si la commission estime que des modifications
substantielles sont nécessaires au point de ne pas valider le rapport, le statut
deviendra 'RAP_REFUSE'. L'étudiant devra alors passer par une réclamation (E.1)
pour une "Demande de Reprise de Processus Rapport", impliquant
potentiellement un nouveau stage et une _nouvelle soumission complète_ du
rapport (retour à C.1 après validation de la reprise par le RS), et non une simple
correction du rapport refusé pour une nouvelle évaluation par la même
commission.
Cette interprétation maintient la commission comme une instance de décision finale
(validation ou refus) sans cycle itératif de correction/resoumission direct avec
l'étudiant via ce module. Les "corrections" de la commission sont des
recommandations ou des conditions pour la note finale/validation, mais pas un appel
à une nouvelle évaluation du même rapport par la commission.
**Tables SQL Primordialement Impliquées (Module Étudiant - Synthèse Révisée)**^1
● **Profil et Compte :** etudiant, utilisateur, historique_mot_de_passe.
● **Contexte Académique :** annee_academique, inscrire, statut_paiement_ref,
faire_stage, entreprise.
● **Gestion du Rapport :** rapport_etudiant, statut_rapport_ref, document_soumis
(pour contenu_textuel et versions), type_document_ref.
● **Consultation des Retours :** approuver (commentaires de conformité),
compte_rendu (PV et recommandations/décisions de la commission).
● **Communication :** recevoir, notification, message.
● **Réclamations :** reclamation, statut_reclamation_ref, type_reclamation_ref.
● **Consultation de Documents :** evaluer, ecue, ue (pour les données des bulletins


de notes PDF), potentiellement document_officiel_genere (pour tracer les PDF
générés).
● **Audit :** enregistrer (pour les actions de l'étudiant comme la soumission, la
modification de profil).
Cette description détaillée du Module Étudiant, intégrant la gestion textuelle des
rapports et la clarification sur le processus de correction par la commission, vise à
fournir une base solide pour la compréhension de ses fonctionnalités et de sa logique
interne.
**Works cited**

1. manueld-aho-parrain.txt


