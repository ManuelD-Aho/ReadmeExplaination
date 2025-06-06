Absolument. Nous allons reprendre la rédaction exhaustive du **Module Administration de A à Z**, en intégrant toutes les clarifications et en étant aussi détaillé que possible, avec l'objectif (théorique, car difficilement atteignable en pratique pour un nombre de tokens aussi précis) d'une grande verbosité.

Je vais structurer la réponse en suivant les sections que nous avions définies, en commençant par le **Header Proposé** et la **Sidebar Dynamique**, puis en détaillant chaque fonctionnalité (A, B, C, D, E, F, G).

---

**Module Administration : Description Détaillée Exhaustive (Version Finale Révisée)**

**1. Header Proposé de l'Interface d'Administration**

*   **Intitulé :** "Panneau de Contrôle Principal - GestionMySoutenance"
*   **Objectif :** Identifier clairement et sans ambiguïté la section de l'application réservée à l'administration de haut niveau. "GestionMySoutenance" ancre l'outil dans le nom global du projet, tandis que "Panneau de Contrôle Principal" indique sa fonction centrale de supervision et de configuration.
*   **Affichage :** Visible en permanence en haut de chaque page du module administration, potentiellement à côté du logo de l'institution ou de l'application.
*   **Fonctionnalités associées au header (communes) :**
    *   **Nom de l'Administrateur connecté :** Affiche le nom et prénom de l'utilisateur administrateur actuellement connecté (`utilisateur.login_utilisateur` ou jointure avec `personnel_administratif` si l'admin est aussi un personnel avec profil détaillé).
    *   **Lien vers le profil utilisateur de l'Admin :** Permettant de modifier son propre mot de passe, ses informations de contact de base (si applicables pour un admin pur).
    *   **Bouton/Lien de Déconnexion :** Permet de clore la session administrative de manière sécurisée. Déclenche l'invalidation de la session côté serveur et redirige vers la page de connexion. L'action est loguée dans `enregistrer`.
    *   **Indicateur d'Année Académique Active :** Peut-être un petit affichage discret rappelant l'`id_annee_academique` (ex: "AA_2024_2025") ou le `libelle_annee_academique` (ex: "2024-2025") qui est actuellement marquée comme `est_active = 1` dans la table `annee_academique`. Cela permet à l'admin de toujours avoir ce contexte critique en vue.

**2. Sidebar Dynamique et Fonctionnalités Associées (Menu de Navigation Principal du Module Administration)**

La sidebar (barre latérale de navigation) est l'outil principal permettant à l'administrateur de naviguer entre les différentes sections et fonctionnalités du module. Elle doit être claire, bien organisée, et potentiellement dynamique (certains items pourraient n'apparaître que si des sous-modules sont activés, bien que dans notre cas, toutes les fonctionnalités sont supposées présentes). Chaque élément de la sidebar est un lien vers une interface (un "onglet" ou une "section") spécifique du module.

*   **Structure Hiérarchique de la Sidebar :**
    *   **Niveau 1 : Sections Principales**
    *   **Niveau 2 : Sous-sections ou Onglets Spécifiques (si la section principale est complexe)**

*   **Éléments de la Sidebar et Fonctionnalités Pointées :**

    *   **Tableau de Bord Principal**
        *   **Libellé Sidebar :** "Tableau de Bord" ou "Accueil Admin"
        *   **Icône :** Souvent une icône de type "maison", "tableau de bord", "graphique".
        *   **Fonctionnalité Pointée :** Section A. Tableau de Bord Principal (détaillée plus bas). Affiche la vue d'ensemble, les KPIs, les alertes, et les raccourcis.
        *   **Interaction :** Cliquer sur cet item charge la page principale du tableau de bord administratif.

    *   **Gestion des Utilisateurs**
        *   **Libellé Sidebar :** "Utilisateurs" ou "Gestion des Comptes"
        *   **Icône :** Souvent une icône de type "groupe de personnes", "utilisateurs".
        *   **Comportement :** Cet item est un menu déroulant (ou une section avec sous-items) menant aux sous-sections suivantes :
            *   **Sous-item : Utilisateurs (Vue Globale)**
                *   **Libellé Sidebar :** "Tous les Utilisateurs"
                *   **Fonctionnalité Pointée :** Section B.0. Utilisateurs (Vue Générale et Actions Transversales).
            *   **Sous-item : Étudiants**
                *   **Libellé Sidebar :** "Étudiants"
                *   **Fonctionnalité Pointée :** Section B.1. Gestion des Étudiants.
            *   **Sous-item : Personnel Administratif**
                *   **Libellé Sidebar :** "Personnel Administratif"
                *   **Fonctionnalité Pointée :** Section B.2. Gestion du Personnel Administratif.
            *   **Sous-item : Enseignants**
                *   **Libellé Sidebar :** "Enseignants"
                *   **Fonctionnalité Pointée :** Section B.3. Gestion des Enseignants.

    *   **Gestion des Habilitations**
        *   **Libellé Sidebar :** "Habilitations" ou "Droits & Permissions"
        *   **Icône :** Souvent une icône de type "clé", "bouclier", "engrenage de sécurité".
        *   **Comportement :** Menu déroulant pour les sous-sections :
            *   **Sous-item : Types Utilisateur (Rôles)**
                *   **Libellé Sidebar :** "Types d'Utilisateur"
                *   **Fonctionnalité Pointée :** Section C.1. Gestion des Types Utilisateur.
            *   **Sous-item : Groupes Utilisateur**
                *   **Libellé Sidebar :** "Groupes d'Utilisateurs"
                *   **Fonctionnalité Pointée :** Section C.2. Gestion des Groupes Utilisateur.
            *   **Sous-item : Niveaux d'Accès aux Données**
                *   **Libellé Sidebar :** "Niveaux d'Accès"
                *   **Fonctionnalité Pointée :** Section C.3. Gestion des Niveaux d'Accès aux Données.
            *   **Sous-item : Permissions (Fonctionnalités)**
                *   **Libellé Sidebar :** "Fonctionnalités Système (Traitements)" ou "Permissions Applicatives"
                *   **Fonctionnalité Pointée :** Section C.4.1. Gestion des Fonctionnalités/Traitements (`traitement`).
            *   **Sous-item : Assignation des Permissions**
                *   **Libellé Sidebar :** "Assigner Permissions aux Groupes"
                *   **Fonctionnalité Pointée :** Section C.4.2. Assignation des Permissions (`rattacher`).

    *   **Configuration Système**
        *   **Libellé Sidebar :** "Configuration Système" ou "Paramètres"
        *   **Icône :** Souvent une icône de type "engrenage", "outils".
        *   **Comportement :** Menu déroulant pour les sous-sections :
            *   **Sous-item : Gestion des Référentiels**
                *   **Libellé Sidebar :** "Référentiels"
                *   **Fonctionnalité Pointée :** Section D.1. Interface principale pour lister et accéder au CRUD de chaque référentiel (Années Académiques, Niveaux d'Étude, Spécialités, Statuts divers, etc.). Une page "liste_referentiels.php" qui ensuite route vers "crud_referentiel_generique.php" avec le nom de la table en paramètre est une approche. La gestion de `annee_academique` pourrait avoir son propre sous-menu ou lien direct à cause de son importance.
            *   **Sous-item : Année Académique (spécifique pour D.1.1)**
                *   **Libellé Sidebar :** "Années Académiques" (Si gestion fréquente et critique, mérite un lien direct).
                *   **Fonctionnalité Pointée :** CRUD pour la table `annee_academique`.
            *   **Sous-item : Paramètres Applicatifs & Workflow**
                *   **Libellé Sidebar :** "Paramètres Généraux"
                *   **Fonctionnalité Pointée :** Section D.2. Configuration des dates limites, règles de validation, alertes, etc.
            *   **Sous-item : Modèles de Documents & Notifications**
                *   **Libellé Sidebar :** "Modèles (Documents/Emails)"
                *   **Fonctionnalité Pointée :** Section D.3. Gestion des gabarits PDF et des templates de `message`.

    *   **Gestion Académique & Administrative (Configuration & Supervision)**
        *   **Libellé Sidebar :** "Gestion Académique" ou "Données Académiques"
        *   **Icône :** Souvent une icône de type "livre", "diplôme".
        *   **Comportement :** Menu déroulant :
            *   **Sous-item : Inscriptions**
                *   **Libellé Sidebar :** "Supervision Inscriptions"
                *   **Fonctionnalité Pointée :** Section E.1. Consultation globale et intervention.
            *   **Sous-item : Évaluations / Notes**
                *   **Libellé Sidebar :** "Supervision Notes"
                *   **Fonctionnalité Pointée :** Section E.2.
            *   **Sous-item : Stages**
                *   **Libellé Sidebar :** "Supervision Stages"
                *   **Fonctionnalité Pointée :** Section E.3.
            *   **Sous-item : Associations Enseignants**
                *   **Libellé Sidebar :** "Associations Enseignants"
                *   **Fonctionnalité Pointée :** Section E.4. Gestion des grades, fonctions, spécialités des enseignants.

    *   **Supervision & Maintenance**
        *   **Libellé Sidebar :** "Supervision & Maintenance"
        *   **Icône :** Souvent une icône de type "œil", "loupe", "clé à molette".
        *   **Comportement :** Menu déroulant :
            *   **Sous-item : Suivi des Workflows**
                *   **Libellé Sidebar :** "Suivi des Workflows"
                *   **Fonctionnalité Pointée :** Section F.1.
            *   **Sous-item : Gestion des PV (Admin)**
                *   **Libellé Sidebar :** "Gestion des Procès-Verbaux"
                *   **Fonctionnalité Pointée :** Section F.2.
            *   **Sous-item : Gestion des Notifications Système**
                *   **Libellé Sidebar :** "Notifications Système"
                *   **Fonctionnalité Pointée :** Section F.3.
            *   **Sous-item : Journaux d'Audit**
                *   **Libellé Sidebar :** "Journaux d'Audit"
                *   **Fonctionnalité Pointée :** Section F.4.
            *   **Sous-item : Outils d'Import/Export Données**
                *   **Libellé Sidebar :** "Import/Export Données"
                *   **Fonctionnalité Pointée :** Section F.5.
            *   **Sous-item : Maintenance Technique**
                *   **Libellé Sidebar :** "Maintenance Technique"
                *   **Fonctionnalité Pointée :** Section F.6.

    *   **Reporting & Analytique**
        *   **Libellé Sidebar :** "Reporting & Analytique"
        *   **Icône :** Souvent une icône de type "graphique à barres", "camembert".
        *   **Comportement :** Menu déroulant :
            *   **Sous-item : Génération de Rapports**
                *   **Libellé Sidebar :** "Générer Rapports"
                *   **Fonctionnalité Pointée :** Section G.1.
            *   **Sous-item : Configurer Tableaux de Bord**
                *   **Libellé Sidebar :** "Configurer Dashboards"
                *   **Fonctionnalité Pointée :** Section G.2.

*   **Considérations pour la Sidebar :**
    *   **Clarté et Intuitivité :** Les libellés doivent être courts et explicites. Les icônes aident à la reconnaissance rapide.
    *   **Réactivité :** La sidebar doit se charger rapidement et indiquer clairement quelle section est actuellement active.
    *   **Permissions :** Bien que l'Admin Système ait accès à tout, si des rôles d'administrateurs délégués étaient créés (ex: Admin Scolarité avec accès limité), la sidebar devrait dynamiquement afficher uniquement les items autorisés pour ce rôle/groupe (logique de vérification des permissions sur chaque item de menu).

La sidebar est l'épine dorsale de la navigation dans le module d'administration. Sa bonne conception est essentielle pour l'efficacité de l'administrateur.

---

**3. Fonctionnalités Détaillées (Contenu des Onglets / Sections) - Début de la Section A**

**(Comme vous avez déjà le détail de la section A du message précédent, je vais directement passer à B.0 comme point de départ pour le reste de la description.)**

Est-ce que cette approche pour le Header et la Sidebar, avant de replonger dans B.0, correspond à vos attentes de détail et d'exhaustivité ? Nous pouvons ajuster si nécessaire avant de poursuivre.


Absolument. Réécrivons et re-détaillons la section **A. Tableau de Bord Principal** du Module Administration avec le niveau d'exhaustivité souhaité, en s'assurant de l'intégration des dernières modifications de schéma (PKs VARCHAR manuelles, `libelle_...`, pas de `code_...`, pas de `description_...` dans les tables de référence, et consolidation email/photo/statut utilisateur).

---

**3. Fonctionnalités Détaillées (Contenu des Onglets / Sections)**

**A. Tableau de Bord Principal (Accès via Sidebar : "Tableau de Bord" / "Accueil Admin")**

Le Tableau de Bord Principal constitue la page d'accueil par défaut et le centre névralgique pour l'administrateur système lorsqu'il se connecte au module d'administration de "GestionMySoutenance". Cette interface est conçue pour offrir une synthèse visuelle, concise et pertinente de l'état actuel de la plateforme, des indicateurs de performance clés, des alertes nécessitant une action immédiate, et des raccourcis vers les fonctionnalités d'administration les plus fréquemment utilisées. Son rôle est d'optimiser l'efficacité de l'administrateur en lui fournissant un aperçu global lui permettant de prioriser ses actions.

*   **Objectif Spécifique :** Fournir une vue d'ensemble en temps réel (ou quasi réel) des métriques vitales de la plateforme, des anomalies potentielles, et un point de départ ergonomique pour la navigation vers des tâches administratives plus spécifiques. Il vise à réduire le temps de diagnostic et à faciliter une gestion proactive du système.

*   **Contenu Affiché et Fonctionnalités Détaillées :**
    Cette section est typiquement organisée en "widgets" ou "cartes" thématiques.

    *   **A.1. Bloc/Widget : Statistiques d'Utilisation Clés et d'Activité**
        *   **Sous-Objectif :** Quantifier l'utilisation de la plateforme et l'activité des processus métier principaux.
        *   **A.1.1. Nombre Total d'Utilisateurs Actifs et Répartition :**
            *   **Source des Données :** Interrogation de la table `utilisateur`.
            *   **Calcul Principal :** `SELECT COUNT(numero_utilisateur) FROM utilisateur WHERE statut_compte = 'actif';` (Rappel: `statut_compte` est un ENUM, 'actif' signifie opérationnel).
            *   **Affichage Principal :** Un chiffre unique, large et clairement visible, libellé "Utilisateurs Actifs".
            *   **Détail Approfondi (Accessible par un clic, un survol, ou dans un sous-widget) :** Répartition par type d'utilisateur.
                *   **Source :** `SELECT tu.libelle_type_utilisateur, COUNT(u.numero_utilisateur) AS nombre_actifs`
                    `FROM utilisateur u`
                    `JOIN type_utilisateur tu ON u.id_type_utilisateur = tu.id_type_utilisateur`
                    `WHERE u.statut_compte = 'actif'`
                    `GROUP BY tu.id_type_utilisateur, tu.libelle_type_utilisateur;`
                *   **Affichage :** Une liste ou un petit graphique à barres indiquant, par exemple :
                    *   "Étudiants Actifs : [Nombre]" (basé sur `id_type_utilisateur` = 'TYPE_ETUD')
                    *   "Enseignants Actifs : [Nombre]" (basé sur `id_type_utilisateur` = 'TYPE_ENS')
                    *   "Personnel Administratif Actif : [Nombre]" (basé sur `id_type_utilisateur` = 'TYPE_PERS_ADMIN')
                    *   "Administrateurs Actifs : [Nombre]" (basé sur `id_type_utilisateur` = 'TYPE_ADMIN')
                *   **Liaison :** Un clic sur chaque catégorie pourrait mener à la liste filtrée des utilisateurs correspondants (Section B).

        *   **A.1.2. Statistiques sur les Rapports de Soutenance (pour l'année académique sélectionnée, par défaut l'active) :**
            *   **Source des Données :** Principalement la table `rapport_etudiant` et sa jointure avec `statut_rapport_ref`. Nécessite une jointure avec `etudiant`, `inscrire`, et `annee_academique` pour filtrer par année.
            *   **Logique d'Affichage :** L'administrateur peut sélectionner une `id_annee_academique` spécifique via une liste déroulante sur le tableau de bord pour contextualiser ces statistiques. Par défaut, l'année où `annee_academique.est_active = 1` est utilisée.
            *   **Calculs :**
                *   `SELECT sr.libelle_statut_rapport, COUNT(r.id_rapport_etudiant) AS nombre_rapports`
                *   `FROM rapport_etudiant r`
                *   `JOIN statut_rapport_ref sr ON r.id_statut_rapport = sr.id_statut_rapport`
                *   `JOIN etudiant etu ON r.numero_carte_etudiant = etu.numero_carte_etudiant`
                *   `JOIN inscrire i ON etu.numero_carte_etudiant = i.numero_carte_etudiant`
                *   `WHERE i.id_annee_academique = '[ID_ANNEE_SELECTIONNEE_OU_ACTIVE]'`
                *   `GROUP BY sr.id_statut_rapport, sr.libelle_statut_rapport`
                *   `ORDER BY sr.etape_workflow;` (l'attribut `etape_workflow` dans `statut_rapport_ref` est crucial pour un ordre logique).
            *   **Affichage Visuel :**
                *   Un diagramme à barres ou un tableau synthétique présentant le nombre de rapports pour chaque `libelle_statut_rapport` clé (ex: 'RAP_SOUMIS', 'RAP_EN_VERIF_CONF' [si un tel statut existe], 'RAP_CONF', 'RAP_NON_CONF', 'RAP_EN_COMM', 'RAP_VALID', 'RAP_REFUSE', 'RAP_CORRECT').
                *   **Total Rapports Année :** Un chiffre global pour l'année sélectionnée.
                *   **Pourcentage de Validation Initiale :** % de rapports "RAP_CONF" par rapport aux rapports ayant passé la vérification de conformité.
                *   **Pourcentage de Succès Commission :** % de rapports "RAP_VALID" par rapport aux rapports soumis à la commission.

        *   **A.1.3. Volume de Données et Indicateurs de Stockage :**
            *   **Objectif :** Fournir des indicateurs techniques sur l'utilisation des ressources.
            *   **Source des Données :** Peut nécessiter des commandes SGBD spécifiques (ex: `SHOW TABLE STATUS` en MySQL pour la taille des tables) ou des calculs sur les fichiers.
            *   **Affichage :**
                *   "Taille de la Base de Données : [X] Mo/Go"
                *   "Nombre Total de Documents Téléversés : [Y]" (calculé par `SELECT COUNT(id_document) FROM document_soumis;`).
                *   "Espace Disque Utilisé par les Documents : [Z] Mo/Go" (calculé par `SELECT SUM(taille_fichier) FROM document_soumis;` - Note : `taille_fichier` doit être en octets pour une somme cohérente).
                *   Ces données sont particulièrement utiles pour l'administrateur système pour anticiper les besoins en stockage.

        *   **A.1.4. Nombre de Nouvelles Inscriptions (pour l'année académique sélectionnée/active) :**
            *   **Source des Données :** Table `inscrire`.
            *   **Calcul :** `SELECT COUNT(DISTINCT i.numero_carte_etudiant) FROM inscrire i WHERE i.id_annee_academique = '[ID_ANNEE_SELECTIONNEE_OU_ACTIVE]';`
            *   **Affichage :** Un chiffre clair. Potentiellement une petite courbe de tendance si l'on compare aux années précédentes (nécessite plus de requêtes historiques).

        *   **A.1.5. Indicateurs d'Activité Récente (Optionnel) :**
            *   **Nombre de Connexions (ex: dernières 24h) :**
                *   **Source :** `SELECT COUNT(numero_utilisateur) FROM utilisateur WHERE derniere_connexion >= DATE_SUB(NOW(), INTERVAL 1 DAY);`
            *   **Nombre de Nouveaux Rapports Soumis (ex: dernières 24h) :**
                *   **Source :** `SELECT COUNT(id_rapport_etudiant) FROM rapport_etudiant WHERE date_soumission >= DATE_SUB(NOW(), INTERVAL 1 DAY);`
            *   **Affichage :** Petits indicateurs numériques.

    *   **A.2. Bloc/Widget : Alertes Système Critiques et Notifications Administratives**
        *   **Sous-Objectif :** Attirer l'attention de l'administrateur sur des événements anormaux ou des conditions nécessitant une intervention.
        *   **A.2.1. État de la Base de Données :**
            *   **Source :** Tentative de connexion à la base de données par l'application, capture d'exceptions. Logs du SGBD (si l'application a un moyen de les lire ou de recevoir des signaux).
            *   **Affichage :** Indicateur simple : "BDD : <span style='color:green;'>OK</span>" ou "BDD : <span style='color:red;'>ERREUR - Voir Logs</span>". Le lien mènerait vers une section de logs techniques (partie de F.6).
        *   **A.2.2. Alertes de Performance Serveur (Monitoring) :**
            *   **Source :** Interface avec un outil de monitoring externe ou scripts internes vérifiant des seuils (CPU, RAM, Disque).
            *   **Affichage :** Liste des alertes actives : "Charge CPU : 85% (Seuil Dépassé)", "Espace Disque /var : 92% (Critique)".
        *   **A.2.3. Alertes de Sécurité (Tentatives d'Accès, Comptes Bloqués) :**
            *   **Source :** Table `utilisateur`.
            *   **Affichage :**
                *   "Comptes Utilisateurs Actuellement Bloqués : [Nombre]" (`SELECT COUNT(*) FROM utilisateur WHERE statut_compte = 'bloque';`). Lien vers la liste filtrée des utilisateurs bloqués (B.0).
                *   "Dernières Tentatives de Connexion Infructueuses (par IP/utilisateur) : [Liste des X dernières]" (nécessite une table de log des tentatives, non présente ; alternative: juste le nombre de comptes avec `tentatives_connexion_echouees` > 0).
                *   **Liaison :** Clics menant vers la gestion des utilisateurs ou les journaux d'audit.
        *   **A.2.4. État des Processus Automatisés (Tâches CRON) :**
            *   **Source :** Système de logging interne pour les tâches CRON (à implémenter si des tâches batch importantes existent).
            *   **Affichage :** Pour chaque tâche CRON majeure (ex: "Nettoyage Nocturne des Sessions", "Envoi Massif d'Emails de Rappel") :
                *   Nom de la tâche.
                *   État du dernier lancement : "Succès" / "Échec".
                *   Date et heure du dernier lancement.
                *   Lien vers le log détaillé de la tâche.
        *   **A.2.5. Années Académiques non Clôturées :**
            *   Si la logique métier implique une "clôture" formelle d'une année académique (au-delà de juste la désactiver via `est_active = 0`), le tableau de bord pourrait alerter si des années passées sont toujours dans un état intermédiaire.
            *   Exemple : `SELECT libelle_annee_academique FROM annee_academique WHERE date_fin < CURDATE() AND est_active = 1;` (années passées toujours marquées comme actives).

    *   **A.3. Bloc/Widget : Raccourcis Rapides vers les Fonctionnalités Administratives Fréquentes**
        *   **Sous-Objectif :** Minimiser le nombre de clics pour accéder aux sections les plus utilisées par l'administrateur.
        *   **Affichage :** Une liste de liens hypertextes clairement libellés, potentiellement accompagnés d'icônes.
        *   **Liens Proposés :**
            *   **"Gérer Tous les Utilisateurs"** -> Lien vers la Section B.0.
            *   **"Gérer les Étudiants"** -> Lien vers la Section B.1.
            *   **"Gérer le Personnel Administratif"** -> Lien vers la Section B.2.
            *   **"Gérer les Enseignants"** -> Lien vers la Section B.3.
            *   **"Configurer l'Année Académique Active"** -> Lien direct vers la gestion de la table `annee_academique` (Section D.1.1).
            *   **"Gérer les Groupes d'Utilisateurs"** -> Lien vers la Section C.2.
            *   **"Assigner Permissions aux Groupes"** -> Lien vers la Section C.4.2.
            *   **"Voir Journal des Actions Utilisateurs"** -> Lien vers la Section F.4.1 (table `enregistrer`).
            *   **"Paramètres Applicatifs (Workflow)"** -> Lien vers la Section D.2.
            *   **"Gestion des Référentiels"** -> Lien vers la page principale de la Section D.1.

    *   **Considérations Techniques et d'Interface :**
        *   **Disposition :** Typiquement, une disposition en tableau de bord avec plusieurs "cartes" ou "widgets" pour chaque catégorie d'information. La disposition doit être responsive pour s'adapter à différentes tailles d'écran.
        *   **Actualisation des Données :** Les statistiques clés sont généralement calculées au chargement de la page. Les alertes critiques pourraient bénéficier d'un mécanisme d'actualisation en temps réel ou à intervalle régulier (ex: via AJAX toutes les N minutes) pour une réactivité accrue.
        *   **Performance :** L'ensemble des requêtes SQL nécessaires pour populer ce tableau de bord doit être hautement optimisé pour garantir un chargement rapide. L'utilisation d'index pertinents sur les tables `utilisateur`, `rapport_etudiant`, `inscrire`, etc., est primordiale, notamment sur les colonnes utilisées dans les clauses `WHERE`, `JOIN`, et `GROUP BY`. Pour les statistiques très lourdes, envisager des agrégations précalculées et mises à jour périodiquement.
        *   **Personnalisation (Évolution) :** À terme, permettre à l'administrateur de choisir quels widgets afficher et comment les agencer augmenterait l'utilité du tableau de bord.

Ce Tableau de Bord Principal, ainsi configuré, devient un outil puissant et central pour l'administrateur, lui permettant d'avoir une maîtrise visuelle et réactive sur l'ensemble de la plateforme "GestionMySoutenance".

---
**(Nous avons détaillé la section A. Prêt à continuer avec la section B.0 : Utilisateurs (Vue Générale et Actions Transversales) en suivant ce même niveau d'exhaustivité.)**

Compris. Je vais reprendre la section **B.0. Utilisateurs (Vue Générale et Actions Transversales)** en poussant le niveau de détail encore plus loin, en décrivant les micro-interactions, les validations côté serveur, les messages d'erreur potentiels, et en essayant d'anticiper chaque aspect de l'algorithme et de la liaison avec la base de données, tout en gardant à l'esprit l'objectif (très exigeant) de verbosité.

---

**B. Gestion des Utilisateurs (Accès via Sidebar, sous-menu "Utilisateurs")**

La section "Gestion des Utilisateurs" représente une composante absolument centrale et vitale du Module Administration au sein de l'écosystème "GestionMySoutenance". Sa vocation première est de conférer à l'administrateur système, et potentiellement à des rôles administratifs délégués sous strict contrôle, un pouvoir exhaustif sur le cycle de vie complet de chaque compte utilisateur. Cela englobe la création initiale des comptes, la consultation détaillée des profils et des attributs de sécurité, la modification des informations, qu'elles soient personnelles ou liées aux accès, et enfin la gestion de la fin de vie des comptes, qui se traduit le plus souvent par une désactivation ou un archivage plutôt qu'une suppression physique, afin de préserver l'intégrité historique et référentielle des données. La précision et la sécurité des opérations effectuées dans cette section sont d'une importance capitale, car elles conditionnent directement l'accès aux fonctionnalités pour tous les rôles (Étudiants, Personnel Administratif, Enseignants, Membres de Commission, et autres Administrateurs), la confidentialité des informations personnelles, et la traçabilité des actions au sein de la plateforme. Chaque intervention administrative dans ce périmètre génère des enregistrements d'audit détaillés dans la table `enregistrer`, assurant une redevabilité complète. Les tables `utilisateur`, `etudiant`, `personnel_administratif`, et `enseignant` sont les principales entités de données manipulées, avec des interactions indirectes mais significatives avec les tables définissant les rôles, les groupes, et les niveaux d'accès (`type_utilisateur`, `groupe_utilisateur`, `niveau_acces_donne`).

*   **B.0. Onglet / Section : Utilisateurs (Vue Générale et Actions Transversales)**
    *   **Accès via Sidebar :** Généralement le premier sous-item du menu "Gestion des Utilisateurs", intitulé par exemple "Tous les Utilisateurs" ou "Vue d'Ensemble Utilisateurs". Un clic sur cet item charge l'interface décrite ci-dessous.
    *   **Objectif Stratégique et Opérationnel :**
        *   **Stratégique :** Donner à l'administrateur une vision consolidée de la population des utilisateurs de la plateforme, permettant d'identifier des tendances, de surveiller l'activité globale des comptes, et de s'assurer de la cohérence de la base utilisateurs.
        *   **Opérationnel :** Fournir un point d'entrée unique pour des recherches rapides sur l'ensemble des utilisateurs, indépendamment de leur type principal (Étudiant, Enseignant, etc.), et permettre des actions administratives groupées ou des interventions ciblées qui ne sont pas spécifiques à un seul type de profil. Cet onglet sert d'aiguillage vers les sections de gestion plus spécialisées (B.1, B.2, B.3) tout en offrant des capacités propres.

    *   **Contenu et Fonctionnalités Détaillées de l'Interface :**
        L'interface est typiquement structurée avec une zone de filtres/recherche en haut, suivie d'un tableau paginé des résultats.

        *   **B.0.1. Zone de Listage Exhaustif de Tous les Utilisateurs :**
            *   **Description de l'Affichage :** Le cœur de l'interface est un tableau de données interactif, conçu pour présenter de manière claire et concise tous les enregistrements de la table `utilisateur`. Pour chaque enregistrement `utilisateur`, des informations clés issues de tables liées (comme `type_utilisateur` et `groupe_utilisateur`) sont affichées grâce à des jointures SQL.
            *   **SQL Requête de Base (Exemple Simplifié pour illustrer les jointures) :**
                ```sql
                SELECT
                    u.numero_utilisateur,
                    u.login_utilisateur,
                    u.email_principal,
                    tu.libelle_type_utilisateur,
                    gu.libelle_groupe_utilisateur,
                    u.statut_compte,
                    u.date_creation,
                    u.derniere_connexion
                FROM
                    utilisateur u
                LEFT JOIN
                    type_utilisateur tu ON u.id_type_utilisateur = tu.id_type_utilisateur
                LEFT JOIN
                    groupe_utilisateur gu ON u.id_groupe_utilisateur = gu.id_groupe_utilisateur
                --potentiels filtres et clauses ORDER BY ici--
                LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
                ```
            *   **Détail des Colonnes Principales Affichées (et leurs implications) :**
                *   **`numero_utilisateur` (Source : `utilisateur.numero_utilisateur`, VARCHAR(50), PK)**
                    *   **Description :** Identifiant unique global et interne pour chaque compte utilisateur. Généré manuellement par la logique PHP lors de la création (ex: "USR_ETU_ suivi d'un UUID court, ou "USR_ENS_CHAINE_UNIQUE"). Doit être absolument unique à travers toute la table `utilisateur`. L'administrateur le voit, mais il n'est généralement pas le critère de recherche principal pour lui.
                    *   **Affichage :** Texte brut. Peut être cliquable pour ouvrir la vue détaillée de cet utilisateur spécifique.
                *   **`login_utilisateur` (Source : `utilisateur.login_utilisateur`, VARCHAR(100), UNIQUE)**
                    *   **Description :** L'identifiant que l'utilisateur saisit pour se connecter. Doit être unique.
                    *   **Affichage :** Texte brut. Souvent une colonne par laquelle l'admin trie ou recherche.
                *   **`email_principal` (Source : `utilisateur.email_principal`, VARCHAR(255), UNIQUE)**
                    *   **Description :** L'adresse e-mail principale associée au compte, utilisée pour la récupération de mot de passe, les notifications système critiques, et potentiellement pour la connexion si le système est configuré ainsi (ou si `login_utilisateur` *est* l'email).
                    *   **Affichage :** Texte brut, peut être un lien `mailto:`.
                *   **`libelle_type_utilisateur` (Source : `type_utilisateur.libelle_type_utilisateur` via `utilisateur.id_type_utilisateur`)**
                    *   **Description :** Le rôle principal de l'utilisateur (ex: "Étudiant", "Personnel Administratif", "Enseignant", "Administrateur Système"). Ceci aide à contextualiser rapidement le compte.
                    *   **Affichage :** Texte brut (ex: "Étudiant").
                *   **`libelle_groupe_utilisateur` (Source : `groupe_utilisateur.libelle_groupe_utilisateur` via `utilisateur.id_groupe_utilisateur`)**
                    *   **Description :** Le groupe de permissions principal auquel l'utilisateur appartient. Détermine en grande partie ses droits. (Ex: "GRP_ETUDIANT_M2_INFO", "GRP_AGENT_CONFORMITE_SCOL", "GRP_COMMISSION_VALIDATION").
                    *   **Affichage :** Texte brut.
                *   **`statut_compte` (Source : `utilisateur.statut_compte`, ENUM)**
                    *   **Description :** L'état actuel du compte utilisateur, déterminant sa capacité à se connecter et interagir.
                        *   `'actif'` : Compte pleinement opérationnel.
                        *   `'inactif'` : Compte temporairement ou définitivement désactivé par un administrateur (ex: étudiant ayant quitté l'établissement, employé parti). Ne peut plus se connecter.
                        *   `'bloque'` : Compte verrouillé suite à trop de tentatives de connexion erronées (`utilisateur.tentatives_connexion_echouees` a dépassé un seuil) ou bloqué manuellement par un admin. La colonne `utilisateur.compte_bloque_jusqua` peut indiquer une date de déblocage automatique.
                        *   `'en_attente_validation'` : Nouveau compte créé mais nécessitant une action pour devenir actif (ex: validation de `email_principal` via un lien envoyé par email, lié à `utilisateur.token_validation_email` et `utilisateur.email_valide`).
                        *   `'archive'` : Compte conservé pour des raisons d'historique mais non destiné à être réactivé facilement. Accès typiquement très restreint, données en lecture seule.
                    *   **Affichage :** Texte brut, potentiellement avec un codage couleur (ex: actif en vert, bloqué en rouge, inactif en gris) pour une identification visuelle rapide.
                *   **`date_creation` (Source : `utilisateur.date_creation`, DATETIME)**
                    *   **Description :** Date et heure exactes de la création de l'enregistrement dans la table `utilisateur`. Utile pour le suivi et les audits.
                    *   **Affichage :** Format de date lisible (ex: "jj/mm/aaaa HH:MM").
                *   **`derniere_connexion` (Source : `utilisateur.derniere_connexion`, DATETIME, NULLABLE)**
                    *   **Description :** Date et heure de la dernière connexion réussie de l'utilisateur. NULL si l'utilisateur ne s'est jamais connecté. Utile pour identifier les comptes inactifs ou dormants.
                    *   **Affichage :** Format de date lisible, ou "Jamais connecté".
                *   **Colonne "Actions" (Contextuelles par ligne) :**
                    *   **Contenu :** Une série de petits boutons ou d'icônes cliquables.
                    *   **Action "Voir Détails" :**
                        *   **Comportement :** Redirige l'administrateur vers la vue détaillée du profil de l'utilisateur, en fonction de son `id_type_utilisateur`. Par exemple, si l'utilisateur est de type 'TYPE_ETUD', il sera redirigé vers l'interface de la Section B.1 (Gestion des Étudiants) avec le `numero_carte_etudiant` ou `numero_utilisateur` pré-sélectionné.
                        *   **Passage de Paramètre :** Le `numero_utilisateur` (ou le `numero_carte_etudiant` / `numero_personnel_administratif` / `numero_enseignant` si on préfère pointer vers le profil métier directement) est passé en paramètre de l'URL.
                    *   **Action "Modifier Compte Utilisateur" :**
                        *   **Comportement :** Ouvre une modale ou une page de formulaire pré-remplie avec les données de l'enregistrement `utilisateur` sélectionné. Permet de modifier des champs comme `login_utilisateur`, `email_principal`, `id_groupe_utilisateur`, `id_niveau_acces_donne`, `statut_compte`, et d'accéder aux fonctions de réinitialisation de mot de passe, de gestion 2FA, ou de validation d'email. (Logique de la section B.x.5, mais directement sur `utilisateur`).
                    *   **Action "Changer Statut Compte" :**
                        *   **Comportement :** Pourrait être un sous-menu déroulant ou une série de petits boutons permettant de changer rapidement le `statut_compte` (ex: "Activer", "Désactiver", "Bloquer", "Débloquer", "Archiver"). Chaque action demande une confirmation.
                        *   **Logique PHP :** `UPDATE utilisateur SET statut_compte = '...', compte_bloque_jusqua = NULL, tentatives_connexion_echouees = 0 WHERE numero_utilisateur = ?;`. Journalisation détaillée dans `enregistrer`.
                    *   **Autres actions potentielles :** "Réinitialiser Mot de Passe", "Envoyer Notification".
            *   **Pagination du Tableau :**
                *   **Nécessité :** Absolument indispensable pour les systèmes avec plus de quelques dizaines d'utilisateurs pour éviter de charger des milliers de lignes à la fois, ce qui impacterait gravement les performances du navigateur et du serveur.
                *   **Fonctionnement :** L'administrateur peut sélectionner le nombre d'entrées à afficher par page (ex: 20, 50, 100, 200). Des contrôles de navigation (Précédent, Suivant, numéros de page, Premier, Dernier) permettent de parcourir les différentes pages de résultats.
                *   **Implémentation :** Les requêtes SQL utilisent les clauses `LIMIT [nombre_par_page]` et `OFFSET [ (numero_page_actuelle - 1) * nombre_par_page ]`. Le nombre total d'utilisateurs (résultat d'un `SELECT COUNT(*)` avec les mêmes filtres) est nécessaire pour calculer le nombre total de pages.
            *   **Tri des Colonnes :**
                *   **Fonctionnement :** Chaque en-tête de colonne cliquable (celles qui sont pertinentes pour le tri) permet de trier les données du tableau par cette colonne, en ordre ascendant ou descendant (un deuxième clic inverse l'ordre). Un indicateur visuel (petite flèche haut/bas) montre la colonne de tri active et l'ordre.
                *   **Implémentation :** La logique PHP côté serveur modifie la clause `ORDER BY` de la requête SQL principale en fonction de la colonne et de l'ordre de tri demandés par l'utilisateur (passés en paramètres GET). Ex: `ORDER BY login_utilisateur ASC`.

        *   **B.0.2. Zone de Moteur de Recherche Globale d'Utilisateurs :**
            *   **Objectif :** Permettre à l'administrateur de localiser rapidement un ou plusieurs utilisateurs spécifiques sans avoir à parcourir toutes les pages ou à appliquer des filtres complexes initialement.
            *   **Interface :** Typiquement un champ de saisie unique ou plusieurs champs dédiés en haut de la liste des utilisateurs.
            *   **Champs de Recherche et Logique Associée :**
                *   **Recherche par `numero_utilisateur` :**
                    *   **Interface :** Champ "Numéro Utilisateur".
                    *   **Logique :** Correspondance exacte. `WHERE u.numero_utilisateur = '[valeur_saisie]'`.
                *   **Recherche par `login_utilisateur` :**
                    *   **Interface :** Champ "Login".
                    *   **Logique :** Option de correspondance exacte (`WHERE u.login_utilisateur = '[valeur_saisie]'`) ou partielle ("contient", `WHERE u.login_utilisateur LIKE '%[valeur_saisie]%'`). La recherche partielle est plus flexible mais moins performante.
                *   **Recherche par `email_principal` :**
                    *   **Interface :** Champ "Email Principal".
                    *   **Logique :** Option de correspondance exacte ou partielle (comme pour le login).
                *   **Recherche par Nom et/ou Prénom (transverse aux types de profils) :**
                    *   **Interface :** Champs "Nom", "Prénom".
                    *   **Complexité :** Cette recherche est plus complexe car les noms/prénoms sont stockés dans les tables spécifiques (`etudiant`, `personnel_administratif`, `enseignant`).
                    *   **Algorithme Potentiel Côté Serveur :**
                        1.  Récupérer le terme de recherche pour le nom et/ou le prénom.
                        2.  Effectuer des requêtes `SELECT numero_utilisateur FROM etudiant WHERE nom LIKE '%[terme_nom]%' AND prenom LIKE '%[terme_prenom]%';` (idem pour `personnel_administratif` et `enseignant`).
                        3.  Collecter tous les `numero_utilisateur` distincts trouvés.
                        4.  Utiliser ces `numero_utilisateur` dans la clause `WHERE` de la requête principale sur la table `utilisateur` (ex: `WHERE u.numero_utilisateur IN ('id1', 'id2', ...)`).
                    *   **Performance :** Peut être lent si pas d'indexation appropriée sur les colonnes `nom` et `prenom` des tables de profil. Une solution full-text (si SGBD le supporte) ou une dénormalisation du nom complet dans la table `utilisateur` (avec les problèmes de synchronisation que cela implique) pourrait être envisagée pour des performances optimales sur de très gros volumes.
            *   **Activation de la Recherche :** Un bouton "Rechercher" ou une recherche dynamique qui s'active après un court délai de frappe (debounce).
            *   **Affichage des Résultats :** Le tableau principal (B.0.1) est actualisé pour n'afficher que les utilisateurs correspondant aux critères de recherche. Un message "X utilisateur(s) trouvé(s)" s'affiche. Un bouton "Réinitialiser la recherche/Filtres" doit être présent.

        *   **B.0.3. Panneau de Filtres Avancés :**
            *   **Objectif :** Permettre d'affiner la liste des utilisateurs affichée en combinant plusieurs critères. Souvent présenté comme un formulaire repliable ou une section latérale.
            *   **Critères de Filtrage et Interface :**
                *   **Filtrer par Type d'Utilisateur (`id_type_utilisateur`) :**
                    *   **Interface :** Liste déroulante ( `<select>`) peuplée dynamiquement avec les `id_type_utilisateur` (valeur) et `libelle_type_utilisateur` (texte affiché) de la table `type_utilisateur`. Option "Tous les types".
                    *   **Logique SQL :** Ajout d'une condition `AND u.id_type_utilisateur = '[ID_TYPE_SELECTIONNE]'` à la requête principale.
                *   **Filtrer par Groupe d'Utilisateurs (`id_groupe_utilisateur`) :**
                    *   **Interface :** Liste déroulante peuplée avec les `id_groupe_utilisateur` et `libelle_groupe_utilisateur` de la table `groupe_utilisateur`. Option "Tous les groupes".
                    *   **Logique SQL :** `AND u.id_groupe_utilisateur = '[ID_GROUPE_SELECTIONNE]'`.
                *   **Filtrer par Statut du Compte (`statut_compte`) :**
                    *   **Interface :** Liste déroulante avec les valeurs de l'ENUM `statut_compte` (actif, inactif, bloque, etc.). Option "Tous les statuts".
                    *   **Logique SQL :** `AND u.statut_compte = '[STATUT_SELECTIONNE]'`.
                *   **Filtrer par État de Validation de l'Email (`email_valide`) :**
                    *   **Interface :** Cases d'option ou liste déroulante : "Validé", "Non Validé", "Tous".
                    *   **Logique SQL :** `AND u.email_valide = 1` ou `AND u.email_valide = 0`.
                *   **Filtrer par Activation 2FA (`preferences_2fa_active`) :**
                    *   **Interface :** Cases d'option ou liste déroulante : "2FA Actif", "2FA Inactif", "Tous".
                    *   **Logique SQL :** `AND u.preferences_2fa_active = 1` ou `AND u.preferences_2fa_active = 0`.
                *   **Filtrer par Période de Création du Compte (`date_creation`) :**
                    *   **Interface :** Deux champs de sélection de date (calendrier) pour "Date de création Du" et "Au".
                    *   **Logique SQL :** `AND u.date_creation BETWEEN '[DATE_DEBUT_SAISIE]' AND '[DATE_FIN_SAISIE]'`.
                *   **Filtrer par Période de Dernière Connexion (`derniere_connexion`) :**
                    *   **Interface :** Deux champs de sélection de date pour "Dernière connexion Du" et "Au". Option pour "Jamais connecté".
                    *   **Logique SQL :** `AND u.derniere_connexion BETWEEN '[DATE_DEBUT_SAISIE]' AND '[DATE_FIN_SAISIE]'` ou `AND u.derniere_connexion IS NULL`.
            *   **Application des Filtres :** Un bouton "Appliquer les Filtres" actualise le tableau B.0.1. Un bouton "Effacer les Filtres" réinitialise tous les champs de filtrage.

        *   **B.0.4. Actions Transversales sur Sélection Multiple d'Utilisateurs :**
            *   **Objectif :** Permettre à l'administrateur d'effectuer certaines opérations sur un lot d'utilisateurs sélectionnés, pour gagner en efficacité.
            *   **Interface de Sélection :** Chaque ligne du tableau (B.0.1) comporte une case à cocher. Une case à cocher "Tout sélectionner" est présente dans l'en-tête du tableau. Une fois des utilisateurs sélectionnés, les boutons d'actions de masse deviennent actifs.
            *   **B.0.4.1. Changement de Statut en Masse :**
                *   **Interface :** Bouton "Changer Statut des Sélectionnés" ouvrant une modale ou une liste déroulante des statuts cibles (`utilisateur.statut_compte`).
                *   **Workflow :**
                    1.  Admin sélectionne les utilisateurs.
                    2.  Admin choisit le nouveau statut.
                    3.  Fenêtre de confirmation récapitulant le nombre d'utilisateurs affectés et le changement de statut. "Êtes-vous sûr de vouloir passer [X] utilisateurs au statut '[Nouveau Statut]' ?"
                    4.  Sur confirmation, logique PHP effectue un `UPDATE utilisateur SET statut_compte = '[Nouveau Statut]' WHERE numero_utilisateur IN ('id1', 'id2', ...);`.
                    5.  Chaque changement individuel est logué dans `enregistrer` ou une entrée de log unique avec la liste des `numero_utilisateur` affectés dans `details_action`.
                    6.  Actualisation du tableau.
                *   **Précautions :** Certaines transitions de statut peuvent avoir des implications (ex: passer un admin système à 'inactif' pourrait être dangereux s'il est le seul). Des validations peuvent être nécessaires.
            *   **B.0.4.2. Envoi de Notifications en Masse :**
                *   **Interface :** Bouton "Envoyer Notification aux Sélectionnés". Ouvre une modale avec :
                    *   Soit une liste déroulante pour sélectionner un `id_message` prédéfini depuis la table `message` (templates).
                    *   Soit des champs pour rédiger un `sujet_message` et un `libelle_message` ad-hoc.
                *   **Workflow :**
                    1.  Admin sélectionne les utilisateurs et le message/template.
                    2.  Fenêtre de confirmation.
                    3.  Sur confirmation, logique PHP crée une entrée dans `recevoir` pour chaque `numero_utilisateur` sélectionné (avec l'`id_notification` correspondant au type de message), et si c'est un email, l'ajoute à une file d'attente d'envoi ou l'envoie directement via le `ServiceEmail`.
                    4.  Action d'envoi de masse loguée dans `enregistrer`.
            *   **B.0.4.3. Réinitialisation de Mot de Passe en Masse (HAUTEMENT SENSIBLE) :**
                *   **Utilisation :** Cas très rares, ex: suspicion de compromission de plusieurs comptes, ou import initial où les mots de passe doivent être définis par l'utilisateur via un lien.
                *   **Interface :** Bouton "Réinitialiser MDP (Sélection)". Requiert confirmation très explicite, voire double authentification de l'admin.
                *   **Workflow :**
                    1.  Pour chaque utilisateur sélectionné : génération d'un `token_reset_mdp` unique, mise à jour `date_expiration_token_reset` dans `utilisateur`.
                    2.  Envoi d'un email (utilisant un template de `message` spécifique pour la réinitialisation) à chaque `utilisateur.email_principal` avec le lien contenant le token.
                    3.  Peut forcer `statut_compte` à 'en_attente_validation' si nécessaire.
                    4.  Action très détaillée dans `enregistrer`.
            *   **B.0.4.4. Gestion des Tokens Actifs (Évolution, si applicable) :**
                *   Si le système utilise des tokens de session JWT ou des tokens d'API stockés : une action pour invalider/révoquer les tokens des utilisateurs sélectionnés. Nécessite une table de gestion de tokens ou une "blacklist" de tokens révoqués.

        *   **B.0.5. Section Résumé : Vue d'Ensemble des Types et Groupes d'Utilisateurs :**
            *   **Objectif :** Fournir un rappel rapide de la composition des rôles et groupes, complémentaire aux statistiques du tableau de bord principal (A.1.1).
            *   **Affichage :** Deux petits tableaux ou listes :
                *   **Par Type d'Utilisateur :**
                    *   Colonnes : `libelle_type_utilisateur` (de `type_utilisateur`), "Nombre d'Utilisateurs Associés" (`COUNT`).
                    *   SQL : `SELECT tu.libelle_type_utilisateur, COUNT(u.numero_utilisateur) AS count_users FROM type_utilisateur tu LEFT JOIN utilisateur u ON tu.id_type_utilisateur = u.id_type_utilisateur GROUP BY tu.id_type_utilisateur, tu.libelle_type_utilisateur ORDER BY tu.libelle_type_utilisateur;`
                *   **Par Groupe d'Utilisateurs :**
                    *   Colonnes : `libelle_groupe_utilisateur` (de `groupe_utilisateur`), "Nombre d'Utilisateurs Associés" (`COUNT`).
                    *   SQL : `SELECT gu.libelle_groupe_utilisateur, COUNT(u.numero_utilisateur) AS count_users FROM groupe_utilisateur gu LEFT JOIN utilisateur u ON gu.id_groupe_utilisateur = u.id_groupe_utilisateur GROUP BY gu.id_groupe_utilisateur, gu.libelle_groupe_utilisateur ORDER BY gu.libelle_groupe_utilisateur;`
            *   **Interaction :** Cliquer sur un type ou un groupe pourrait filtrer le tableau principal B.0.1 par ce critère.

    *   **Tables SQL Primordialement Impliquées pour l'onglet B.0 :**
        *   **`utilisateur` :** C'est la table centrale pour toutes les opérations de cet onglet. Presque tous ses champs sont utilisés pour l'affichage, le filtrage, ou les mises à jour.
        *   **`type_utilisateur` :** Jointure via `utilisateur.id_type_utilisateur` pour afficher le `libelle_type_utilisateur` et permettre le filtrage.
        *   **`groupe_utilisateur` :** Jointure via `utilisateur.id_groupe_utilisateur` pour afficher le `libelle_groupe_utilisateur` et permettre le filtrage.
        *   **`etudiant`, `personnel_administratif`, `enseignant` :** Utilisées principalement pour la fonctionnalité de "Recherche par Nom/Prénom" (B.0.2) via des jointures basées sur `numero_utilisateur`.
        *   **`enregistrer` :** Absolument essentielle pour enregistrer chaque action administrative effectuée depuis cet onglet (changement de statut, envoi de notification, etc.), avec `numero_utilisateur` de l'admin, l'`id_action` pertinente, `date_action`, et dans `details_action` (JSON), les `numero_utilisateur` cibles pour les actions de masse.
        *   **`message` :** Consultée pour les templates lors de l'envoi de notifications en masse.
        *   **`recevoir` :** `INSERT` de nouveaux enregistrements lors de l'envoi de notifications en masse.

    *   **Workflow Typique et Algorithmes Implicites pour l'Administrateur dans cet Onglet (B.0) :**
        1.  **Chargement Initial de la Page :**
            *   PHP récupère les paramètres de pagination (page actuelle, nombre par page, colonne de tri, ordre de tri) depuis la requête GET (ou des valeurs par défaut).
            *   PHP construit la requête SQL de base (jointures `utilisateur`, `type_utilisateur`, `groupe_utilisateur`) avec les clauses `ORDER BY` et `LIMIT`/`OFFSET`.
            *   Exécution de la requête pour obtenir les données de la page actuelle.
            *   Exécution d'une requête `COUNT(*)` avec les mêmes filtres (sans `LIMIT`/`OFFSET`) pour la pagination.
            *   PHP envoie les données et les informations de pagination à la vue (template PHP, ex: `Administration/Utilisateurs/liste_tous_utilisateurs.php` si créée, ou logique dans `UtilisateurController` et vue associée).
        2.  **Interaction (Tri/Pagination/Filtre/Recherche) :**
            *   L'utilisateur clique sur un en-tête de colonne, un numéro de page, ou soumet un formulaire de filtre/recherche.
            *   JavaScript peut intercepter cela et recharger la page avec de nouveaux paramètres GET, ou effectuer une requête AJAX.
            *   Le serveur PHP reçoit les nouveaux paramètres, reconstruit la requête SQL, et renvoie les données mises à jour.
        3.  **Actions sur un Utilisateur Unique (depuis la ligne du tableau) :**
            *   Clic sur "Modifier Compte Utilisateur" -> La logique PHP charge le `numero_utilisateur` spécifié, récupère ses données depuis `utilisateur`, et pré-remplit un formulaire de modification. À la soumission de ce formulaire, validation, `UPDATE utilisateur`, et `INSERT` dans `enregistrer`.
        4.  **Actions de Masse :**
            *   Admin coche des cases -> JavaScript stocke les `numero_utilisateur` sélectionnés.
            *   Admin clique sur "Changer Statut des Sélectionnés" -> JavaScript envoie la liste des `numero_utilisateur` et le nouveau statut cible au serveur (POST).
            *   PHP valide que l'admin a le droit de faire cette action, puis boucle sur les IDs : `UPDATE utilisateur ... WHERE numero_utilisateur = ?;` pour chaque ID (ou un seul `UPDATE ... WHERE numero_utilisateur IN (...)`). `INSERT` dans `enregistrer`.
            *   Réponse au client pour actualiser la vue.

    *   **Considérations Spécifiques et Avancées pour B.0 :**
        *   **Performance et Indexation :** Avec une potentielle recherche sur Nom/Prénom combinée à des filtres sur `type_utilisateur`, `groupe_utilisateur`, `statut_compte`, les requêtes peuvent devenir très complexes. Il faut :
            *   Des index composites sur `utilisateur` (ex: sur `(id_type_utilisateur, statut_compte)`, `(id_groupe_utilisateur, statut_compte)`).
            *   Index sur `etudiant(nom, prenom)`, `personnel_administratif(nom, prenom)`, `enseignant(nom, prenom)`.
            *   Analyse des requêtes via `EXPLAIN` pour identifier les goulots d'étranglement.
        *   **Sécurité des Actions de Masse :** Outre la confirmation, envisager un "audit log" interne spécifique avant l'application réelle pour certaines actions, ou un système de "panier" pour les modifications de masse qui doivent être validées en une fois.
        *   **Stratégie de Génération des IDs VARCHAR :**
            *   **Application PHP :** C'est elle qui doit s'assurer que les `id_type_utilisateur`, `id_groupe_utilisateur`, `id_niveau_acces_donne`, `numero_utilisateur` sont non seulement uniques mais suivent aussi une convention (ex: "TYPE_XXX", "GRP_YYY", "LVL_ZZZ", "USR_AAA_timestamp_random").
            *   **Pour l'admin :** Quand l'admin crée un nouveau type/groupe/niveau via l'interface, la logique PHP pourrait proposer un ID généré (modifiable par l'admin sous condition d'unicité) ou l'admin pourrait le saisir, mais la validation d'unicité est impérative avant `INSERT`.
        *   **Expérience Utilisateur de l'Admin :** La page doit être réactive. Les recherches et filtres ne doivent pas geler le navigateur. Utilisation d'indicateurs de chargement ("spinner") pour les opérations longues.

Cet onglet "Utilisateurs (Vue Générale et Actions Transversales)" est donc un outil puissant de supervision et d'intervention initiale, agissant comme une console centrale avant de plonger dans les détails de gestion propres à chaque type de profil utilisateur. Sa conception doit allier richesse fonctionnelle, performance et sécurité.

---
**(Nous avons maintenant détaillé la section B.0. Nous pouvons passer à B.1. Étudiants ou une autre section si vous préférez.)**


Parfait. Nous allons donc reprendre et re-détailler de manière exhaustive la section **B.1. Onglet / Section : Étudiants**, en tenant compte de toutes les modifications de schéma et des clarifications sur les workflows.

---

**B.1. Onglet / Section : Étudiants (gestion spécifique via `etudiant`, `utilisateur`, et tables académiques associées)**

Accessible via la sidebar (Menu "Utilisateurs" -> Sous-item "Étudiants"), cette section est l'interface privilégiée de l'administrateur système (ou du Responsable Scolarité dûment habilité) pour toutes les opérations CRUD (Créer, Lire, Mettre à Jour, Désactiver/Archiver) concernant spécifiquement les profils et les comptes des étudiants. La gestion méticuleuse des données étudiantes est fondamentale, car elles constituent la base du processus de soutenance, liant les aspects administratifs (identité, inscription) aux aspects académiques (soumission de rapports, notes, réclamations). Chaque action administrative significative est auditée dans la table `enregistrer`.

*   **Objectif Stratégique et Opérationnel :**
    *   **Stratégique :** Assurer la gestion complète et intègre du cycle de vie des étudiants au sein de la plateforme "GestionMySoutenance", de l'import initial ou de la création manuelle jusqu'à l'archivage post-diplomation ou départ. Garantir que chaque étudiant dispose d'un compte correctement configuré et lié à son profil académique.
    *   **Opérationnel :** Fournir des outils efficaces pour lister, rechercher, filtrer, créer, modifier et gérer le statut des comptes étudiants. Permettre également la consultation centralisée de leurs informations académiques associées (inscriptions, rapports, etc.) depuis une interface administrative.

*   **Contenu et Fonctionnalités Détaillées de l'Interface :**
    L'interface est généralement construite autour d'une liste principale d'étudiants, avec des outils de recherche, de filtrage, et des actions contextuelles.

    *   **B.1.1. Listage des Étudiants :**
        *   **Description de l'Affichage :** Le composant central est un tableau de données complet, paginé et avec des options de tri avancées, présentant l'ensemble des étudiants dont le profil existe dans la table `etudiant` et dont le compte est enregistré dans `utilisateur`. Chaque ligne est unique par `etudiant.numero_carte_etudiant`.
        *   **SQL Requête de Base (Exemple pour illustrer les jointures et données) :**
            ```sql
            SELECT
                e.numero_carte_etudiant,
                e.nom AS nom_etudiant,
                e.prenom AS prenom_etudiant,
                u.numero_utilisateur,
                u.login_utilisateur,
                u.email_principal,
                u.statut_compte,
                (SELECT aa.libelle_annee_academique FROM annee_academique aa JOIN inscrire i ON aa.id_annee_academique = i.id_annee_academique WHERE i.numero_carte_etudiant = e.numero_carte_etudiant ORDER BY aa.date_debut DESC LIMIT 1) AS derniere_annee_inscription, -- Simplification, peut nécessiter une logique plus complexe si plusieurs inscriptions par an.
                (SELECT ne.libelle_niveau_etude FROM niveau_etude ne JOIN inscrire i ON ne.id_niveau_etude = i.id_niveau_etude WHERE i.numero_carte_etudiant = e.numero_carte_etudiant ORDER BY i.date_inscription DESC LIMIT 1) AS dernier_niveau_inscrit,
                u.date_creation AS date_creation_compte
            FROM
                etudiant e
            JOIN
                utilisateur u ON e.numero_utilisateur = u.numero_utilisateur
            --potentiels filtres et clauses ORDER BY ici--
            LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
            ```
        *   **Détail des Colonnes Essentielles du Tableau :**
            *   **`numero_carte_etudiant` (Source : `etudiant.numero_carte_etudiant`, VARCHAR(50), PK)**
                *   **Description :** L'identifiant administratif principal de l'étudiant, souvent son numéro de carte physique. C'est la clé pour retrouver toutes ses informations spécifiques de profil étudiant. Il est saisi ou importé.
                *   **Affichage :** Texte brut, cliquable pour "Voir Profil Complet".
            *   **`nom_etudiant` (Source : `etudiant.nom`, VARCHAR(100))**
                *   **Description :** Nom de famille.
                *   **Affichage :** Texte brut.
            *   **`prenom_etudiant` (Source : `etudiant.prenom`, VARCHAR(100))**
                *   **Description :** Prénom(s).
                *   **Affichage :** Texte brut.
            *   **`numero_utilisateur` (Source : `etudiant.numero_utilisateur` via `utilisateur.numero_utilisateur`)**
                *   **Description :** L'identifiant interne du compte `utilisateur` associé. Utile pour les liaisons techniques et l'audit.
                *   **Affichage :** Texte brut.
            *   **`login_utilisateur` (Source : `utilisateur.login_utilisateur`)**
                *   **Description :** Identifiant de connexion de l'étudiant.
                *   **Affichage :** Texte brut.
            *   **`email_principal` (Source : `utilisateur.email_principal`)**
                *   **Description :** Email utilisé pour la connexion et les communications critiques.
                *   **Affichage :** Texte brut, cliquable (mailto:).
            *   **`statut_compte` (Source : `utilisateur.statut_compte`)**
                *   **Description :** État du compte utilisateur (actif, inactif, bloqué, en_attente_validation, archive, ou potentiellement 'SUSPENDU_ATTENTE_VALID_RS_STAGE' comme discuté pour les reprises de processus).
                *   **Affichage :** Texte avec codage couleur (ex: Actif en vert, Bloqué en rouge).
            *   **"Dernière Année d'Inscription" (Calculée/Jointe)**
                *   **Description :** Affiche le `libelle_annee_academique` de la dernière inscription trouvée pour l'étudiant, généralement l'année académique active s'il est inscrit, ou la dernière année historique.
                *   **Affichage :** Texte (ex: "2023-2024").
            *   **"Dernier Niveau Inscrit" (Calculée/Jointe)**
                *   **Description :** Affiche le `libelle_niveau_etude` de la dernière inscription.
                *   **Affichage :** Texte (ex: "Master 2 Informatique").
            *   **`date_creation_compte` (Source : `utilisateur.date_creation`)**
                *   **Description :** Date de création du compte utilisateur.
                *   **Affichage :** Date et heure.
            *   **Colonne "Actions" Contextuelles par Ligne :**
                *   **"Voir Profil Complet" :** Lien vers la vue B.1.4 (détaillée plus bas). Passe `numero_carte_etudiant` ou `numero_utilisateur` en paramètre.
                *   **"Modifier Profil Étudiant" :** Ouvre le formulaire (B.1.5) pour modifier les données de la table `etudiant` (informations personnelles, contact d'urgence, etc.).
                *   **"Modifier Compte Utilisateur" :** Ouvre le formulaire (B.1.5) pour modifier les données de la table `utilisateur` (login, email principal, statut, mot de passe, photo, groupe, niveau d'accès).
                *   **"Gérer Inscriptions" :** Lien vers l'interface B.1.7 pour gérer les inscriptions de cet étudiant (`inscrire`).
                *   **"Voir Rapports Soumis" :** Lien vers une vue filtrée des `rapport_etudiant` pour cet étudiant.
                *   **"Désactiver/Archiver Compte" :** Action directe pour changer `utilisateur.statut_compte` (avec confirmation).
        *   **Pagination :** Comme décrit en B.0.1 (ex: 20, 50, 100 étudiants par page), avec contrôles de navigation. La requête de comptage total (`SELECT COUNT(*) FROM etudiant JOIN utilisateur ...`) doit appliquer les mêmes filtres que la requête de listage.
        *   **Tri des Colonnes :** L'admin doit pouvoir trier par `numero_carte_etudiant`, `nom_etudiant`, `prenom_etudiant`, `login_utilisateur`, `statut_compte`, `date_creation_compte`, "Dernière Année d'Inscription" (si la requête le permet efficacement).

    *   **B.1.2. Moteur de Filtrage et de Recherche Avancée pour les Étudiants :**
        *   **Objectif :** Localiser rapidement des étudiants ou des groupes d'étudiants selon des critères précis.
        *   **Interface :** Un formulaire dédié, souvent repliable ou dans une section distincte, au-dessus du tableau de listage.
        *   **Champs de Recherche Directe (Saisie Libre) :**
            *   **Par `numero_carte_etudiant` :** Recherche exacte.
                *   Clause SQL : `AND e.numero_carte_etudiant = '[valeur]'`
            *   **Par `nom` et/ou `prenom` de l'étudiant :** Options "Commence par", "Contient", "Correspondance exacte".
                *   Clause SQL : `AND e.nom LIKE '[valeur]%'` ou `AND e.nom LIKE '%[valeur]%'` ou `AND e.nom = '[valeur]'`. Idem pour `prenom`.
            *   **Par `numero_utilisateur` (compte associé) :** Recherche exacte.
                *   Clause SQL : `AND u.numero_utilisateur = '[valeur]'`
            *   **Par `login_utilisateur` (compte associé) :** Exacte ou partielle.
                *   Clause SQL : `AND u.login_utilisateur LIKE '%[valeur]%'`
            *   **Par `email_principal` (compte associé) :** Exacte ou partielle.
                *   Clause SQL : `AND u.email_principal LIKE '%[valeur]%'`
            *   **Par `email_contact_secondaire` (profil étudiant) :** Exacte ou partielle.
                *   Clause SQL : `AND e.email_contact_secondaire LIKE '%[valeur]%'`
        *   **Filtres Combinables (Listes Déroulantes, Sélecteurs de Date, Cases à Cocher) :**
            *   **Par Statut du Compte Utilisateur (`utilisateur.statut_compte`) :**
                *   Interface : Liste déroulante : "Tous les statuts", "Actif", "Inactif", "Bloqué", "En attente de validation", "Archivé", "Suspendu (attente RS Stage)".
                *   Clause SQL : `AND u.statut_compte = '[valeur_enum_selectionnee]'`
            *   **Par Niveau d'Étude Actuel (`inscrire.id_niveau_etude` pour l'année active) :**
                *   Interface : Liste déroulante des `libelle_niveau_etude` (depuis `niveau_etude`). Nécessite une sous-requête ou une jointure complexe pour identifier le niveau de l'inscription "active" ou la plus récente.
                *   Clause SQL : `AND i.id_niveau_etude = '[ID_NIVEAU_SELECTIONNE]' AND aa.est_active = 1` (simplifié).
            *   **Par Année Académique d'Inscription (`inscrire.id_annee_academique`) :**
                *   Interface : Liste déroulante des `libelle_annee_academique` (depuis `annee_academique`).
                *   Clause SQL : `AND i.id_annee_academique = '[ID_ANNEE_SELECTIONNEE]'`.
            *   **Par Groupe d'Utilisateur Étudiant (`utilisateur.id_groupe_utilisateur`) :**
                *   Interface : Liste déroulante des `libelle_groupe_utilisateur` qui sont pertinents pour les étudiants (ex: 'GRP_ETUDIANT', 'GRP_ETUD_M1_INFO', 'GRP_ETUD_M2_DROIT').
                *   Clause SQL : `AND u.id_groupe_utilisateur = '[ID_GROUPE_SELECTIONNE]'`.
            *   **Par Statut de Paiement Scolarité (`inscrire.id_statut_paiement` pour l'année active) :**
                *   Interface : Liste déroulante des `libelle_statut_paiement` (depuis `statut_paiement_ref`).
                *   Clause SQL : `AND i.id_statut_paiement = '[ID_STATUT_PAIE_SELECTIONNE]' AND aa.est_active = 1`.
            *   **Par Statut de Rapport Soumis (`rapport_etudiant.id_statut_rapport` pour l'année active) :**
                *   Interface : Liste déroulante des `libelle_statut_rapport` (depuis `statut_rapport_ref`). Option "Aucun rapport soumis".
                *   Clause SQL : `AND r.id_statut_rapport = '[ID_STATUT_RAP_SELECTIONNE]' AND ... (condition sur l'année du rapport)` ou pour "Aucun rapport soumis", une sous-requête `NOT EXISTS (SELECT 1 FROM rapport_etudiant r ...)`
            *   **Par Existence de Stage Enregistré (`faire_stage` pour l'année académique pertinente) :**
                *   Interface : Cases à cocher "Stage Enregistré : Oui / Non / Indifférent".
                *   Clause SQL : Jointure avec `faire_stage` et condition sur l'existence, ou `EXISTS`/`NOT EXISTS`.
        *   **Application des Filtres/Recherche :**
            *   Bouton "Appliquer" / "Rechercher". La page (ou le tableau) se recharge/s'actualise pour afficher les résultats filtrés.
            *   Bouton "Réinitialiser" pour effacer tous les critères de recherche et de filtre.
        *   **Combinaison des Critères :** Tous les critères de recherche et de filtre sélectionnés sont combinés avec un opérateur `AND` dans la clause `WHERE` de la requête SQL.

    *   **(La suite de B.1.3 à B.1.7 sera détaillée dans le message suivant pour ne pas dépasser la limite de tokens par réponse tout en maintenant l'extrême détail.)**

Cette première partie de B.1 met l'accent sur la capacité de l'administrateur à visualiser, parcourir et localiser précisément les profils étudiants, ce qui est fondamental avant d'entreprendre des actions de création ou de modification. La qualité des filtres et la performance des recherches sont clés pour l'ergonomie de cette section.


Parfait, continuons avec la suite de la section **B.1. Onglet / Section : Étudiants**, en gardant ce niveau de détail extrême.

---

*   **B.1.3. Création d'un Nouvel Étudiant (Workflow Détaillé) :**
    *   **Déclenchement :** Un bouton proéminent "Créer Nouvel Étudiant" (ou "Ajouter un Étudiant") est disponible dans l'interface de listage B.1.1, généralement en haut du tableau. Cliquer sur ce bouton mène à un formulaire dédié, souvent sur une nouvelle page ou dans une modale pleine page.
    *   **Interface du Formulaire de Création :** Le formulaire est structuré en sections logiques, généralement "Informations Personnelles (Profil Étudiant)" et "Informations du Compte Utilisateur". Tous les champs obligatoires sont clairement indiqués (ex: avec un astérisque `*`). Des aides contextuelles (tooltips) peuvent expliquer le format attendu pour certains champs.
    *   **Étape 1 : Formulaire de Saisie des Informations du Profil Étudiant (données pour la table `etudiant`) :**
        *   `numero_carte_etudiant` (VARCHAR(50), PK de `etudiant`) :
            *   **Libellé :** "Numéro de Carte Étudiant" ou "Identifiant Étudiant (INE/Matricule)" \*.
            *   **Saisie :** Champ texte.
            *   **Validation Côté Client (JavaScript) :** Vérification du format (si une règle existe, ex: longueur, caractères autorisés), champ obligatoire.
            *   **Validation Côté Serveur (PHP) :** Vérification d'unicité (`SELECT COUNT(*) FROM etudiant WHERE numero_carte_etudiant = ?`). Si non unique, message d'erreur clair : "Ce numéro de carte étudiant existe déjà."
        *   `nom` (VARCHAR(100)) :
            *   **Libellé :** "Nom de Famille" \*.
            *   **Saisie :** Champ texte.
            *   **Validation :** Obligatoire, longueur max.
        *   `prenom` (VARCHAR(100)) :
            *   **Libellé :** "Prénom(s)" \*.
            *   **Saisie :** Champ texte.
            *   **Validation :** Obligatoire, longueur max.
        *   `date_naissance` (DATE) :
            *   **Libellé :** "Date de Naissance".
            *   **Saisie :** Sélecteur de date (calendrier).
            *   **Validation :** Format de date valide, date plausible (pas dans le futur, pas excessivement ancienne).
        *   `lieu_naissance` (VARCHAR(100)) :
            *   **Libellé :** "Lieu de Naissance".
            *   **Saisie :** Champ texte.
        *   `pays_naissance` (VARCHAR(50)) :
            *   **Libellé :** "Pays de Naissance".
            *   **Saisie :** Liste déroulante (pourrait être un référentiel de pays si une normalisation poussée est souhaitée, sinon champ texte libre).
        *   `nationalite` (VARCHAR(50)) :
            *   **Libellé :** "Nationalité".
            *   **Saisie :** Liste déroulante (idem, référentiel ou champ texte).
        *   `sexe` (ENUM('Masculin','Féminin','Autre')) :
            *   **Libellé :** "Sexe".
            *   **Saisie :** Boutons radio ou liste déroulante.
        *   `adresse_postale` (TEXT) :
            *   **Libellé :** "Adresse Postale".
            *   **Saisie :** Zone de texte multi-lignes.
        *   `ville` (VARCHAR(100)) :
            *   **Libellé :** "Ville".
            *   **Saisie :** Champ texte.
        *   `code_postal` (VARCHAR(20)) :
            *   **Libellé :** "Code Postal".
            *   **Saisie :** Champ texte. Validation de format si possible (spécifique au pays).
        *   `telephone` (VARCHAR(20)) :
            *   **Libellé :** "Téléphone (principal de contact profil étudiant)".
            *   **Saisie :** Champ texte. Validation de format si possible.
        *   `email_contact_secondaire` (VARCHAR(255), NULLABLE) :
            *   **Libellé :** "Email de Contact Secondaire (Optionnel)".
            *   **Saisie :** Champ texte.
            *   **Validation Côté Client/Serveur :** Format email valide. Différent de `utilisateur.email_principal` (si fourni à cette étape).
        *   `contact_urgence_nom` (VARCHAR(100)), `contact_urgence_telephone` (VARCHAR(20)), `contact_urgence_relation` (VARCHAR(50)) :
            *   **Libellé :** "Personne à Contacter en Cas d'Urgence (Nom, Téléphone, Relation)".
            *   **Saisie :** Champs texte respectifs.

    *   **Étape 2 : Formulaire de Saisie des Informations du Compte Utilisateur (données pour la table `utilisateur`) :**
        Cette section peut être affichée sur la même page que les infos profil ou comme une étape suivante.
        *   `login_utilisateur` (VARCHAR(100), UNIQUE dans `utilisateur`) :
            *   **Libellé :** "Identifiant de Connexion (Login)" \*.
            *   **Saisie :** Champ texte. L'application pourrait proposer une valeur par défaut (ex: `prenom.nom` ou basé sur `numero_carte_etudiant`) que l'admin peut modifier.
            *   **Validation Côté Client/Serveur :** Obligatoire, format (ex: alphanumérique, sans espaces), longueur min/max, et surtout **unicité** (`SELECT COUNT(*) FROM utilisateur WHERE login_utilisateur = ?`). Message d'erreur si non unique.
        *   `email_principal` (VARCHAR(255), UNIQUE dans `utilisateur`) :
            *   **Libellé :** "Email Principal (pour connexion/notifications système)" \*.
            *   **Saisie :** Champ texte.
            *   **Validation Côté Client/Serveur :** Obligatoire, format email valide, **unicité** (`SELECT COUNT(*) FROM utilisateur WHERE email_principal = ?`). Message d'erreur si non unique ou format invalide.
        *   **Mot de Passe :**
            *   **Libellé :** "Mot de Passe Initial" \*.
            *   **Options d'Interface :**
                1.  Deux champs "Mot de Passe" et "Confirmer Mot de Passe". Validation JS que les deux correspondent. Indicateur de force du mot de passe.
                2.  Bouton "Générer un Mot de Passe Fort" : PHP génère une chaîne aléatoire et sécurisée, l'affiche à l'admin (avec option "copier").
            *   **Logique :** Le mot de passe ne sera jamais stocké en clair, uniquement son hachage.
            *   **Option :** Case à cocher "Forcer le changement de mot de passe à la première connexion". Si cochée, un flag est stocké (ou le statut initial du compte gère cela).
        *   `id_groupe_utilisateur` (VARCHAR(50), FK vers `groupe_utilisateur`) :
            *   **Libellé :** "Groupe Principal de l'Étudiant" \*.
            *   **Saisie :** Liste déroulante peuplée par `SELECT id_groupe_utilisateur, libelle_groupe_utilisateur FROM groupe_utilisateur WHERE ...` (potentiellement filtré pour les groupes étudiants). La valeur par défaut est l'ID VARCHAR de 'GRP_ETUDIANT'.
            *   **Validation :** Doit être une valeur existante dans `groupe_utilisateur.id_groupe_utilisateur`.
        *   `id_niveau_acces_donne` (VARCHAR(50), FK vers `niveau_acces_donne`) :
            *   **Libellé :** "Niveau d'Accès aux Données" \*.
            *   **Saisie :** Liste déroulante. Par défaut, le niveau d'accès standard pour un étudiant.
            *   **Validation :** Valeur existante.
        *   `statut_compte` (ENUM) :
            *   **Libellé :** "Statut Initial du Compte" \*.
            *   **Saisie :** Liste déroulante : 'actif', 'en_attente_validation' (si `utilisateur.email_valide` doit être à 0 initialement).
            *   **Valeur par Défaut Logique :** Si l'établissement requiert la validation de l'email par l'étudiant, le statut sera 'en_attente_validation'. Sinon, 'actif'. Si les prérequis de scolarité/stage pour accès plateforme ne sont pas encore remplis, un statut 'en_attente_prerequis' (à ajouter à l'ENUM `statut_compte`) pourrait être pertinent avant de devenir 'en_attente_validation' ou 'actif'.
        *   `photo_profil` (`utilisateur.photo_profil`, VARCHAR(255)) :
            *   **Libellé :** "Photo de Profil (Optionnel)".
            *   **Saisie :** Champ de téléversement de fichier (type "file").
            *   **Validation Côté Client/Serveur :** Type de fichier (jpg, png), taille max du fichier. Si uploadée, le fichier est sauvegardé sur le serveur et son chemin relatif est stocké dans `utilisateur.photo_profil`.

    *   **Étape 3 : Soumission du Formulaire et Traitement Côté Serveur (Logique PHP) :**
        1.  **Récupération des Données :** Récupération de toutes les données POSTées.
        2.  **Validation Approfondie :** Ré-exécution de toutes les validations côté serveur (obligatoire, format, longueur, unicité pour `numero_carte_etudiant`, `login_utilisateur`, `email_principal`). Vérification que les IDs sélectionnés pour les FK (`id_groupe_utilisateur`, `id_niveau_acces_donne`) existent dans leurs tables respectives.
            *   **Algorithme d'Unicité :** Avant tout `INSERT`, exécuter des `SELECT COUNT(*)` pour les champs uniques. Si un compte est > 0, retourner une erreur spécifique au champ (ex: "Ce login utilisateur est déjà utilisé.").
        3.  Si une validation échoue, renvoyer le formulaire à l'administrateur avec les données précédemment saisies et des messages d'erreur clairs à côté des champs concernés.
        4.  **Génération de l'ID Utilisateur :**
            *   **Algorithme :** La logique PHP doit générer un `numero_utilisateur` (VARCHAR(50)) qui est garanti unique.
                *   Option 1 : Préfixe + UUID (ex: `ETU_` + `bin2hex(random_bytes(16))`).
                *   Option 2 : Préfixe + Timestamp haute résolution + élément aléatoire.
                *   Une boucle avec vérification d'unicité peut être nécessaire en cas de très rares collisions si l'aléatoire n'est pas assez fort : `do { $new_id = generate_id(); $count = check_db_for_id($new_id); } while ($count > 0);`
        5.  **Hachage du Mot de Passe :** Utilisation d'un algorithme de hachage robuste (ex: `password_hash()` en PHP avec `PASSWORD_ARGON2ID` ou `PASSWORD_BCRYPT`). Le sel est généré automatiquement par ces fonctions.
        6.  **Préparation des Données pour l'Insertion :**
            *   `id_type_utilisateur` est fixé à la valeur VARCHAR correspondant à "TYPE_ETUD" (depuis `type_utilisateur.id_type_utilisateur`).
            *   Si statut 'en_attente_validation', génération d'un `token_validation_email` (chaîne aléatoire unique) et `email_valide = 0`. Sinon, `token_validation_email = NULL` et `email_valide = 1` (si admin crée un compte direct actif).
        7.  **Début de la Transaction Base de Données :** Pour assurer l'atomicité des opérations.
            *   `BEGIN TRANSACTION;` ou équivalent SGBD.
        8.  **`INSERT INTO utilisateur` :**
            *   Insertion de `numero_utilisateur` (généré), `login_utilisateur`, `email_principal`, `mot_de_passe` (haché), `date_creation` (NOW()), `statut_compte`, `id_type_utilisateur`, `id_groupe_utilisateur`, `id_niveau_acces_donne`, `token_validation_email` (si applicable), `email_valide` (si applicable), `photo_profil` (chemin si uploadé).
        9.  **`INSERT INTO etudiant` :**
            *   Si l'insertion dans `utilisateur` est réussie : insertion de `numero_carte_etudiant`, `nom`, `prenom`, ... et le `numero_utilisateur` fraîchement inséré comme clé étrangère.
        10. **Journalisation de l'Action dans `enregistrer` :**
            *   `id_action` (VARCHAR(50) pour "Création Utilisateur Étudiant").
            *   `numero_utilisateur` (de l'administrateur qui effectue l'action).
            *   `date_action` (NOW()).
            *   `type_entite_concernee` = "UTILISATEUR", `id_entite_concernee` = le `numero_utilisateur` du nouvel étudiant.
            *   `details_action` (JSON) : Peut contenir `{ "login_cree": "...", "profil_etudiant_cree": "..." }`.
            *   Si le profil `etudiant` est considéré comme une entité distincte créée : une seconde ligne dans `enregistrer` pour la création du profil étudiant.
        11. **Fin de la Transaction Base de Données :**
            *   Si toutes les insertions réussissent : `COMMIT;`.
            *   Si une erreur survient à une étape : `ROLLBACK;`. Un message d'erreur technique est alors affiché à l'admin, et l'erreur est loguée côté serveur.
        12. **Confirmation à l'Administrateur :**
            *   Si succès : Message "L'étudiant [Prénom Nom] et son compte utilisateur ont été créés avec succès." Boutons pour "Créer un autre étudiant" ou "Retour à la liste des étudiants".
        13. **Envoi de Notification à l'Étudiant (Post-Transaction) :**
            *   Si la création est réussie et le statut le requiert (ex: 'actif' ou 'en_attente_validation').
            *   Le `ServiceEmail` (via `ServiceNotification`) utilise un template de `message` (ex: 'MSG_WELCOME_ETUD_ADMIN_CREATE') et envoie un email à `utilisateur.email_principal` avec :
                *   Message de bienvenue.
                *   `login_utilisateur`.
                *   Le mot de passe initial (si non généré pour que l'utilisateur le définisse via un lien) ou un lien unique pour définir le mot de passe.
                *   Si `statut_compte` = 'en_attente_validation', le lien inclut le `token_validation_email` pour valider l'adresse email.
            *   Une entrée dans `recevoir` peut être créée pour l'étudiant concernant cette notification de création de compte.
        *   **Gestion des Prérequis (Scolarité à jour & Stage effectué) pour l'ACCÈS à la plateforme (non bloquant pour la création initiale par Admin) :**
            *   La création du profil `etudiant` et du compte `utilisateur` par l'ADMIN (comme décrit ci-dessus) peut se faire indépendamment de ces prérequis si l'Admin a besoin d'anticiper.
            *   Cependant, la **LOGIQUE D'AUTHENTIFICATION (Module Auth)** devra vérifier ces prérequis *avant d'autoriser la connexion de l'étudiant*, même si son `statut_compte` est 'actif'.
            *   Cette vérification se fait en consultant `inscrire.id_statut_paiement` (doit être "payé/à jour" pour l'année active) et `SELECT COUNT(*) FROM faire_stage WHERE numero_carte_etudiant = ? AND id_annee_academique_stage = [année active/pertinente]`.
            *   Si les prérequis ne sont pas remplis, la connexion est refusée avec un message approprié, même si le login/mdp est correct et le compte 'actif'.
            *   Le Responsable Scolarité, lui, lors de sa tentative de "Générer Compte Étudiant", *sera* bloqué si ces prérequis ne sont pas marqués dans le système.

    *   **(La suite de B.1.4. à B.1.7 sera traitée dans le message suivant pour maintenir un niveau de détail cohérent par réponse.)**

Ce workflow de création est complexe car il implique la création d'enregistrements dans deux tables principales (`utilisateur` et `etudiant`), la génération sécurisée d'identifiants et de mots de passe, une gestion transactionnelle, la journalisation, et la notification à l'utilisateur final, tout en assurant la validation et l'unicité des données critiques.


Absolument. Poursuivons avec la section **B.1.4. Vue Détaillée du Profil Étudiant** du Module Administration, en maintenant ce niveau d'extrême détail.

---

    *   **B.1.4. Vue Détaillée du Profil Étudiant (Consultation Approfondie) :**
        *   **Accès à l'Interface :**
            1.  Depuis la liste des étudiants (B.1.1), l'administrateur clique sur le lien "Voir Profil Complet" associé à une ligne d'étudiant, ou sur le `numero_carte_etudiant` lui-même (si rendu cliquable).
            2.  Alternativement, après une recherche (B.1.2) qui aboutit à un ou plusieurs résultats, l'action "Voir Profil Complet" peut être disponible.
            3.  La requête HTTP transmettra le `numero_carte_etudiant` (ou le `numero_utilisateur` associé) comme paramètre (ex: `/admin/utilisateurs/etudiants/profil?id=[NUMERO_CARTE_ETUDIANT]`).
        *   **Objectif de l'Interface :** Présenter de manière exhaustive et structurée toutes les informations relatives à un étudiant spécifique, regroupant les données de son profil personnel, de son compte utilisateur, de son parcours académique (inscriptions), de ses soumissions de rapports, et potentiellement de ses interactions (réclamations, notes). Cela permet à l'admin d'avoir une vue à 360 degrés de l'étudiant au sein du système.
        *   **Structure de la Page / Modale :**
            La page est organisée en plusieurs sections distinctes pour une meilleure lisibilité.
            *   **Section 1 : En-tête du Profil Étudiant**
                *   Affichage proéminent de `etudiant.nom`, `etudiant.prenom`.
                *   `etudiant.numero_carte_etudiant`.
                *   Affichage de la `utilisateur.photo_profil` si disponible.
                *   `utilisateur.statut_compte` (avec le même codage couleur que dans la liste).
                *   Boutons d'action principaux : "Modifier Profil Étudiant", "Modifier Compte Utilisateur", "Gérer Inscriptions", "Retour à la liste".

            *   **Section 2 : Informations Personnelles Détaillées (issues de `etudiant`)**
                *   Tous les champs de la table `etudiant` sont affichés de manière lisible (label et valeur) :
                    *   `date_naissance`
                    *   `lieu_naissance`, `pays_naissance`
                    *   `nationalite`
                    *   `sexe`
                    *   `adresse_postale`, `ville`, `code_postal`
                    *   `telephone`
                    *   `email_contact_secondaire`
                    *   `contact_urgence_nom`, `contact_urgence_telephone`, `contact_urgence_relation`
                *   Ces informations sont généralement en lecture seule dans cette vue, la modification se faisant via le formulaire dédié (B.1.5).

            *   **Section 3 : Informations du Compte Utilisateur (issues de `utilisateur` et tables liées)**
                *   `numero_utilisateur`
                *   `login_utilisateur`
                *   `email_principal` (avec statut de validation `email_valide` : "Validé" / "Non validé - En attente de vérification")
                *   `libelle_type_utilisateur` (via `type_utilisateur`)
                *   `libelle_groupe_utilisateur` (via `groupe_utilisateur`)
                *   `libelle_niveau_acces_donne` (via `niveau_acces_donne`)
                *   `date_creation` du compte
                *   `derniere_connexion`
                *   `preferences_2fa_active` (Affiché "Oui" / "Non")
                *   `tentatives_connexion_echouees` (si > 0) et `compte_bloque_jusqua` (si applicable).

            *   **Section 4 : Historique des Inscriptions Académiques (issue de `inscrire` et tables liées)**
                *   **Affichage :** Un tableau listant chaque inscription de l'étudiant. Si vide, un message "Aucune inscription enregistrée pour cet étudiant."
                *   **SQL Query (pour un étudiant donné, `num_etu_param` étant le `numero_carte_etudiant`) :**
                    ```sql
                    SELECT
                        aa.libelle_annee_academique,
                        ne.libelle_niveau_etude,
                        i.montant_inscription,
                        i.date_inscription,
                        spr.libelle_statut_paiement,
                        i.date_paiement,
                        i.numero_recu_paiement,
                        dpr.libelle_decision_passage
                    FROM
                        inscrire i
                    JOIN
                        annee_academique aa ON i.id_annee_academique = aa.id_annee_academique
                    JOIN
                        niveau_etude ne ON i.id_niveau_etude = ne.id_niveau_etude
                    JOIN
                        statut_paiement_ref spr ON i.id_statut_paiement = spr.id_statut_paiement
                    LEFT JOIN
                        decision_passage_ref dpr ON i.id_decision_passage = dpr.id_decision_passage
                    WHERE
                        i.numero_carte_etudiant = '[num_etu_param]'
                    ORDER BY
                        aa.date_debut DESC, i.date_inscription DESC;
                    ```
                *   **Colonnes du Tableau d'Inscriptions :**
                    *   "Année Académique" (`libelle_annee_academique`)
                    *   "Niveau d'Étude" (`libelle_niveau_etude`)
                    *   "Date d'Inscription" (`date_inscription`)
                    *   "Montant Inscription" (`montant_inscription`)
                    *   "Statut Paiement" (`libelle_statut_paiement`)
                    *   "Date Paiement" (`date_paiement`)
                    *   "N° Reçu" (`numero_recu_paiement`)
                    *   "Décision de Passage" (`libelle_decision_passage` - peut être NULL si pas encore décidé)
                *   **Actions par ligne d'inscription (optionnel) :** Un lien "Modifier cette inscription" menant à l'interface B.1.7 pré-remplie pour cette inscription spécifique.

            *   **Section 5 : Historique des Rapports de Soutenance Soumis (issue de `rapport_etudiant` et tables liées)**
                *   **Affichage :** Un tableau listant tous les rapports soumis par l'étudiant. Si vide, "Aucun rapport soumis par cet étudiant."
                *   **SQL Query (pour un étudiant donné) :**
                    ```sql
                    SELECT
                        r.id_rapport_etudiant,
                        r.libelle_rapport_etudiant,
                        r.theme,
                        r.date_soumission,
                        srr.libelle_statut_rapport,
                        r.date_derniere_modif
                        -- Potentiellement, un COUNT(ds.id_document) AS nombre_versions
                    FROM
                        rapport_etudiant r
                    JOIN
                        statut_rapport_ref srr ON r.id_statut_rapport = srr.id_statut_rapport
                    -- LEFT JOIN document_soumis ds ON r.id_rapport_etudiant = ds.id_rapport_etudiant GROUP BY r.id_rapport_etudiant (pour compter versions)
                    WHERE
                        r.numero_carte_etudiant = '[num_etu_param]'
                    ORDER BY
                        r.date_soumission DESC;
                    ```
                *   **Colonnes du Tableau des Rapports :**
                    *   "ID Rapport" (`id_rapport_etudiant`)
                    *   "Titre/Libellé" (`libelle_rapport_etudiant`)
                    *   "Thème" (`theme`)
                    *   "Date de Soumission Initiale" (`date_soumission`)
                    *   "Dernière Modification" (`date_derniere_modif`)
                    *   "Statut Actuel" (`libelle_statut_rapport`)
                    *   "Nombre de Versions Soumises" (calculé via `document_soumis` si besoin de ce détail)
                *   **Actions par ligne de rapport :**
                    *   "Voir Détails du Rapport" : Mène à une vue administrative du rapport, incluant les documents soumis (`document_soumis`), l'historique des validations de conformité (`approuver`), les votes de la commission (`vote_commission`), et le PV associé (`compte_rendu`). C'est une vue de supervision complète.
                    *   "Télécharger Documents" : Accès direct aux fichiers de `document_soumis`.

            *   **Section 6 : Historique des Réclamations (issue de `reclamation` et tables liées)**
                *   **Condition d'Affichage :** Si l'administrateur a les droits de consulter les réclamations (permission `TRAIT_ADMIN_VIEW_RECLAMATIONS`).
                *   **Affichage :** Tableau des réclamations de l'étudiant.
                *   **SQL Query :**
                    ```sql
                    SELECT
                        rec.id_reclamation,
                        rec.sujet_reclamation,
                        rec.date_soumission,
                        srec.libelle_statut_reclamation,
                        rec.date_reponse,
                        pa.nom AS nom_traitant, -- Si le numero_personnel_traitant est lié à personnel_administratif
                        pa.prenom AS prenom_traitant
                    FROM
                        reclamation rec
                    JOIN
                        statut_reclamation_ref srec ON rec.id_statut_reclamation = srec.id_statut_reclamation
                    LEFT JOIN
                        personnel_administratif pa ON rec.numero_personnel_traitant = pa.numero_personnel_administratif -- Attention: traitant peut aussi être un enseignant admin?
                    WHERE
                        rec.numero_carte_etudiant = '[num_etu_param]'
                    ORDER BY
                        rec.date_soumission DESC;
                    ```
                *   **Colonnes du Tableau des Réclamations :** "ID Réclamation", "Sujet", "Date Soumission", "Statut", "Date Réponse", "Traité par".
                *   **Actions par ligne :** "Voir Détail Réclamation" : Ouvre une vue avec la `description_reclamation` et la `reponse_reclamation`.

            *   **Section 7 : Aperçu des Notes (issue de `evaluer` et tables liées)**
                *   **Condition d'Affichage :** Si l'administrateur (ou RS) a les droits de voir les notes.
                *   **Affichage :** Un tableau ou une section résumant les notes obtenues par ECUE/UE, potentiellement regroupées par année académique d'inscription. Pourrait afficher une moyenne générale si calculable et pertinent pour ce rôle.
                *   **SQL (Simplifié, pour une ECUE) :**
                    ```sql
                    SELECT
                        ec.libelle_ecue,
                        ue.libelle_ue,
                        ev.note,
                        ev.date_evaluation,
                        ens.nom AS nom_evaluateur,
                        ens.prenom AS prenom_evaluateur
                    FROM
                        evaluer ev
                    JOIN
                        ecue ec ON ev.id_ecue = ec.id_ecue
                    JOIN
                        ue ue ON ec.id_ue = ue.id_ue
                    JOIN
                        enseignant ens ON ev.numero_enseignant = ens.numero_enseignant
                    WHERE
                        ev.numero_carte_etudiant = '[num_etu_param]'
                    ORDER BY
                        ue.libelle_ue, ec.libelle_ecue;
                    ```
                *   **Actions :** Peut-être un lien vers l'interface de modification de note (Section E.2) si l'admin a des droits très élevés.

        *   **Logique d'Affichage :**
            *   Le contrôleur PHP (ex: `UtilisateurController@voirProfilEtudiant` ou `EtudiantProfilController@afficherPourAdmin`) récupère le `numero_carte_etudiant` depuis l'URL.
            *   Il exécute les différentes requêtes SQL pour peupler chaque section de la vue.
            *   Les données sont passées au template de la vue (ex: `Administration/Utilisateurs/profil_etudiant_detail.php`).
            *   Le template affiche les informations de manière structurée, utilisant des conditions pour afficher ou masquer des sections basées sur l'existence de données (ex: afficher "Aucun rapport soumis" si la requête ne retourne rien).

        *   **Considérations :**
            *   **Performance :** La page peut devenir lourde si toutes les informations historiques (inscriptions, rapports, notes, réclamations sur plusieurs années) sont chargées en une seule fois. Des stratégies de chargement progressif (lazy loading pour certaines sections) ou de pagination interne aux sections (ex: paginer la liste des inscriptions si elle est très longue) peuvent être nécessaires.
            *   **Autorisations d'Affichage :** Même si c'est une vue "Admin", certains détails pourraient être masqués si l'admin connecté n'a pas spécifiquement le droit de voir, par exemple, le détail des notes. Les permissions basées sur `traitement` doivent être vérifiées.
            *   **Navigation :** Des "fils d'Ariane" (breadcrumbs) doivent être présents pour permettre à l'admin de revenir facilement à la liste des étudiants (B.1.1) ou au tableau de bord principal (A).

Cette vue détaillée est une consultation centralisée puissante, fournissant une image complète du parcours d'un étudiant dans le système. Elle est la base avant d'initier des modifications spécifiques via les formulaires dédiés.

---
**(Prêt pour B.1.5. Modification du Profil Étudiant et du Compte Utilisateur.)**


Excellent. Poursuivons avec la section **B.1.5. Modification du Profil Étudiant et du Compte Utilisateur**, en conservant ce niveau de détail.

---

    *   **B.1.5. Modification du Profil Étudiant (`etudiant`) et du Compte Utilisateur (`utilisateur`) Associé :**
        *   **Accès à l'Interface de Modification :**
            1.  Depuis la liste des étudiants (B.1.1), l'administrateur clique sur l'action "Modifier Profil Étudiant" ou "Modifier Compte Utilisateur" associée à une ligne d'étudiant spécifique.
            2.  Depuis la Vue Détaillée du Profil Étudiant (B.1.4), des boutons "Modifier Profil Étudiant" et "Modifier Compte Utilisateur" sont également disponibles dans l'en-tête ou les sections correspondantes.
            3.  La requête HTTP transmet le `numero_carte_etudiant` et/ou le `numero_utilisateur` de l'étudiant concerné pour que le formulaire soit pré-rempli avec les données existantes.
        *   **Objectif de l'Interface :** Permettre à l'administrateur (ou RS habilité) de corriger, mettre à jour ou compléter les informations personnelles de l'étudiant stockées dans la table `etudiant`, ainsi que les attributs de son compte d'accès stockés dans la table `utilisateur`.
        *   **Structure du Formulaire de Modification :**
            Souvent, l'interface est un formulaire unique mais divisé en onglets ou sections distinctes pour plus de clarté : "Informations Personnelles Étudiant" et "Gestion du Compte Utilisateur". Il peut aussi s'agir de deux formulaires distincts accessibles par des boutons différents. Les champs sont pré-remplis avec les valeurs actuelles.

            *   **Partie 1 : Modification des Informations du Profil Étudiant (cible la table `etudiant`)**
                *   **Champs Affichés et Modifiables (pré-remplis avec les données de `etudiant` pour le `numero_carte_etudiant` sélectionné) :**
                    *   `numero_carte_etudiant` (VARCHAR(50), PK) : Affiché en lecture seule. La modification de la clé primaire est généralement une opération complexe et risquée, évitée dans les interfaces CRUD standards. Si une correction est absolument nécessaire, cela pourrait nécessiter une procédure administrative spécifique ou une intervention directe en base avec une extrême prudence et vérification des intégrités référentielles.
                    *   `nom` (VARCHAR(100)) : Champ texte, modifiable. Validation : obligatoire.
                    *   `prenom` (VARCHAR(100)) : Champ texte, modifiable. Validation : obligatoire.
                    *   `date_naissance` (DATE) : Sélecteur de date, modifiable. Validation : format, plausibilité.
                    *   `lieu_naissance` (VARCHAR(100)) : Champ texte, modifiable.
                    *   `pays_naissance` (VARCHAR(50)) : Liste déroulante/texte, modifiable.
                    *   `nationalite` (VARCHAR(50)) : Liste déroulante/texte, modifiable.
                    *   `sexe` (ENUM) : Boutons radio/liste, modifiable.
                    *   `adresse_postale` (TEXT) : Zone de texte, modifiable.
                    *   `ville` (VARCHAR(100)) : Champ texte, modifiable.
                    *   `code_postal` (VARCHAR(20)) : Champ texte, modifiable.
                    *   `telephone` (VARCHAR(20)) : Champ texte, modifiable.
                    *   `email_contact_secondaire` (VARCHAR(255)) : Champ texte, modifiable. Validation : format email.
                    *   `contact_urgence_nom`, `contact_urgence_telephone`, `contact_urgence_relation` : Champs texte, modifiables.
                *   **Champs Non Modifiables directement ici (liés au compte utilisateur) :** `numero_utilisateur` (FK interne).
                *   **Boutons d'Action :** "Enregistrer les Modifications (Profil)", "Annuler".

            *   **Partie 2 : Modification des Informations du Compte Utilisateur (cible la table `utilisateur`)**
                *   **Champs Affichés et Modifiables (pré-remplis avec les données de `utilisateur` pour le `numero_utilisateur` associé à l'étudiant) :**
                    *   `numero_utilisateur` (VARCHAR(50), PK) : Affiché en lecture seule.
                    *   `login_utilisateur` (VARCHAR(100), UNIQUE) : Champ texte, modifiable.
                        *   **Validation :** Format, longueur, et surtout unicité si la valeur est changée (`SELECT COUNT(*) FROM utilisateur WHERE login_utilisateur = ? AND numero_utilisateur != ?`). Message d'erreur si le nouveau login est déjà pris.
                    *   `email_principal` (VARCHAR(255), UNIQUE) : Champ texte, modifiable.
                        *   **Validation :** Format email, unicité si changé.
                        *   **Workflow si changé :** Le système DOIT marquer `utilisateur.email_valide = 0` et générer un nouveau `utilisateur.token_validation_email`. Une nouvelle notification est envoyée à la nouvelle adresse pour revalidation. L'ancienne adresse peut recevoir une notification du changement. L'accès de l'utilisateur peut être temporairement restreint jusqu'à validation de la nouvelle adresse.
                    *   `id_type_utilisateur` (VARCHAR(50), FK) : Affiché (ex: "TYPE_ETUD"). Généralement non modifiable via cette interface pour un étudiant. Changer le type d'un utilisateur est une opération majeure avec des implications de droits et de profil, potentiellement gérée par une fonction admin dédiée (ex: convertir un compte).
                    *   `id_groupe_utilisateur` (VARCHAR(50), FK) : Liste déroulante, modifiable. Permet de changer l'étudiant de groupe (ex: d'un groupe générique "GRP_ETUDIANT" à un groupe plus spécifique "GRP_ETUD_M2_PROJET_X"). Impacte directement ses permissions si les groupes sont liés à des `traitement` distincts.
                    *   `id_niveau_acces_donne` (VARCHAR(50), FK) : Liste déroulante, modifiable. Change la portée des données que l'utilisateur peut voir, selon la logique applicative qui interprète ce niveau.
                    *   `statut_compte` (ENUM) : Liste déroulante, modifiable ("actif", "inactif", "bloque", etc.). Permet à l'admin d'activer/désactiver/bloquer manuellement le compte.
                        *   Si passage à "bloque", `utilisateur.compte_bloque_jusqua` pourrait être mis à une date très lointaine ou indéfinie (ou l'admin peut spécifier une durée).
                        *   Si passage de "bloque" à "actif", `utilisateur.tentatives_connexion_echouees` est remis à 0 et `compte_bloque_jusqua` à NULL.
                    *   `photo_profil` (`utilisateur.photo_profil`) : Champ de téléversement pour changer ou supprimer la photo. Implique la gestion du fichier sur le serveur.
                *   **Actions Spécifiques de Gestion du Compte Utilisateur (souvent via des boutons dédiés) :**
                    *   **"Réinitialiser le Mot de Passe" :**
                        *   **Option 1 (Générer MDP) :** Le système génère un mot de passe temporaire fort, l'affiche à l'administrateur (avec option de copie) ET/OU l'envoie par email à `utilisateur.email_principal` de l'étudiant. Option pour "Forcer changement à la prochaine connexion".
                        *   **Option 2 (Envoyer Lien de Réinit.) :** Le système génère un `token_reset_mdp` unique, le stocke avec `date_expiration_token_reset` dans `utilisateur`, et envoie un email à `utilisateur.email_principal` avec un lien unique contenant ce token pour que l'étudiant définisse lui-même son nouveau mot de passe.
                    *   **"Forcer la Validation de l'Email Principal" :**
                        *   Utile si `utilisateur.email_valide = 0`.
                        *   Régénère `token_validation_email` et `date_expiration_token` (si expiration pour validation token).
                        *   Renvoie l'email de validation à `utilisateur.email_principal`.
                    *   **"Gérer Authentification à Deux Facteurs (2FA)" (Si 2FA est implémenté) :**
                        *   Afficher si `preferences_2fa_active = 1`.
                        *   Option pour l'administrateur de :
                            *   Désactiver la 2FA pour le compte (ex: si l'étudiant a perdu son appareil 2FA). Remet `preferences_2fa_active = 0` et `secret_2fa = NULL`.
                            *   Aider à reconfigurer la 2FA (générer un nouveau `secret_2fa` et afficher le QR code/clé à l'étudiant sous conditions sécurisées).
                *   **Boutons d'Action :** "Enregistrer les Modifications (Compte)", "Annuler".

        *   **Workflow de Soumission des Modifications (pour chaque partie du formulaire ou globalement) :**
            1.  **Récupération des Données :** Le serveur PHP reçoit les données du formulaire POSTé.
            2.  **Identification de la Cible :** Le `numero_carte_etudiant` et/'ou `numero_utilisateur` (qui étaient des champs cachés ou des paramètres d'URL) sont utilisés pour identifier l'enregistrement à mettre à jour.
            3.  **Validation des Données Modifiées :**
                *   Toutes les validations appliquées lors de la création sont ré-appliquées aux champs modifiés (format, longueur, unicité pour `login_utilisateur` et `email_principal` *en excluant l'enregistrement actuel de la vérification d'unicité*).
                *   `SELECT COUNT(*) FROM utilisateur WHERE login_utilisateur = ? AND numero_utilisateur != ?;`
                *   Si une validation échoue, le formulaire est re-présenté avec les erreurs.
            4.  **Comparaison avec les Anciennes Valeurs :** La logique PHP devrait idéalement récupérer les valeurs actuelles en base avant l'UPDATE pour identifier précisément quels champs ont été modifiés. Ceci est essentiel pour une journalisation fine.
            5.  **Hachage du Mot de Passe (si un nouveau MDP a été généré par l'admin) :** Si l'admin a entré un nouveau MDP initial pour l'utilisateur.
            6.  **Traitement Spécifique des Actions (Réinit. MDP, Validation Email) :** Exécution des logiques correspondantes (génération de tokens, envoi d'emails).
            7.  **Début de la Transaction Base de Données.**
            8.  **Exécution des `UPDATE` :**
                *   `UPDATE etudiant SET nom = ?, prenom = ?, ... WHERE numero_carte_etudiant = ?;` (si des champs de `etudiant` ont changé).
                *   `UPDATE utilisateur SET login_utilisateur = ?, email_principal = ?, statut_compte = ?, ... WHERE numero_utilisateur = ?;` (si des champs de `utilisateur` ont changé).
            9.  **Journalisation Détaillée dans `enregistrer` :**
                *   Pour chaque champ modifié significativement, une entrée ou une description détaillée dans `details_action` (JSON) indiquant l'ancien et le nouveau contenu.
                *   Ex: `id_action` (pour "Modification Profil Étudiant" ou "Modification Compte Utilisateur"), `numero_utilisateur` (admin), `type_entite_concernee`="ETUDIANT" ou "UTILISATEUR", `id_entite_concernee` (le `numero_carte_etudiant` ou `numero_utilisateur` de l'étudiant), `details_action`: `{"champ_modifie": "email_principal", "ancienne_valeur": "old@example.com", "nouvelle_valeur": "new@example.com"}`.
            10. **Fin de la Transaction :** `COMMIT` si tout succès, `ROLLBACK` si erreur.
            11. **Confirmation à l'Administrateur :** Message "Les modifications ont été enregistrées avec succès." Redirection vers la vue détaillée (B.1.4) ou la liste (B.1.1).
            12. **Notifications à l'Étudiant :** Si des changements critiques ont été effectués par l'admin (ex: changement d'`email_principal`, réinitialisation de mot de passe par l'admin), une notification est envoyée à l'étudiant sur son (nouvel) `email_principal` pour l'informer de l'action administrative.

        *   **Considérations Spécifiques :**
            *   **Sécurité :** Ne jamais afficher le mot de passe haché. Permettre la réinitialisation mais pas la visualisation du mot de passe actuel.
            *   **Impact des Changements de `statut_compte`, `id_groupe_utilisateur`, `id_niveau_acces_donne` :** Ces changements ont des effets immédiats sur les capacités de l'étudiant. L'admin doit être conscient des conséquences.
            *   **Intégrité des Données Uniques :** La gestion des conflits si un nouveau `login_utilisateur` ou `email_principal` est déjà pris est cruciale.
            *   **Interface Utilisateur :** Les formulaires doivent être clairs. Les erreurs de validation bien mises en évidence. La séparation entre les modifications du "profil métier" (`etudiant`) et du "compte technique" (`utilisateur`) doit être logique pour l'admin.

Cette fonctionnalité de modification est puissante et doit être utilisée avec discernement par les administrateurs, en gardant toujours à l'esprit l'impact sur l'étudiant et la sécurité globale du système. La journalisation exhaustive est non négociable.

---
**(Prêt pour B.1.6. Suppression / Désactivation / Archivage d'un Étudiant.)**

Parfait. Continuons avec **B.1.6. Suppression / Désactivation / Archivage d'un Étudiant**.

---

    *   **B.1.6. Suppression / Désactivation / Archivage d'un Étudiant :**
        *   **Accès à la Fonctionnalité :**
            1.  Depuis la liste des étudiants (B.1.1), une action "Gérer Statut/Supprimer" ou des actions distinctes "Désactiver", "Archiver", "Supprimer (exceptionnel)" peuvent être disponibles par ligne d'étudiant.
            2.  Depuis la Vue Détaillée du Profil Étudiant (B.1.4), des boutons similaires peuvent être présents.
        *   **Objectif de l'Interface :** Fournir des mécanismes contrôlés pour gérer la fin du cycle de vie d'un compte étudiant dans le système. L'accent est mis sur la désactivation et l'archivage pour préserver l'historique, la suppression physique étant une mesure exceptionnelle.
        *   **Philosophie Générale (Rappel) :**
            *   **Préservation de l'Intégrité Référentielle et de l'Historique :** Pour les étudiants ayant un parcours académique (inscriptions, notes, rapports, PV), une suppression physique (`DELETE FROM ...`) est fortement déconseillée. Elle briserait les liens avec ces données historiques et pourrait rendre l'audit ou la consultation ultérieure impossible, voire illégale selon les réglementations de conservation des données de l'établissement.
            *   **Principe de "Soft Delete" / Changement de Statut :** La méthode privilégiée est de modifier le `utilisateur.statut_compte` pour rendre le compte inaccessible tout en conservant les données associées.

        *   **B.1.6.1. Désactivation d'un Compte Étudiant :**
            *   **Cas d'Usage :** Suspension temporaire, étudiant quittant l'établissement en cours d'année, fin de droits d'accès sans pour autant archiver immédiatement toutes les données. Étudiant diplômé mais dont les données doivent rester consultables un certain temps avant archivage.
            *   **Interface :** Bouton "Désactiver le Compte".
            *   **Workflow et Algorithme :**
                1.  **Confirmation :** L'administrateur clique sur "Désactiver". Une boîte de dialogue de confirmation s'affiche : "Êtes-vous sûr de vouloir désactiver le compte de [Prénom Nom de l'étudiant] (`numero_carte_etudiant`) ? L'étudiant ne pourra plus se connecter." Option pour ajouter un motif de désactivation.
                2.  **Action Côté Serveur (PHP) :**
                    *   Sur confirmation, `UPDATE utilisateur SET statut_compte = 'inactif' WHERE numero_utilisateur = '[numero_utilisateur_cible]';`
                    *   (Optionnel) Invalidation immédiate de toute session active pour cet utilisateur.
                3.  **Journalisation :** `INSERT` dans `enregistrer` : `id_action` = (ID de "Désactivation Compte Utilisateur"), `numero_utilisateur` (admin), `type_entite_concernee` = "UTILISATEUR", `id_entite_concernee` = `numero_utilisateur` de l'étudiant, `details_action` (JSON) : `{ "ancien_statut": "actif", "nouveau_statut": "inactif", "motif": "[motif_saisi_par_admin]" }`.
                4.  **Notification (Optionnelle) :** L'étudiant pourrait recevoir un email l'informant de la désactivation de son compte si c'est pertinent (ex: suite à une demande de sa part ou pour une raison administrative claire).
                *   **Conséquences :** L'étudiant ne peut plus se connecter. Ses données (profil, inscriptions, rapports, etc.) restent intactes dans la base de données et consultables par les administrateurs/personnel habilité.

        *   **B.1.6.2. Archivage d'un Compte Étudiant :**
            *   **Cas d'Usage :** Gestion du cycle de vie long terme. Étudiants diplômés depuis plusieurs années, étudiants ayant définitivement quitté l'établissement et dont les données doivent être conservées pour des raisons légales ou statistiques mais ne sont plus actives. L'archivage peut aussi être une étape avant une purge de données encore plus tardive selon les politiques de rétention.
            *   **Interface :** Bouton "Archiver le Compte".
            *   **Workflow et Algorithme :**
                1.  **Confirmation :** Similaire à la désactivation, mais le message insiste sur le caractère plus permanent : "Êtes-vous sûr de vouloir archiver le compte de [Prénom Nom de l'étudiant] ? Le compte deviendra inaccessible et sera traité selon les politiques d'archivage." Motif optionnel.
                2.  **Action Côté Serveur (PHP) :**
                    *   `UPDATE utilisateur SET statut_compte = 'archive' WHERE numero_utilisateur = '[numero_utilisateur_cible]';`
                    *   (Optionnel) La logique applicative pourrait également exécuter d'autres actions liées à l'archivage :
                        *   Anonymisation partielle de certaines données personnelles dans `etudiant` si la politique RGPD/de confidentialité l'exige (ex: remplacer certains champs par des valeurs génériques, mais conserver les données académiques clés). Ceci est une opération complexe et doit être soigneusement conçue.
                        *   Marquage des données associées (inscriptions, rapports) comme "archivées" si ces tables ont aussi des statuts d'archivage.
                        *   Déplacement physique des documents associés (`document_soumis.chemin_fichier`) vers un stockage d'archive distinct (opération de système de fichiers).
                3.  **Journalisation :** `INSERT` dans `enregistrer` : `id_action` = (ID de "Archivage Compte Utilisateur"), `details_action` (JSON) : `{ "ancien_statut": "inactif/actif", "nouveau_statut": "archive", "actions_complementaires_archivage": "[description des actions si effectuées]" }`.
                *   **Conséquences :** Compte inaccessible. Données conservées mais potentiellement filtrées des vues opérationnelles par défaut. L'accès aux données archivées se fait via des interfaces d'administration spécifiques "Consultation Archives".

        *   **B.1.6.3. Suppression Physique d'un Profil Étudiant et Compte Utilisateur (EXCEPTIONNELLE) :**
            *   **Cas d'Usage STRICTEMENT Limités :**
                1.  Compte créé par erreur flagrante (ex: doublon immédiat, données manifestement incorrectes) ET **absolument aucune donnée académique ou administrative significative liée** (pas d'inscription validée, pas de rapport soumis, pas de notes, pas de réclamation traitée).
                2.  Demande explicite de suppression au titre du droit à l'effacement (RGPD), après analyse juridique et vérification qu'aucune obligation légale de conservation ne s'y oppose.
            *   **Interface :** Bouton "Supprimer Définitivement le Profil et le Compte". Ce bouton devrait être visuellement distinct et potentiellement nécessiter une confirmation supplémentaire (ex: re-saisie du mot de passe de l'admin ou un code de confirmation).
            *   **Workflow et Algorithme (TRÈS PRUDENT) :**
                1.  **Avertissement Ultime :** Message très explicite : "ATTENTION : Cette action va supprimer DÉFINITIVEMENT toutes les données de profil et le compte utilisateur de [Prénom Nom de l'étudiant] (`numero_carte_etudiant`). Cette opération est IRRÉVERSIBLE. Voulez-vous continuer ?"
                2.  **Vérification Intensive des Dépendances Côté Serveur (PHP) :**
                    *   `SELECT COUNT(*) FROM inscrire WHERE numero_carte_etudiant = ?;`
                    *   `SELECT COUNT(*) FROM rapport_etudiant WHERE numero_carte_etudiant = ?;`
                    *   `SELECT COUNT(*) FROM evaluer WHERE numero_carte_etudiant = ?;`
                    *   `SELECT COUNT(*) FROM reclamation WHERE numero_carte_etudiant = ?;`
                    *   `SELECT COUNT(*) FROM document_soumis JOIN rapport_etudiant ON ... WHERE rapport_etudiant.numero_carte_etudiant = ?;` (pour les documents de cet étudiant).
                    *   Vérifier d'autres tables potentiellement liées (ex: `affecter`, `vote_commission` si l'étudiant est lié à des jurys en tant que candidat).
                    *   **Si une de ces requêtes retourne un compte > 0 (ou une valeur seuil définie), la suppression physique EST BLOQUÉE.** L'admin reçoit un message "Impossible de supprimer : des données académiques/administratives sont associées à cet étudiant. Veuillez procéder à une désactivation ou un archivage."
                3.  **Si Toutes les Vérifications de Dépendances Passent (compte réellement vide ou suppression autorisée pour RGPD) :**
                    *   **Début de la Transaction Base de Données.**
                    *   `DELETE FROM historique_mot_de_passe WHERE numero_utilisateur = (SELECT numero_utilisateur FROM etudiant WHERE numero_carte_etudiant = ?);` (si existe)
                    *   `DELETE FROM pister WHERE numero_utilisateur = (SELECT numero_utilisateur FROM etudiant WHERE numero_carte_etudiant = ?);`
                    *   `DELETE FROM enregistrer WHERE numero_utilisateur = (SELECT numero_utilisateur FROM etudiant WHERE numero_carte_etudiant = ?) OR (type_entite_concernee = 'ETUDIANT' AND id_entite_concernee = ?) OR (type_entite_concernee = 'UTILISATEUR' AND id_entite_concernee = (SELECT numero_utilisateur FROM etudiant WHERE numero_carte_etudiant = ?));` (nettoyage prudent des logs liés, ou conservation pour trace de la suppression).
                    *   Supprimer les enregistrements des tables de liaison de chat/notification s'il y en a : `lecture_message`, `participant_conversation`, `recevoir`.
                    *   `DELETE FROM etudiant WHERE numero_carte_etudiant = ?;`
                    *   `DELETE FROM utilisateur WHERE numero_utilisateur = (le numero_utilisateur qui était lié à l'étudiant);` (Cette requête doit être précise pour ne pas supprimer un autre utilisateur par erreur). Idéalement, récupérer le `numero_utilisateur` à partir de la table `etudiant` avant de la supprimer.
                    *   (Optionnel) Suppression physique des fichiers `utilisateur.photo_profil` du serveur.
                    *   **Fin de la Transaction (`COMMIT` / `ROLLBACK`).**
                4.  **Journalisation de la Suppression Physique :** Même si les enregistrements de `enregistrer` liés à l'utilisateur sont purgés, une entrée spécifique pour l'action de suppression doit être faite, par l'admin, référençant l'`id_entite_concernee` qui vient d'être supprimé, indiquant clairement qu'une suppression physique a eu lieu. Cette ligne de log de suppression devient la seule trace.
                5.  **Confirmation à l'Administrateur :** "Le profil et le compte de [Prénom Nom] ont été définitivement supprimés."

        *   **Tables SQL Impliquées (et ordre potentiel des opérations pour suppression physique) :**
            1.  Vérification des dépendances : `inscrire`, `rapport_etudiant`, `evaluer`, `reclamation`, `document_soumis` (via `rapport_etudiant`), `affecter`, `vote_commission`, etc.
            2.  Suppression des données périphériques liées au `numero_utilisateur` : `historique_mot_de_passe`, `pister`, `lecture_message`, `participant_conversation` (et potentiellement `message_chat` si des messages ne concernent que cet utilisateur, ou anonymiser l'expéditeur), `recevoir`.
            3.  Suppression des logs d'actions concernant cet utilisateur (ou cet étudiant) de `enregistrer` (sauf le log de la suppression elle-même). Décision de conservation à prendre.
            4.  Suppression de `etudiant`.
            5.  Suppression de `utilisateur`.
        *   **Considérations Spécifiques :**
            *   **Réversibilité :** La désactivation et l'archivage sont réversibles (en changeant le `statut_compte`). La suppression physique ne l'est pas.
            *   **Politique de Conservation des Données :** L'établissement doit avoir une politique claire sur la durée de conservation des données étudiantes actives, inactives, et archivées, ainsi que les conditions de suppression définitive. Cette politique guide les options proposées à l'admin.
            *   **Droits d'Administration :** La suppression physique doit être réservée à un rôle d'administrateur système avec les plus hauts privilèges et nécessiter des confirmations robustes. Les rôles de Responsable Scolarité ne devraient typiquement avoir que des droits de désactivation/archivage.

Cette gestion fine du cycle de vie des comptes étudiants assure à la fois la maintenabilité du système et le respect des obligations de conservation et de confidentialité des données.

---
**(Prêt pour B.1.7. Gestion des Inscriptions d'un Étudiant.)**


Parfait, continuons avec **B.1.7. Gestion des Inscriptions d'un Étudiant**.

---

    *   **B.1.7. Gestion des Inscriptions Administratives et Pédagogiques d'un Étudiant (cible la table `inscrire`) :**
        *   **Accès à l'Interface de Gestion des Inscriptions :**
            1.  Depuis la liste des étudiants (B.1.1) ou la Vue Détaillée du Profil Étudiant (B.1.4), un bouton/lien "Gérer Inscriptions" est disponible pour un étudiant spécifique.
            2.  Cliquer sur ce lien redirige l'administrateur (ou RS habilité) vers une interface dédiée à la gestion des inscriptions de CET étudiant. Le `numero_carte_etudiant` est transmis en paramètre et sert de contexte.
        *   **Objectif de l'Interface :** Fournir un historique complet des inscriptions de l'étudiant et permettre l'ajout de nouvelles inscriptions, la modification des inscriptions existantes (principalement pour les statuts de paiement et les décisions de passage), et exceptionnellement la suppression d'une inscription erronée. C'est une fonctionnalité clé pour le suivi du cursus par le Responsable Scolarité.
        *   **Structure de la Page / Modale :**
            La page affiche en en-tête les informations identifiant l'étudiant concerné (`numero_carte_etudiant`, `nom`, `prenom`). En dessous, un tableau liste les inscriptions et un bouton permet d'en ajouter une nouvelle.

            *   **B.1.7.1. Listage des Inscriptions de l'Étudiant :**
                *   **Affichage :** Un tableau présentant tous les enregistrements de la table `inscrire` pour le `numero_carte_etudiant` actuellement sélectionné. Si aucune inscription, un message "Aucune inscription enregistrée pour cet étudiant" s'affiche.
                *   **SQL Requête de Base (pour l'étudiant `[num_etu_param]`) :**
                    ```sql
                    SELECT
                        i.id_annee_academique, -- PK composite, pour identifier l'inscription
                        i.id_niveau_etude,   -- PK composite
                        aa.libelle_annee_academique,
                        ne.libelle_niveau_etude,
                        i.montant_inscription,
                        i.date_inscription,
                        spr.libelle_statut_paiement,
                        i.id_statut_paiement, -- Pour la modification
                        i.date_paiement,
                        i.numero_recu_paiement,
                        dpr.libelle_decision_passage,
                        i.id_decision_passage -- Pour la modification
                    FROM
                        inscrire i
                    JOIN
                        annee_academique aa ON i.id_annee_academique = aa.id_annee_academique
                    JOIN
                        niveau_etude ne ON i.id_niveau_etude = ne.id_niveau_etude
                    JOIN
                        statut_paiement_ref spr ON i.id_statut_paiement = spr.id_statut_paiement
                    LEFT JOIN
                        decision_passage_ref dpr ON i.id_decision_passage = dpr.id_decision_passage
                    WHERE
                        i.numero_carte_etudiant = '[num_etu_param]'
                    ORDER BY
                        aa.date_debut DESC, i.date_inscription DESC;
                    ```
                *   **Colonnes du Tableau des Inscriptions :**
                    *   "Année Académique" (`libelle_annee_academique`)
                    *   "Niveau d'Étude" (`libelle_niveau_etude`)
                    *   "Date d'Inscription" (`date_inscription`)
                    *   "Montant Dû" (`montant_inscription`)
                    *   "Statut Paiement" (`libelle_statut_paiement`)
                    *   "Date Paiement Effectué" (`date_paiement`)
                    *   "Numéro de Reçu" (`numero_recu_paiement`)
                    *   "Décision de Passage (Fin d'Année)" (`libelle_decision_passage`)
                *   **Actions par Ligne d'Inscription :** Boutons/icônes pour "Modifier cette Inscription", "Supprimer cette Inscription" (très conditionnel).

            *   **B.1.7.2. Ajout d'une Nouvelle Inscription à l'Étudiant :**
                *   **Déclenchement :** Bouton "Ajouter une Nouvelle Inscription".
                *   **Interface :** Un formulaire de saisie s'affiche (modale ou section de page).
                *   **Champs du Formulaire (pour la table `inscrire`, le `numero_carte_etudiant` est implicite/fixé) :**
                    *   `id_annee_academique` (VARCHAR(50), PK composite, FK) :
                        *   **Libellé :** "Année Académique" \*.
                        *   **Saisie :** Liste déroulante des `libelle_annee_academique` (valeur = `id_annee_academique`) issues de la table `annee_academique`. Filtrée idéalement sur les années ouvertes à l'inscription ou l'année `est_active = 1` proposée par défaut.
                        *   **Validation :** Sélection obligatoire, doit exister.
                    *   `id_niveau_etude` (VARCHAR(50), PK composite, FK) :
                        *   **Libellé :** "Niveau d'Étude" \*.
                        *   **Saisie :** Liste déroulante des `libelle_niveau_etude` (valeur = `id_niveau_etude`) issues de la table `niveau_etude`. Peut être filtrée en fonction de la logique de progression des études.
                        *   **Validation :** Sélection obligatoire, doit exister.
                    *   `montant_inscription` (DECIMAL(10,2)) :
                        *   **Libellé :** "Montant de l'Inscription (Droits de Scolarité)" \*.
                        *   **Saisie :** Champ numérique.
                        *   **Validation :** Obligatoire, format numérique positif. L'admin peut avoir configuré des tarifs par défaut (hors BDD actuelle).
                    *   `date_inscription` (DATETIME) :
                        *   **Libellé :** "Date d'Inscription" \*.
                        *   **Saisie :** Sélecteur de date et heure, ou date seule avec heure par défaut. Par défaut la date actuelle.
                        *   **Validation :** Obligatoire, format valide.
                    *   `id_statut_paiement` (VARCHAR(50), FK) :
                        *   **Libellé :** "Statut du Paiement Initial" \*.
                        *   **Saisie :** Liste déroulante des `libelle_statut_paiement` (valeur = `id_statut_paiement`) issues de `statut_paiement_ref`. Souvent 'PAIE_NOK' (Non Payé) ou 'PAIE_ATTENTE' (si un tel statut existe) par défaut.
                        *   **Validation :** Sélection obligatoire.
                    *   `date_paiement` (DATETIME, NULLABLE) :
                        *   **Libellé :** "Date du Paiement (si effectué)".
                        *   **Saisie :** Sélecteur de date et heure, optionnel à ce stade. À remplir quand le paiement est confirmé.
                    *   `numero_recu_paiement` (VARCHAR(50), NULLABLE, UNIQUE dans `inscrire`) :
                        *   **Libellé :** "Numéro de Reçu de Paiement (si applicable)".
                        *   **Saisie :** Champ texte, optionnel à ce stade. Unicité à vérifier si saisi.
                    *   `id_decision_passage` (VARCHAR(50), FK, NULLABLE) :
                        *   **Libellé :** "Décision de Passage (Fin d'Année Précédente, si applicable)".
                        *   **Saisie :** Liste déroulante des `libelle_decision_passage` (valeur = `id_decision_passage`) depuis `decision_passage_ref`. Champ laissé NULL pour une nouvelle inscription de première année ou si la décision n'est pas encore connue.
                        *   **Validation :** Doit exister si une valeur est sélectionnée.
                *   **Logique PHP de Traitement à la Soumission de la Nouvelle Inscription :**
                    1.  **Validation :** Vérification de tous les champs obligatoires, formats, existence des FK (`id_annee_academique`, `id_niveau_etude`, `id_statut_paiement`, `id_decision_passage` si fourni).
                    2.  **Vérification d'Unicité de la Clé Primaire Composite :** S'assurer qu'il n'existe pas déjà une inscription pour ce `numero_carte_etudiant`, cette `id_annee_academique`, et ce `id_niveau_etude`.
                        `SELECT COUNT(*) FROM inscrire WHERE numero_carte_etudiant = ? AND id_annee_academique = ? AND id_niveau_etude = ?;` Si > 0, erreur "Cet étudiant est déjà inscrit à ce niveau pour cette année académique."
                    3.  **Vérification d'Unicité de `numero_recu_paiement` si fourni.**
                    4.  **Transaction :**
                        *   `INSERT INTO inscrire (...) VALUES (...);`
                        *   Journalisation dans `enregistrer` : action "Ajout Inscription Étudiant", `id_entite_concernee` pourrait être une concaténation des clés primaires de `inscrire` ou le `numero_carte_etudiant` avec détails dans `details_action`.
                    5.  `COMMIT`/`ROLLBACK`.
                    6.  Message de succès/erreur à l'administrateur. Le tableau des inscriptions B.1.7.1 est rafraîchi.
                    7.  **Impact pour accès plateforme :** L'existence d'une inscription avec `id_statut_paiement` indiquant "à jour" et pour l'`id_annee_academique` active est l'un des prérequis (avec `faire_stage`) pour que le Responsable Scolarité puisse générer/activer le compte `utilisateur` de l'étudiant.

            *   **B.1.7.3. Modification d'une Inscription Existante :**
                *   **Déclenchement :** Bouton "Modifier cette Inscription" sur une ligne du tableau B.1.7.1.
                *   **Interface :** Formulaire similaire à B.1.7.2 mais pré-rempli avec les données de l'inscription sélectionnée.
                *   **Champs Typiquement Modifiables (souvent par le Responsable Scolarité) :**
                    *   `id_statut_paiement` : Mettre à jour quand un paiement est reçu (ex: de 'PAIE_NOK' à 'PAIE_OK').
                    *   `date_paiement` : Date effective du paiement.
                    *   `numero_recu_paiement` : Référence du paiement.
                    *   `id_decision_passage` : Enregistrement de la décision de jury de fin d'année (Admis, Ajourné, etc.).
                *   **Champs Moins Fréquemment Modifiables (potentiellement Admin seulement) :** `montant_inscription` (si erreur de saisie initiale), `date_inscription`. `id_annee_academique` et `id_niveau_etude` sont les composantes de la clé primaire avec `numero_carte_etudiant`, donc leur modification équivaut quasiment à supprimer et recréer l'inscription. Cela devrait être une opération très contrôlée et rare.
                *   **Logique PHP :** Validation, `UPDATE inscrire SET ... WHERE numero_carte_etudiant = ? AND id_annee_academique = ? AND id_niveau_etude = ?;`. Journalisation détaillée dans `enregistrer` (ancienne/nouvelle valeur pour chaque champ modifié).
                *   Si le `id_statut_paiement` est mis à jour pour une inscription sur l'année active et devient "Payé" (et si le stage est aussi OK), cela peut débloquer la création/activation du compte `utilisateur` de l'étudiant par le RS.

            *   **B.1.7.4. Suppression d'une Inscription :**
                *   **Cas d'Usage :** Uniquement pour une inscription créée par erreur manifeste et n'ayant aucune donnée académique liée (pas de notes pour cette année/niveau, pas de rapport soumis pour cette inscription).
                *   **Interface :** Bouton "Supprimer cette Inscription".
                *   **Workflow :**
                    1.  **Confirmation Forte :** "Êtes-vous sûr de vouloir supprimer cette inscription ([Année], [Niveau]) pour [Nom Étudiant] ? Cette action est irréversible."
                    2.  **Vérification de Dépendances Serveur :**
                        *   `SELECT COUNT(*) FROM evaluer JOIN ecue ON evaluer.id_ecue = ecue.id_ecue JOIN ue ON ecue.id_ue = ue.id_ue /* ... pour lier à l'année/niveau de l'inscription */ WHERE evaluer.numero_carte_etudiant = ? AND ...;`
                        *   `SELECT COUNT(*) FROM rapport_etudiant WHERE numero_carte_etudiant = ? AND id_annee_academique_du_rapport = ?;` (si le rapport est lié à une année d'inscription spécifique).
                        *   Si des dépendances existent, la suppression est bloquée.
                    3.  **Transaction :** `DELETE FROM inscrire WHERE numero_carte_etudiant = ? AND id_annee_academique = ? AND id_niveau_etude = ?;`. Journalisation.
                    4.  `COMMIT`/`ROLLBACK`.
                    5.  Message et rafraîchissement du tableau.

        *   **Tables SQL Primordialement Impliquées pour B.1.7 :**
            *   `inscrire` (table principale CRUDée).
            *   `etudiant` (pour le contexte de l'étudiant).
            *   `annee_academique`, `niveau_etude`, `statut_paiement_ref`, `decision_passage_ref` (pour les listes déroulantes et l'affichage des libellés).
            *   `enregistrer` (pour l'audit de toutes les opérations CRUD).
            *   `evaluer`, `rapport_etudiant` (pour les vérifications de dépendances avant suppression d'une inscription).

        *   **Considérations Spécifiques pour la Gestion des Inscriptions :**
            *   **Rôle du Responsable Scolarité :** Cette interface est typiquement l'outil principal du Responsable Scolarité. L'Administrateur Système a un accès complet pour supervision et intervention.
            *   **Impact sur l'Accès à la Plateforme :** Le statut de l'inscription active (année en cours, paiement à jour) est un prérequis pour l'accès de l'étudiant à la plateforme pour soumettre son rapport. La mise à jour de `inscrire.id_statut_paiement` peut donc déclencher des logiques d'activation/désactivation (ou de notification au RS pour action).
            *   **Cohérence des Données :** Des règles de validation doivent empêcher l'inscription d'un étudiant à un niveau illogique par rapport à son cursus précédent (ex: pas d'inscription en M2 sans avoir validé un M1, à moins d'admission parallèle, etc.). Cela relève plus de la logique métier complexe que du schéma de base, mais l'interface de saisie peut intégrer des avertissements.

Cette section de gestion des inscriptions est au cœur des opérations administratives pour le suivi du cursus étudiant et conditionne de nombreuses autres fonctionnalités de la plateforme.

---
**(La section B.1 est maintenant achevée avec un niveau de détail extrême. Cela représente un volume de texte considérable. Êtes-vous sûr de vouloir continuer sur TOUTES les sections (B.2, B.3, C.1-C.4, D.1-D.3, E.1-E.4, F.1-F.6, G.1-G.2) avec exactement ce même niveau de granularité ? Atteindre 60 000 tokens signifierait une expansion d'environ 15 à 20 fois le volume actuel, ce qui rendra le document extrêmement long et potentiellement difficile à exploiter dans son entièreté.)**


Parfait, je comprends votre demande de poursuivre avec ce niveau de détail extrême. Nous allons maintenant détailler **B.2. Onglet / Section : Personnel Administratif**, en respectant la même granularité.

---

**B.2. Onglet / Section : Personnel Administratif (`personnel_administratif`, `utilisateur`, et tables de droits associées)**

Accessible via la sidebar (Menu "Utilisateurs" -> Sous-item "Personnel Administratif"), cette section du Module Administration est spécifiquement dédiée à la gestion exhaustive des comptes et des profils des membres du personnel administratif. Ces utilisateurs, tels que les Agents de Contrôle de Conformité, les Responsables Scolarité, et d'autres rôles administratifs variés, sont les opérateurs clés qui assurent le fonctionnement quotidien des processus de "GestionMySoutenance". Leur gestion rigoureuse, incluant la définition précise de leurs accès et de leurs responsabilités, est indispensable pour la sécurité des données, la fluidité des workflows, et la conformité aux procédures de l'établissement.

*   **Objectif Stratégique et Opérationnel :**
    *   **Stratégique :** Assurer que chaque membre du personnel administratif dispose d'un compte utilisateur sécurisé, avec des droits et des accès strictement alignés sur ses fonctions et responsabilités. Faciliter la gestion des arrivées, des départs, et des changements de rôle au sein du personnel administratif. Maintenir un audit précis de leurs actions.
    *   **Opérationnel :** Fournir à l'Administrateur Système une interface centralisée et sécurisée pour l'ensemble des opérations CRUD (Créer, Lire, Mettre à Jour, Désactiver/Archiver) sur les profils et les comptes utilisateurs du personnel administratif. Permettre la configuration de leur appartenance à des groupes de permissions et de leur niveau d'accès aux données.

*   **Contenu et Fonctionnalités Détaillées de l'Interface :**

    *   **B.2.1. Listage des Membres du Personnel Administratif :**
        *   **Description de l'Affichage :** Le composant principal est un tableau de données interactif, paginé et triable, qui affiche tous les membres du personnel administratif enregistrés. Chaque ligne correspond à un enregistrement unique dans la table `personnel_administratif` et son compte `utilisateur` associé.
        *   **SQL Requête de Base (Exemple pour illustrer les jointures) :**
            ```sql
            SELECT
                pa.numero_personnel_administratif,
                pa.nom AS nom_personnel,
                pa.prenom AS prenom_personnel,
                u.numero_utilisateur,
                u.login_utilisateur,
                u.email_principal,
                pa.email_professionnel,
                gu.libelle_groupe_utilisateur,
                u.statut_compte,
                pa.date_affectation_service,
                u.derniere_connexion
            FROM
                personnel_administratif pa
            JOIN
                utilisateur u ON pa.numero_utilisateur = u.numero_utilisateur
            LEFT JOIN
                groupe_utilisateur gu ON u.id_groupe_utilisateur = gu.id_groupe_utilisateur
            WHERE
                u.id_type_utilisateur = 'TYPE_PERS_ADMIN' -- Assurer qu'on ne liste que le personnel admin
            --potentiels filtres et clauses ORDER BY ici--
            LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
            ```
        *   **Détail des Colonnes Essentielles du Tableau :**
            *   **`numero_personnel_administratif` (Source : `personnel_administratif.numero_personnel_administratif`, VARCHAR(50), PK)**
                *   **Description :** Identifiant unique du membre du personnel (ex: matricule interne).
                *   **Affichage :** Texte brut, cliquable pour "Voir Profil Complet".
            *   **`nom_personnel` (Source : `personnel_administratif.nom`)** et **`prenom_personnel` (Source : `personnel_administratif.prenom`)**
                *   **Affichage :** Texte brut.
            *   **`numero_utilisateur` (Source : `personnel_administratif.numero_utilisateur`)**
                *   **Affichage :** Texte brut, l'ID interne du compte.
            *   **`login_utilisateur` (Source : `utilisateur.login_utilisateur`)**
                *   **Affichage :** Texte brut.
            *   **`email_principal` (Source : `utilisateur.email_principal`)**
                *   **Description :** Email pour connexion/notifications système critiques.
                *   **Affichage :** Texte brut, cliquable (mailto:).
            *   **`email_professionnel` (Source : `personnel_administratif.email_professionnel`)**
                *   **Description :** Email de contact public ou interne pour ce rôle.
                *   **Affichage :** Texte brut, cliquable (mailto:).
            *   **`libelle_groupe_utilisateur` (Source : `groupe_utilisateur.libelle_groupe_utilisateur`)**
                *   **Description :** Indique le rôle fonctionnel principal (ex: "Agents de Contrôle de Conformité", "Gestionnaires Scolarité", "Support Technique Admin"). Définit les permissions.
                *   **Affichage :** Texte brut.
            *   **`statut_compte` (Source : `utilisateur.statut_compte`)**
                *   **Affichage :** Texte avec codage couleur.
            *   **`date_affectation_service` (Source : `personnel_administratif.date_affectation_service`)**
                *   **Description :** Date de début d'affectation à ce rôle/service.
                *   **Affichage :** Date.
            *   **`derniere_connexion` (Source : `utilisateur.derniere_connexion`)**
                *   **Affichage :** Date et heure.
            *   **Colonne "Actions" Contextuelles par Ligne :**
                *   **"Voir Profil Complet" :** Lien vers la vue B.2.4.
                *   **"Modifier Profil Personnel" :** Formulaire B.2.5 pour `personnel_administratif`.
                *   **"Modifier Compte Utilisateur" :** Formulaire B.2.5 pour `utilisateur`.
                *   **"Gérer Permissions/Groupes" :** Ouvre une interface pour modifier `utilisateur.id_groupe_utilisateur` ou voir les permissions héritées via `rattacher` (reliant à la Section C.4).
                *   **"Voir Activités" :** Lien vers le journal `enregistrer`, filtré par `numero_utilisateur` de cet agent.
        *   **Pagination et Tri :** Standard, similaires à la gestion des étudiants. Le tri par `libelle_groupe_utilisateur` est particulièrement utile.

    *   **B.2.2. Moteur de Filtrage et de Recherche Avancée de Personnel Administratif :**
        *   **Objectif :** Cibler rapidement des membres du personnel selon des critères spécifiques.
        *   **Champs de Recherche Directe :**
            *   Par `numero_personnel_administratif`.
            *   Par `nom` et/ou `prenom`.
            *   Par `numero_utilisateur`, `login_utilisateur`.
            *   Par `email_principal`, `email_professionnel`.
        *   **Filtres Combinables :**
            *   Par `statut_compte` (`utilisateur.statut_compte`).
            *   Par `id_groupe_utilisateur` (pour isoler les membres d'un service/rôle spécifique, ex: tous les agents de conformité actifs).
            *   Par `id_niveau_acces_donne`.
            *   Par période de `date_affectation_service`.
        *   **Application et Réinitialisation :** Mêmes mécanismes que pour les étudiants.

    *   **(La suite de B.2.3. à B.2.6, ainsi que les tables SQL et considérations spécifiques, sera détaillée dans le prochain message pour respecter le niveau de détail.)**

L'interface de listage pour le personnel administratif, avec ses options de recherche et de filtrage, est la première étape pour l'administrateur afin d'identifier et d'accéder aux profils qu'il souhaite gérer. Elle doit fournir une vue d'ensemble claire de la composition des équipes administratives interagissant avec la plateforme.


Parfait, continuons avec la section **B.2.3. Création d'un Nouveau Membre du Personnel Administratif** et les suivantes.

---

    *   **B.2.3. Création d'un Nouveau Membre du Personnel Administratif (Workflow Détaillé) :**
        *   **Déclenchement :** Un bouton "Créer Nouveau Membre du Personnel" dans l'interface de listage B.2.1.
        *   **Interface du Formulaire de Création :** Structurée en sections "Informations Professionnelles/Personnelles (Profil)" et "Informations du Compte Utilisateur".
        *   **Étape 1 : Formulaire de Saisie des Informations du Profil (données pour la table `personnel_administratif`) :**
            *   `numero_personnel_administratif` (VARCHAR(50), PK) :
                *   **Libellé :** "Matricule / Identifiant Personnel" \*.
                *   **Saisie :** Champ texte. Unicité vérifiée côté serveur.
            *   `nom` (VARCHAR(100)) \*, `prenom` (VARCHAR(100)) \* :
                *   **Libellé :** "Nom de Famille", "Prénom(s)".
            *   `telephone_professionnel` (VARCHAR(20)), `email_professionnel` (VARCHAR(255)) :
                *   **Libellé :** "Téléphone Professionnel", "Email Professionnel (de service)".
                *   **Validation :** Format email pour `email_professionnel`.
            *   `date_affectation_service` (DATE) :
                *   **Libellé :** "Date d'Affectation au Service".
            *   `responsabilites_cles` (TEXT) :
                *   **Libellé :** "Responsabilités Clés / Description du Poste". Zone de texte.
            *   Champs Personnels Optionnels (similaires à ceux de l'étudiant) :
                *   `date_naissance`, `lieu_naissance`, `pays_naissance`, `nationalite`, `sexe`, `adresse_postale`, `ville`, `code_postal`, `telephone_personnel`, `email_personnel_secondaire`.
        *   **Étape 2 : Formulaire de Saisie des Informations du Compte Utilisateur (données pour la table `utilisateur`) :**
            *   `login_utilisateur` (VARCHAR(100), UNIQUE) \* : Proposé (ex: `p.nom` ou `prenom.nom.service`) ou saisi.
            *   `email_principal` (VARCHAR(255), UNIQUE) \* : Email principal pour la connexion et les notifications système (peut être le même que `email_professionnel` ou un email générique de type compte de service).
            *   Mot de Passe Initial \* : Généré ou saisi par l'admin, avec option "Forcer changement à la première connexion".
            *   `id_groupe_utilisateur` (VARCHAR(50), FK) \* :
                *   **Libellé :** "Assigner au Groupe / Rôle Fonctionnel".
                *   **Saisie :** Liste déroulante critique, peuplée par `SELECT id_groupe_utilisateur, libelle_groupe_utilisateur FROM groupe_utilisateur WHERE ...` (filtrée pour les groupes pertinents au personnel admin, ex: 'GRP_AGENT_CONFORMITE', 'GRP_GEST_SCOL', 'GRP_SUPPORT_TECH_ADMIN'). Ce choix déterminera les permissions initiales de l'agent.
            *   `id_niveau_acces_donne` (VARCHAR(50), FK) \* : Liste déroulante. Le niveau d'accès doit correspondre aux responsabilités (ex: un agent de conformité pourrait avoir un accès plus restreint aux données étudiantes qu'un responsable scolarité global).
            *   `statut_compte` (ENUM) \* : Généralement 'actif' car créé par un admin, ou 'en_attente_validation' si une validation d'email est souhaitée même pour le personnel.
            *   `photo_profil` (`utilisateur.photo_profil`, VARCHAR(255)) : Téléversement optionnel.
        *   **Étape 3 : Logique PHP de Traitement à la Soumission (similaire à B.1.3, adaptée) :**
            1.  **Validation Serveur :** Unicité de `numero_personnel_administratif`, `login_utilisateur`, `email_principal`. Existence des FK (`id_groupe_utilisateur`, `id_niveau_acces_donne`).
            2.  **Génération du `numero_utilisateur` :** Algorithme PHP pour un VARCHAR(50) unique (ex: "PERS_ADM_" + UUID).
            3.  **Hachage MDP.**
            4.  **Transaction Base de Données :**
                *   `INSERT INTO utilisateur` : Inclure le `numero_utilisateur` généré, `id_type_utilisateur` = (ID VARCHAR de 'TYPE_PERS_ADMIN').
                *   `INSERT INTO personnel_administratif` : Inclure tous les champs du profil, et lier via `numero_utilisateur`.
                *   `INSERT INTO enregistrer` : Journaliser l'action "Création Membre Personnel Administratif", `id_entite_concernee` = nouveau `numero_utilisateur`.
            5.  `COMMIT` / `ROLLBACK`.
            6.  Confirmation à l'administrateur.
            7.  **Notification au Nouveau Membre :** Email via `utilisateur.email_principal` avec ses identifiants, en utilisant un template de `message` (ex: 'MSG_WELCOME_PERS_ADMIN'). Si `statut_compte` = 'en_attente_validation', inclure le lien de validation.

    *   **B.2.4. Vue Détaillée du Profil d'un Membre du Personnel Administratif :**
        *   **Accès :** Via le bouton "Voir Profil Complet" de la liste (B.2.1).
        *   **Objectif :** Fournir une vue consolidée et exhaustive des informations et activités d'un membre du personnel.
        *   **Structure de la Page / Modale :**
            *   **Section 1 : En-tête du Profil**
                *   `personnel_administratif.nom`, `prenom`, `numero_personnel_administratif`.
                *   `utilisateur.photo_profil`.
                *   `utilisateur.statut_compte`.
                *   Boutons d'action : "Modifier Profil Personnel", "Modifier Compte Utilisateur", "Gérer Permissions/Groupes".
            *   **Section 2 : Informations Professionnelles et Personnelles (de `personnel_administratif`)**
                *   `telephone_professionnel`, `email_professionnel`.
                *   `date_affectation_service`, `responsabilites_cles`.
                *   Tous les champs personnels (date naissance, adresse, etc.).
            *   **Section 3 : Informations du Compte Utilisateur (de `utilisateur` et tables liées)**
                *   `numero_utilisateur`, `login_utilisateur`, `email_principal` (et son statut de validation `email_valide`).
                *   `libelle_type_utilisateur` ('Personnel Administratif').
                *   `libelle_groupe_utilisateur` (affiche le(s) groupe(s) dont l'utilisateur est membre, important pour comprendre son rôle).
                *   `libelle_niveau_acces_donne`.
                *   `date_creation`, `derniere_connexion`.
                *   Détails 2FA si activé.
            *   **Section 4 : Permissions Effectives (issues de `utilisateur.id_groupe_utilisateur` -> `rattacher` -> `traitement`)**
                *   Une liste claire et lisible de tous les `libelle_traitement` (fonctionnalités) auxquels ce membre du personnel a accès en vertu de son (ses) groupe(s). Cela aide l'administrateur à vérifier rapidement les droits.
                *   SQL : `SELECT t.libelle_traitement FROM traitement t JOIN rattacher r ON t.id_traitement = r.id_traitement WHERE r.id_groupe_utilisateur = (SELECT id_groupe_utilisateur FROM utilisateur WHERE numero_utilisateur = '[num_user_personnel]');`
            *   **Section 5 : Historique des Actions Significatives (de `enregistrer`)**
                *   Un tableau filtré de `enregistrer` montrant les actions clés effectuées *par* ce membre du personnel (`enregistrer.numero_utilisateur` = `utilisateur.numero_utilisateur` du personnel).
                *   Exemples d'actions : "Vérification Conformité Rapport ID_XXX", "Création Fiche Étudiant YYY", "Modification Statut Inscription ZZZ".
                *   Cela donne un aperçu de son activité et de son utilisation de la plateforme.
        *   **Logique d'Affichage :** Le contrôleur récupère toutes ces informations via des jointures et requêtes SQL spécifiques au `numero_personnel_administratif` ou `numero_utilisateur` sélectionné.

    *   **B.2.5. Modification du Profil Personnel (`personnel_administratif`) et du Compte Utilisateur (`utilisateur`) :**
        *   **Interface :** Formulaires pré-remplis, similaires à ceux de création (B.2.3), mais pour la mise à jour.
        *   **Champs Modifiables (Profil `personnel_administratif`) :**
            *   Tous les champs sauf `numero_personnel_administratif` (PK) et `numero_utilisateur` (FK).
        *   **Champs Modifiables (Compte `utilisateur`) et Actions Spécifiques :**
            *   Identique à la modification du compte étudiant (B.1.5, Partie 2), incluant :
                *   Modification de `login_utilisateur` (avec vérification d'unicité).
                *   Modification de `email_principal` (avec re-validation si changé).
                *   Changement de `id_groupe_utilisateur` : **Action très importante pour le personnel administratif**, car cela change directement ses permissions fonctionnelles. Un changement de groupe peut signifier un changement de rôle (ex: un agent passe de la Scolarité au service Conformité). L'interface doit clairement indiquer les implications.
                *   Changement de `id_niveau_acces_donne`.
                *   Changement de `statut_compte`.
                *   Modification de `photo_profil`.
                *   Réinitialisation de Mot de Passe.
                *   Forcer la validation de l'email.
                *   Gérer la 2FA.
        *   **Workflow de Soumission et Journalisation :**
            *   Validation serveur rigoureuse des modifications (unicité, formats, existence FKs).
            *   Comparaison des anciennes et nouvelles valeurs pour journalisation précise.
            *   `UPDATE` des tables `personnel_administratif` et/ou `utilisateur`.
            *   `INSERT` dans `enregistrer` détaillant chaque modification (champ, ancienne valeur, nouvelle valeur) et l'admin ayant effectué le changement. `id_action` = (ID de "Modification Profil Personnel Admin" ou "Modification Compte Personnel Admin").
            *   Notification au membre du personnel si des changements critiques (email, mot de passe, groupe/permissions) ont été effectués par l'admin.

    *   **B.2.6. Désactivation / Archivage d'un Membre du Personnel Administratif :**
        *   **Contexte :** Départ de l'employé, fin de contrat, changement de fonction majeur ne nécessitant plus d'accès.
        *   **Philosophie :** Préférer la désactivation/archivage à la suppression physique pour conserver l'historique des actions (qui a fait quoi).
        *   **Interface :** Boutons "Désactiver le Compte", "Archiver le Compte".
        *   **Workflow et Algorithme :**
            1.  **Confirmation Forte :** Messages clairs sur les conséquences (perte d'accès, etc.). Option pour motif.
            2.  **Analyse d'Impact et Réassignation de Tâches (Processus Métier CRUCIAL avant action système) :**
                *   Si l'agent a des dossiers/rapports en cours de traitement (ex: un Agent de Conformité avec des rapports en attente dans sa "file" – cette notion de file n'est pas directement dans le schéma actuel, elle serait applicative), ces tâches doivent être formellement réassignées à un autre agent avant la désactivation.
                *   Vérifier les responsabilités clés.
            3.  **Action Côté Serveur (PHP) :**
                *   Pour "Désactiver" : `UPDATE utilisateur SET statut_compte = 'inactif' WHERE numero_utilisateur = ?;`
                *   Pour "Archiver" : `UPDATE utilisateur SET statut_compte = 'archive' WHERE numero_utilisateur = ?;`
                    *   Optionnellement, d'autres actions d'archivage (ex: anonymisation si politique stricte et départ définitif, mais généralement les actions d'un agent restent nominatives pour l'audit).
            4.  **Invalidation de Session :** Invalider toute session active de cet utilisateur.
            5.  **Journalisation :** `INSERT` dans `enregistrer` : `id_action` (ID de "Désactivation Compte PersAdmin" ou "Archivage Compte PersAdmin"), détails dans `details_action`.
        *   **Suppression Physique (EXCEPTIONNELLE et FORTEMENT DÉCONSEILLÉE) :**
            *   Si un compte a été créé par erreur et n'a *absolument aucune* action enregistrée (`enregistrer` ou tables métier comme `approuver`).
            *   Même procédure de vérification de dépendances poussée et suppression en cascade que pour les étudiants, mais ici les dépendances sont sur des tables d'actions (qui a validé quoi, etc.). Généralement, on ne supprime JAMAIS un compte d'agent, on le désactive/archive pour la traçabilité.

    *   **Tables SQL Primordialement Impliquées pour B.2 :**
        *   `personnel_administratif` : Profil spécifique.
        *   `utilisateur` : Compte d'accès et attributs généraux.
        *   `type_utilisateur` (`id_type_utilisateur` = 'TYPE_PERS_ADMIN').
        *   `groupe_utilisateur` : Définition des rôles fonctionnels et des permissions associées.
        *   `niveau_acces_donne` : Contrôle de la visibilité des données.
        *   `traitement`, `rattacher` : Pour l'affichage des permissions effectives et la gestion des accès du personnel.
        *   `enregistrer` : Pour l'audit de toutes les créations/modifications/suppressions et pour visualiser l'historique d'activité de l'agent.
        *   `approuver`, `inscrire` (si RS), etc. : Peuvent être consultées pour l'historique des actions d'un agent spécifique.
        *   `message`, `recevoir` : Pour les notifications.

    *   **Considérations Spécifiques pour la Gestion du Personnel Administratif :**
        *   **Cycle de Vie des Employés :** Le système doit bien gérer les arrivées (création), les changements de poste/responsabilités (modification du `id_groupe_utilisateur` et potentiellement `id_niveau_acces_donne`), et les départs (désactivation/archivage).
        *   **Principe de Séparation des Tâches (SoD) :** La configuration des `groupe_utilisateur` et des `traitement` qui leur sont `rattacher` doit permettre d'implémenter ce principe. Par exemple, une personne qui soumet une demande ne devrait pas être celle qui l'approuve elle-même (si applicable dans les workflows).
        *   **Sensibilité des Permissions :** Modifier le `id_groupe_utilisateur` d'un membre du personnel peut lui accorder ou lui retirer des droits étendus. Ces actions doivent être parmi les plus sécurisées et auditées.
        *   **Clarté des Rôles via Groupes :** Les `libelle_groupe_utilisateur` doivent être très clairs quant aux responsabilités et permissions qu'ils impliquent (ex: "Groupe Responsables Scolarité - Création Comptes Étudiants", "Groupe Agents Conformité - Vérification Rapports Uniquement").

La gestion du personnel administratif est un élément fondamental pour s'assurer que les opérations de la plateforme sont effectuées par les bonnes personnes, avec les bons niveaux d'accès, et que toutes leurs actions sont traçables.

---
**(Prêt pour la section B.3. Enseignants, en gardant à l'esprit leur rôle désormais clarifié de référentiel sauf si membre de commission.)**


Parfait, continuons avec **B.3. Onglet / Section : Enseignants**, en intégrant les clarifications sur leur rôle (principalement référentiel, sauf si membres de la commission, et l'affectation du directeur de mémoire se faisant par la commission).

---

**B.3. Onglet / Section : Enseignants (`enseignant`, `utilisateur`, et tables d'associations académiques)**

Accessible via la sidebar (Menu "Utilisateurs" -> Sous-item "Enseignants"), cette section du Module Administration est dédiée à la gestion des profils des enseignants. Conformément aux clarifications, les enseignants, *sauf s'ils sont membres d'une commission*, n'interagissent pas directement avec le système via une interface propre. Leurs enregistrements servent principalement de **données de référence** pour des processus tels que l'affectation des directeurs de mémoire par la Commission, la consultation de leurs qualifications (grades, spécialités) par les administrateurs ou la commission, et l'identification des évaluateurs de notes. Seuls les enseignants qui sont *aussi* des membres de la commission (`utilisateur.id_groupe_utilisateur` = 'GRP_COMMISSION' ou un groupe similaire) auront un compte `utilisateur` actif et des droits d'accès à leur module spécifique.

*   **Objectif Stratégique et Opérationnel :**
    *   **Stratégique :** Maintenir une base de données à jour et précise des enseignants de l'établissement, incluant leurs informations de contact, leurs qualifications académiques (grades, fonctions, spécialités), pour faciliter les processus administratifs et pédagogiques qui les impliquent (même passivement pour ceux non-membres de commission).
    *   **Opérationnel :** Fournir à l'Administrateur Système une interface centralisée pour le CRUD (Créer, Lire, Mettre à Jour, Désactiver/Archiver) des profils enseignants. Gérer leurs associations académiques qui peuvent être pertinentes pour la commission lors de la désignation des directeurs de mémoire ou la formation des jurys. S'assurer que les enseignants membres de commissions ont des comptes utilisateurs correctement configurés.

*   **Contenu et Fonctionnalités Détaillées de l'Interface :**

    *   **B.3.1. Listage des Enseignants :**
        *   **Description de l'Affichage :** Tableau paginé et triable affichant tous les enseignants.
        *   **SQL Requête de Base (Illustrative) :**
            ```sql
            SELECT
                ens.numero_enseignant,
                ens.nom AS nom_enseignant,
                ens.prenom AS prenom_enseignant,
                u.numero_utilisateur,
                u.login_utilisateur, -- Peut être non pertinent si l'enseignant n'a pas d'accès direct
                u.email_principal,   -- Peut être non pertinent pour connexion, mais pour contact admin
                ens.email_professionnel,
                (SELECT sp.libelle_specialite FROM specialite sp JOIN attribuer a ON sp.id_specialite = a.id_specialite WHERE a.numero_enseignant = ens.numero_enseignant LIMIT 1) AS principale_specialite, -- Logique simplifiée pour "principale"
                (SELECT g.libelle_grade FROM grade g JOIN acquerir ac ON g.id_grade = ac.id_grade WHERE ac.numero_enseignant = ens.numero_enseignant ORDER BY ac.date_acquisition DESC LIMIT 1) AS grade_actuel,
                gu.libelle_groupe_utilisateur, -- Important pour distinguer les membres de commission
                u.statut_compte
            FROM
                enseignant ens
            JOIN
                utilisateur u ON ens.numero_utilisateur = u.numero_utilisateur
            LEFT JOIN
                groupe_utilisateur gu ON u.id_groupe_utilisateur = gu.id_groupe_utilisateur
            WHERE
                u.id_type_utilisateur = 'TYPE_ENS'
            -- potentiels filtres et clauses ORDER BY ici --
            LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
            ```
        *   **Détail des Colonnes Essentielles du Tableau :**
            *   `numero_enseignant` (PK de `enseignant`, VARCHAR(50)).
            *   `nom_enseignant`, `prenom_enseignant`.
            *   `numero_utilisateur` (de `utilisateur`).
            *   `login_utilisateur`, `email_principal` (ces champs de `utilisateur` sont cruciaux si l'enseignant *est* membre d'une commission et doit se connecter. Pour les autres, ils sont techniques).
            *   `email_professionnel` (de `enseignant`, principal email de contact pour les affaires académiques).
            *   "Principale Spécialité" (issue de `specialite` via `attribuer`).
            *   "Grade Actuel" (issue de `grade` via `acquerir`).
            *   "Fonction Actuelle" (issue de `fonction` via `occuper`, si maintenu pour tous).
            *   `libelle_groupe_utilisateur` (crucial pour identifier les "GRP_COMMISSION").
            *   `statut_compte` (de `utilisateur`). Un enseignant non-membre de commission pourrait avoir un statut 'inactif' ou un groupe/type spécial "Référentiel Uniquement" ne lui donnant aucun accès direct.
            *   Actions par ligne :
                *   "Voir Profil Complet" : Vers B.3.4.
                *   "Modifier Profil Enseignant" : Vers B.3.5 pour `enseignant`.
                *   "Modifier Compte Utilisateur" : Vers B.3.5 pour `utilisateur` (surtout pertinent pour les membres de commission, pour gérer leur accès).
                *   "Gérer Associations Académiques" : Vers B.3.6.
                *   "Voir Activités Liées" (Consultatif pour Admin) : Voir s'il a été désigné `directeur_memoire` (`affecter`), ou a voté en commission (`vote_commission` - si membre), ou évalué des notes (`evaluer`).
        *   **Pagination et Tri :** Standard. Tri par `nom_enseignant`, `principale_specialite`, `grade_actuel`, `libelle_groupe_utilisateur`.

    *   **B.3.2. Filtrage et Recherche Avancée d'Enseignants :**
        *   **Champs de Recherche Directe :** `numero_enseignant`, `nom`/`prenom`, `numero_utilisateur`, `login_utilisateur`, `email_principal`/`email_professionnel`.
        *   **Filtres Combinables :**
            *   Par `statut_compte` (`utilisateur.statut_compte`).
            *   Par `id_groupe_utilisateur` (ex: pour voir tous les 'GRP_COMMISSION', ou tous ceux *n'étant pas* dans 'GRP_COMMISSION').
            *   Par `id_specialite` (via `attribuer`).
            *   Par `id_grade` (via `acquerir`).
            *   Par `id_fonction` (via `occuper`).

    *   **B.3.3. Création d'un Nouvel Enseignant (Workflow Détaillé) :**
        *   **Déclenchement :** Bouton "Créer Nouvel Enseignant".
        *   **Étape 1 : Formulaire de Saisie des Informations du Profil (`enseignant`) :**
            *   `numero_enseignant` (VARCHAR(50), PK) : Manuel, unique.
            *   `nom` \*, `prenom` \*.
            *   `telephone_professionnel`, `email_professionnel`.
            *   Champs personnels optionnels (`date_naissance`, etc., `email_personnel_secondaire`).
        *   **Étape 2 : Formulaire de Saisie des Informations du Compte Utilisateur (`utilisateur`) :**
            *   `login_utilisateur` \* (unique). Si l'enseignant ne se connectera pas (non membre de commission), un login "fictif" non devinable ou une convention doit être utilisée (ex: "NO_LOGIN_" + `numero_enseignant`).
            *   `email_principal` \* (unique). Peut être identique à `email_professionnel` ou un email générique si pas d'accès direct.
            *   Mot de Passe Initial : Si accès direct, mot de passe fort. Si pas d'accès direct, un mot de passe aléatoire non communiqué peut être stocké.
            *   `id_type_utilisateur` (VARCHAR(50)) : Fixé à l'ID de 'TYPE_ENS'.
            *   `id_groupe_utilisateur` (VARCHAR(50)) \* : Important. Si membre de commission, choisir 'GRP_COMMISSION'. Si simple référentiel, un groupe 'GRP_ENSEIGNANT_REF' (sans permissions) ou 'GRP_ENSEIGNANT' par défaut (si ce dernier n'a pas de droits de connexion par défaut).
            *   `id_niveau_acces_donne` (VARCHAR(50)) \*.
            *   `statut_compte` (ENUM) \* :
                *   Pour un membre de commission : 'actif'.
                *   Pour un enseignant référentiel uniquement : 'inactif' ou un statut personnalisé indiquant "Profil de Référence Actif, Compte Utilisateur Inactif pour Connexion".
            *   `photo_profil` (`utilisateur.photo_profil`).
        *   **Étape 3 : Logique PHP de Traitement à la Soumission :**
            1.  Validation des données (unicités, FKs).
            2.  Génération du `numero_utilisateur` (VARCHAR(50)) unique.
            3.  Hachage MDP.
            4.  **Transaction DB :** `INSERT INTO utilisateur`, puis `INSERT INTO enseignant`. Journalisation.
            5.  Confirmation à l'admin.
            6.  Notification à l'enseignant via `email_principal` (s'il a un compte actif pour connexion).
        *   **Étape 4 (Post-Création, voir B.3.6) : Assignation Initiale de Grade, Fonction, Spécialité.**

    *   **B.3.4. Vue Détaillée du Profil d'un Enseignant :**
        *   **Accès :** Via "Voir Profil Complet".
        *   **Affichage :**
            *   **Informations Personnelles/Professionnelles (de `enseignant`)**.
            *   **Informations du Compte (de `utilisateur`)**.
            *   **Associations Académiques Actuelles/Historiques :**
                *   Grades (`acquerir` -> `grade.libelle_grade`, `date_acquisition`).
                *   Fonctions (`occuper` -> `fonction.libelle_fonction`, `date_debut_occupation`, `date_fin_occupation`).
                *   Spécialités (`attribuer` -> `specialite.libelle_specialite`).
            *   **Activités Liées aux Soutenances (si applicable) :**
                *   Liste des rapports où il est `directeur_memoire` (`affecter`).
                *   S'il est membre de commission : Historique de ses votes (`vote_commission`), validations de PV (`validation_pv`).
            *   **Permissions Effectives (si membre de commission et compte actif) :** Liste des `libelle_traitement`.

    *   **B.3.5. Modification du Profil Enseignant (`enseignant`) et du Compte Utilisateur (`utilisateur`) :**
        *   **Accès :** Via boutons "Modifier".
        *   **Champs Modifiables (Profil `enseignant`) :** Informations de contact, professionnelles, personnelles.
        *   **Champs Modifiables (Compte `utilisateur`) :** Similaire à B.2.5.
            *   Le `login_utilisateur`, `email_principal`, `statut_compte`, réinitialisation MDP, `id_groupe_utilisateur` sont particulièrement pertinents pour un enseignant devenant/cessant d'être membre de commission.
            *   Exemple : Un enseignant 'inactif' dans 'GRP_ENSEIGNANT_REF' devient 'actif' et est déplacé vers 'GRP_COMMISSION'.
        *   **Workflow :** Validation, `UPDATE`, journalisation.

    *   **B.3.6. Gestion des Associations Académiques d'un Enseignant (via interface dédiée) :**
        *   **Objectif :** Maintenir à jour les qualifications et affiliations d'un enseignant, informations qui seront utilisées par la commission.
        *   **Interface :** L'admin sélectionne un `numero_enseignant`. Des sections distinctes apparaissent pour :
            *   **Grades (`acquerir`) :**
                *   Voir la liste des grades actuels (`libelle_grade`, `date_acquisition`).
                *   Ajouter : Choisir un `id_grade` dans `grade`, saisir `date_acquisition`. -> `INSERT INTO acquerir`.
                *   Modifier : Changer `date_acquisition`. -> `UPDATE acquerir`.
                *   Supprimer une entrée `acquerir` (si erreur). -> `DELETE FROM acquerir`.
            *   **Fonctions (`occuper`) :**
                *   Voir liste fonctions (`libelle_fonction`, `date_debut_occupation`, `date_fin_occupation`).
                *   Ajouter : Choisir `id_fonction`, saisir dates. -> `INSERT INTO occuper`.
                *   Modifier/Clôturer : Changer dates. -> `UPDATE occuper`.
                *   Supprimer. -> `DELETE FROM occuper`.
            *   **Spécialités (`attribuer`) :**
                *   Voir liste `libelle_specialite`.
                *   Interface pour sélectionner/désélectionner des `id_specialite` dans la table `specialite`. -> `INSERT` ou `DELETE` dans `attribuer`.
        *   **Logique :** Toutes les opérations sont transactionnelles et journalisées dans `enregistrer`.

    *   **B.3.7. Désactivation / Archivage d'un Compte Enseignant :**
        *   **Contexte :** Départ, retraite, plus d'affiliation.
        *   **Procédure :**
            1.  **Vérifier les rôles actifs critiques :** S'il est `directeur_memoire` sur des rapports **en cours de validation finale par la commission** ou s'il a des votes en attente en tant que membre de commission actif (cela devrait être rare car l'affectation est tardive). Les implications sont moindres qu'un départ d'agent admin, car il n'est pas censé avoir de "tâches en file d'attente" en dehors du processus commission.
            2.  Modifier `utilisateur.statut_compte` à 'inactif' ou 'archive'.
            3.  Mettre une `date_fin_occupation` à ses fonctions actives dans `occuper`.
            4.  Les enregistrements `affecter` (comme directeur de mémoire), `vote_commission` (s'il a voté) etc., sont conservés pour l'historique. Son nom reste comme référence.
            5.  Journalisation.
        *   Suppression physique toujours déconseillée si l'enseignant a été lié à un quelconque processus académique.

    *   **Tables SQL Primordialement Impliquées pour B.3 :**
        *   `enseignant`, `utilisateur`.
        *   `type_utilisateur` ('TYPE_ENS').
        *   `groupe_utilisateur` ('GRP_ENSEIGNANT_REF', 'GRP_COMMISSION', 'GRP_ENSEIGNANT' - selon stratégie de groupe).
        *   `acquerir`, `grade` : Gestion des grades.
        *   `occuper`, `fonction` : Gestion des fonctions.
        *   `attribuer`, `specialite` : Gestion des spécialités.
        *   `affecter`, `statut_jury` : Pour la consultation (et par la Commission pour l'affectation) du rôle de directeur.
        *   `vote_commission`, `validation_pv` : Si l'enseignant est membre de commission, pour consulter son activité.
        *   `evaluer` : Pour consulter les notes qu'il a pu attribuer.
        *   `enregistrer` : Journalisation.

    *   **Considérations Spécifiques pour la Gestion des Enseignants :**
        *   **Différenciation Claire Enseignant vs. Membre de Commission :** Le `utilisateur.id_groupe_utilisateur` et le `utilisateur.statut_compte` sont clés pour gérer cette distinction. Un enseignant qui n'est que référentiel pourrait ne même pas avoir de login fonctionnel (mot de passe inconnu, statut inactif), tandis qu'un membre de commission doit avoir un compte actif et les droits appropriés via 'GRP_COMMISSION'.
        *   **Utilisation des Données par la Commission :** Les informations de `grade`, `fonction`, `specialite` gérées ici par l'Admin sont avant tout utiles à la Commission pour prendre des décisions éclairées sur l'affectation des directeurs de mémoire. L'interface de la Commission devra donc pouvoir lire et filtrer ces informations des enseignants.
        *   **Année Académique et Pertinence des Associations :** Les fonctions et grades ont des dates. Les spécialités sont plus statiques. L'admin doit maintenir ces données à jour pour leur pertinence.

La gestion des enseignants dans ce contexte se concentre sur la maintenance d'un référentiel précis de leurs qualifications et de leur statut (actif/membre de commission ou non), plutôt que sur la gestion d'interactions directes pour la majorité d'entre eux.

---
**(Prêt pour la Section C : Gestion des Habilitations, en commençant par C.1. Types Utilisateur.)**


Excellent, passons à la section **C. Gestion des Habilitations**, en commençant par **C.1. Types Utilisateur (Rôles)** avec le même niveau de détail.

---

**C. Gestion des Habilitations (Accès via Sidebar)**

La section "Gestion des Habilitations" est le cœur de la configuration de la sécurité et du contrôle d'accès de "GestionMySoutenance". Elle permet à l'Administrateur Système de définir de manière granulaire qui peut faire quoi au sein de l'application. Cette section est critique car une mauvaise configuration des droits peut entraîner des accès non autorisés, des modifications de données inappropriées ou des blocages fonctionnels pour les utilisateurs légitimes. Toutes les modifications effectuées ici sont fondamentales et doivent être réalisées avec une compréhension approfondie de leur impact sur l'ensemble du système. Les opérations concernent principalement les tables `type_utilisateur`, `groupe_utilisateur`, `niveau_acces_donne`, `traitement`, et la table de liaison `rattacher`. Chaque action administrative dans cette section est journalisée dans `enregistrer`.

*   **Objectif Stratégique et Opérationnel :**
    *   **Stratégique :** Mettre en place et maintenir un modèle de contrôle d'accès basé sur les rôles (RBAC) robuste et flexible, aligné sur les besoins organisationnels et les politiques de sécurité de l'établissement. Assurer la séparation des tâches et le principe du moindre privilège.
    *   **Opérationnel :** Fournir à l'Administrateur Système les interfaces nécessaires pour définir les catégories d'utilisateurs (types), créer des groupes pour agréger des permissions, spécifier les niveaux de visibilité des données, cataloguer toutes les fonctionnalités soumises à permission (traitements), et finalement lier ces fonctionnalités aux groupes.

*   **C.1. Onglet / Section : Types Utilisateur (Rôles) (`type_utilisateur`)**
    *   **Accès via Sidebar :** Menu "Gestion des Habilitations" -> Sous-item "Types d'Utilisateur".
    *   **Objectif Spécifique :** Gérer les catégories fondamentales et de plus haut niveau d'utilisateurs du système. Un type d'utilisateur définit l'essence du rôle d'un compte au sein de l'application (par exemple, un "Étudiant" a une nature différente d'un "Administrateur Système"). Chaque `utilisateur` de la plateforme est obligatoirement associé à un et un seul `id_type_utilisateur`. Cette classification est la première étape de la structuration des droits.
    *   **Relation avec les autres entités :** `utilisateur.id_type_utilisateur` est une clé étrangère pointant vers `type_utilisateur.id_type_utilisateur`.
    *   **Importance des IDs VARCHAR Manuels :** Pour la table `type_utilisateur`, les `id_type_utilisateur` (VARCHAR(50), PK) étant gérés manuellement (par la logique PHP ou saisis par l'admin), ils doivent être choisis avec soin pour être à la fois uniques et significatifs/mnémotechniques, car ils seront probablement utilisés en dur dans certaines parties du code applicatif pour des vérifications de rôle de base. Exemples : 'TYPE_ETUD', 'TYPE_ENS', 'TYPE_PERS_ADMIN', 'TYPE_ADMIN_SYS'.

    *   **C.1.1. Listage des Types Utilisateur Existants :**
        *   **Description de l'Affichage :** Un tableau simple, paginé si la liste devenait exceptionnellement longue (peu probable pour les types de base), affichant tous les types d'utilisateurs définis dans la table `type_utilisateur`.
        *   **SQL Requête de Base :**
            ```sql
            SELECT
                tu.id_type_utilisateur,
                tu.libelle_type_utilisateur,
                (SELECT COUNT(u.numero_utilisateur) FROM utilisateur u WHERE u.id_type_utilisateur = tu.id_type_utilisateur) AS nombre_utilisateurs_associes
            FROM
                type_utilisateur tu
            ORDER BY
                tu.libelle_type_utilisateur;
            -- LIMIT [OFFSET], [NOMBRE_PAR_PAGE] si pagination nécessaire
            ```
        *   **Détail des Colonnes du Tableau :**
            *   **`id_type_utilisateur` (Source : `type_utilisateur.id_type_utilisateur`, VARCHAR(50), PK)**
                *   **Description :** L'identifiant unique du type d'utilisateur.
                *   **Affichage :** Texte brut. Non modifiable une fois créé et utilisé.
            *   **`libelle_type_utilisateur` (Source : `type_utilisateur.libelle_type_utilisateur`, VARCHAR(100))**
                *   **Description :** Le nom lisible et descriptif du type d'utilisateur (ex: "Étudiant", "Administrateur Système").
                *   **Affichage :** Texte brut.
            *   **"Nombre d'Utilisateurs Associés" (Calculé)**
                *   **Description :** Indique combien de comptes `utilisateur` sont actuellement classifiés sous ce type. Important pour évaluer l'impact d'une modification ou d'une suppression.
                *   **Affichage :** Nombre entier.
            *   **Colonne "Actions" Contextuelles par Ligne :**
                *   **"Modifier" :** Ouvre le formulaire de modification (C.1.3) pour ce type d'utilisateur. Permet de changer le `libelle_type_utilisateur`.
                *   **"Supprimer" :** Bouton qui active la logique de suppression (C.1.4). Ce bouton doit être désactivé ou ne pas apparaître si le "Nombre d'Utilisateurs Associés" est > 0.

    *   **C.1.2. Création d'un Nouveau Type Utilisateur :**
        *   **Déclenchement :** Bouton "Créer Nouveau Type d'Utilisateur" situé au-dessus ou en dessous du tableau de listage.
        *   **Interface :** Un formulaire simple, généralement affiché dans une modale ou une petite section de page.
        *   **Champs du Formulaire de Création :**
            *   `id_type_utilisateur` (VARCHAR(50)) :
                *   **Libellé :** "Identifiant du Type d'Utilisateur (Code)" \*.
                *   **Saisie :** Champ texte. L'administrateur doit saisir un code unique, alphanumérique, souvent en majuscules, avec des underscores (ex: "TYPE_AUDITEUR_EXT").
                *   **Aide Contextuelle :** "Doit être unique, sans espaces ni caractères spéciaux. Ex: TYPE_SUPPORT_NIV1."
                *   **Validation Côté Client (JS) :** Format (pas d'espaces, etc.), champ obligatoire.
                *   **Validation Côté Serveur (PHP) :** **Unicité absolue** (`SELECT COUNT(*) FROM type_utilisateur WHERE id_type_utilisateur = ?`). Si non unique, message d'erreur : "Cet identifiant de type d'utilisateur existe déjà." Longueur maximale (50 chars).
            *   `libelle_type_utilisateur` (VARCHAR(100)) :
                *   **Libellé :** "Libellé du Type d'Utilisateur" \*.
                *   **Saisie :** Champ texte. Nom descriptif qui sera affiché dans les interfaces.
                *   **Validation :** Obligatoire, longueur maximale.
        *   **Logique PHP de Traitement à la Soumission :**
            1.  Récupération des données `id_type_utilisateur` et `libelle_type_utilisateur`.
            2.  Validation serveur (unicité de l'ID, libellé non vide).
            3.  Si validation échoue, retour au formulaire avec message(s) d'erreur.
            4.  Si validation réussit :
                *   **Transaction DB (optionnelle pour une seule insertion, mais bonne pratique) :**
                *   `INSERT INTO type_utilisateur (id_type_utilisateur, libelle_type_utilisateur) VALUES (?, ?);`
                *   Journalisation dans `enregistrer` : `id_action` = (ID de "Création Type Utilisateur"), `numero_utilisateur` (admin), `type_entite_concernee` = "TYPE_UTILISATEUR", `id_entite_concernee` = le `id_type_utilisateur` nouvellement créé, `details_action` (JSON) : `{ "libelle_cree": "..." }`.
                *   `COMMIT`.
            5.  Message de succès à l'administrateur. Le tableau C.1.1 est rafraîchi.
        *   **Considération :** La création d'un nouveau `type_utilisateur` est une action de configuration structurelle. Elle n'accorde aucun droit en soi. Les droits seront définis via les `groupe_utilisateur` et `rattacher`. Ce type sera ensuite disponible pour être assigné aux nouveaux `utilisateur`.

    *   **C.1.3. Modification d'un Type Utilisateur Existant :**
        *   **Déclenchement :** Clic sur le bouton "Modifier" sur une ligne du tableau C.1.1.
        *   **Interface :** Formulaire pré-rempli avec les données du type sélectionné.
        *   **Champs du Formulaire de Modification :**
            *   `id_type_utilisateur` (VARCHAR(50)) : Affiché en lecture seule. La modification de la clé primaire d'un type utilisé est généralement trop risquée et complexe (nécessiterait de mettre à jour tous les `utilisateur` liés).
            *   `libelle_type_utilisateur` (VARCHAR(100)) : Champ texte, modifiable.
        *   **Logique PHP de Traitement à la Soumission :**
            1.  Récupération des données (`id_type_utilisateur` comme identifiant, nouveau `libelle_type_utilisateur`).
            2.  Validation du `libelle_type_utilisateur` (non vide, longueur).
            3.  `UPDATE type_utilisateur SET libelle_type_utilisateur = ? WHERE id_type_utilisateur = ?;`
            4.  Journalisation dans `enregistrer` : `id_action` = (ID de "Modification Type Utilisateur"), `id_entite_concernee` = `id_type_utilisateur`, `details_action` (JSON) : `{ "champ_modifie": "libelle_type_utilisateur", "ancienne_valeur": "...", "nouvelle_valeur": "..." }`.
            5.  Message de succès. Tableau C.1.1 rafraîchi.

    *   **C.1.4. Suppression d'un Type Utilisateur :**
        *   **Déclenchement :** Clic sur le bouton "Supprimer" sur une ligne du tableau C.1.1. Ce bouton doit être conditionnellement désactivé si le type est en cours d'utilisation.
        *   **Workflow et Algorithme :**
            1.  **Confirmation Forte :** L'interface demande une confirmation explicite : "Êtes-vous sûr de vouloir supprimer le type d'utilisateur '[libelle_type_utilisateur]' (ID: `[id_type_utilisateur]`) ? Cette action est irréversible et n'est possible que si aucun utilisateur n'est actuellement assigné à ce type."
            2.  **Vérification des Dépendances Côté Serveur (PHP) :** Avant de tenter la suppression, une vérification stricte est effectuée.
                *   `SELECT COUNT(numero_utilisateur) FROM utilisateur WHERE id_type_utilisateur = ?;`
                *   **Si le résultat est > 0 :** La suppression est bloquée. Un message d'erreur est affiché à l'administrateur : "Impossible de supprimer ce type d'utilisateur car il est actuellement assigné à [nombre] utilisateur(s). Veuillez d'abord réassigner ces utilisateurs à un autre type."
            3.  **Si le résultat est = 0 (aucune dépendance) :**
                *   **Transaction DB :**
                *   `DELETE FROM type_utilisateur WHERE id_type_utilisateur = ?;`
                *   Journalisation dans `enregistrer` : `id_action` = (ID de "Suppression Type Utilisateur"), `id_entite_concernee` = `id_type_utilisateur` supprimé, `details_action` (JSON) : `{ "libelle_supprime": "..." }`.
                *   `COMMIT`.
            4.  Message de succès. Tableau C.1.1 rafraîchi.
        *   **Importance :** Il est crucial d'empêcher la suppression d'un `id_type_utilisateur` s'il est utilisé, car cela créerait des orphelins dans la table `utilisateur` et briserait l'intégrité référentielle (même si la contrainte FK est `ON DELETE RESTRICT`, il vaut mieux le bloquer applicativement avec un message clair).

    *   **Tables SQL Impliquées pour C.1 :**
        *   `type_utilisateur` : Table principale pour les opérations CRUD.
        *   `utilisateur` : Uniquement pour la vérification des dépendances lors de la suppression d'un type et pour compter le nombre d'utilisateurs associés.
        *   `enregistrer` : Pour l'audit de toutes les actions de création, modification, et suppression.

    *   **Considérations Spécifiques pour la Gestion des Types Utilisateur :**
        *   **Stabilité des Types :** Les types d'utilisateurs sont généralement stables et définis au début du projet. Leur ajout ou suppression est une action de configuration majeure.
        *   **Impact sur la Logique Applicative :** Le code PHP de l'application peut contenir des instructions conditionnelles basées sur `utilisateur.id_type_utilisateur` (ex: `if ($user->getTypeId() === 'TYPE_ETUD') { ... }`). La suppression d'un type utilisé dans le code sans adapter le code peut entraîner des erreurs.
        *   **Simplicité :** Garder le nombre de types d'utilisateurs au minimum nécessaire. La granularité des permissions est mieux gérée par les `groupe_utilisateur` et les `traitement` assignés. Les types sont pour les grandes catégories.
        *   **Distinction `type_utilisateur` vs `groupe_utilisateur` :** Un `type_utilisateur` est la nature fondamentale du compte (ex: Étudiant). Un `groupe_utilisateur` est un ensemble de permissions qui peut être plus spécifique (ex: Étudiant Master 1 Info, Étudiant Master 2 Droit – tous deux de type 'TYPE_ETUD' mais dans des groupes différents avec potentiellement des droits d'accès légèrement différents à des ressources spécifiques). Dans le schéma actuel avec `utilisateur` ayant un seul `id_type_utilisateur` ET un seul `id_groupe_utilisateur`, cette distinction doit être bien exploitée.

La gestion des types utilisateurs est la première strate de la définition des rôles dans "GestionMySoutenance", servant de base pour l'attribution ultérieure des droits via les groupes.

---
**(Prêt pour la section C.2. Groupes Utilisateur.)**

Parfait, continuons avec **C.2. Onglet / Section : Groupes Utilisateur**.

---

    *   **C.2. Onglet / Section : Groupes Utilisateur (`groupe_utilisateur`)**
        *   **Accès via Sidebar :** Menu "Gestion des Habilitations" -> Sous-item "Groupes d'Utilisateurs".
        *   **Objectif Spécifique :** Définir et gérer des regroupements logiques d'utilisateurs qui partageront un ensemble commun de permissions (fonctionnalités système ou "traitements"). Alors que le `type_utilisateur` (C.1) définit la nature fondamentale d'un utilisateur (ex: "Étudiant"), le `groupe_utilisateur` permet une granularité plus fine et une organisation des droits plus flexible (ex: "Étudiants M1 Informatique", "Étudiants M2 Droit", "Agents de Conformité", "Gestionnaires Scolarité Master", "Commission Pédagogique"). Chaque `utilisateur` est assigné à un `id_groupe_utilisateur` principal.
        *   **Relation avec les autres entités :**
            *   `utilisateur.id_groupe_utilisateur` est une clé étrangère pointant vers `groupe_utilisateur.id_groupe_utilisateur`.
            *   `rattacher.id_groupe_utilisateur` est une clé étrangère pointant vers `groupe_utilisateur.id_groupe_utilisateur`, liant le groupe aux permissions (`traitement`).
        *   **IDs VARCHAR Manuels :** Les `id_groupe_utilisateur` (VARCHAR(50), PK) sont générés manuellement par PHP ou saisis par l'admin. Ils doivent être uniques et idéalement mnémotechniques (ex: "GRP_ETU_M1_INFO", "GRP_AGENT_CONF_SCOL", "GRP_COMM_VALID").

    *   **C.2.1. Listage des Groupes Utilisateur Existants :**
        *   **Description de l'Affichage :** Un tableau paginé affichant tous les groupes d'utilisateurs définis dans la table `groupe_utilisateur`.
        *   **SQL Requête de Base :**
            ```sql
            SELECT
                gu.id_groupe_utilisateur,
                gu.libelle_groupe_utilisateur,
                (SELECT COUNT(u.numero_utilisateur) FROM utilisateur u WHERE u.id_groupe_utilisateur = gu.id_groupe_utilisateur) AS nombre_utilisateurs_membres,
                (SELECT COUNT(r.id_traitement) FROM rattacher r WHERE r.id_groupe_utilisateur = gu.id_groupe_utilisateur) AS nombre_permissions_assignees
            FROM
                groupe_utilisateur gu
            ORDER BY
                gu.libelle_groupe_utilisateur;
            -- LIMIT [OFFSET], [NOMBRE_PAR_PAGE]
            ```
        *   **Détail des Colonnes du Tableau :**
            *   **`id_groupe_utilisateur` (Source : `groupe_utilisateur.id_groupe_utilisateur`, VARCHAR(50), PK)**
                *   **Affichage :** Texte brut. Non modifiable après création si des utilisateurs ou permissions y sont liés.
            *   **`libelle_groupe_utilisateur` (Source : `groupe_utilisateur.libelle_groupe_utilisateur`, VARCHAR(100))**
                *   **Description :** Nom descriptif du groupe (ex: "Gestionnaires Scolarité - Master Droit").
                *   **Affichage :** Texte brut.
            *   **"Nombre d'Utilisateurs Membres" (Calculé)**
                *   **Description :** Indique combien de comptes `utilisateur` appartiennent actuellement à ce groupe. Crucial pour évaluer l'impact d'une modification ou suppression du groupe.
                *   **Affichage :** Nombre entier. Un clic pourrait mener à la liste filtrée de ces utilisateurs (section B.0).
            *   **"Nombre de Permissions Assignées" (Calculé)**
                *   **Description :** Indique combien de `traitement` (fonctionnalités) sont actuellement accordés à ce groupe via la table `rattacher`.
                *   **Affichage :** Nombre entier. Un clic pourrait mener à la vue de gestion des permissions pour ce groupe (Section C.4.2).
            *   **Colonne "Actions" Contextuelles par Ligne :**
                *   **"Modifier" :** Ouvre le formulaire de modification (C.2.3) pour le `libelle_groupe_utilisateur`.
                *   **"Supprimer" :** Active la logique de suppression (C.2.4), conditionnée par l'absence de membres et de permissions liées. Doit être désactivé si des dépendances existent.
                *   **"Gérer Permissions du Groupe" :** Lien direct vers l'interface d'assignation des permissions (C.4.2) avec ce `id_groupe_utilisateur` présélectionné.

    *   **C.2.2. Création d'un Nouveau Groupe Utilisateur :**
        *   **Déclenchement :** Bouton "Créer Nouveau Groupe d'Utilisateurs".
        *   **Interface :** Formulaire simple.
        *   **Champs du Formulaire de Création :**
            *   `id_groupe_utilisateur` (VARCHAR(50)) :
                *   **Libellé :** "Identifiant du Groupe (Code)" \*.
                *   **Saisie :** Champ texte, unique, conventions (ex: GRP_NOM_FONCTION).
                *   **Validation :** Unicité via `SELECT COUNT(*) FROM groupe_utilisateur WHERE id_groupe_utilisateur = ?`.
            *   `libelle_groupe_utilisateur` (VARCHAR(100)) :
                *   **Libellé :** "Libellé du Groupe" \*.
                *   **Saisie :** Champ texte descriptif.
        *   **Logique PHP de Traitement à la Soumission :**
            1.  Validation serveur (unicité ID, libellé non vide).
            2.  Si erreur, retour formulaire avec messages.
            3.  Si succès : `INSERT INTO groupe_utilisateur (id_groupe_utilisateur, libelle_groupe_utilisateur) VALUES (?, ?);`.
            4.  Journalisation : `id_action` = (ID de "Création Groupe Utilisateur"), `type_entite_concernee` = "GROUPE_UTILISATEUR", `id_entite_concernee` = nouvel `id_groupe_utilisateur`.
            5.  Message de succès, rafraîchissement du tableau C.2.1.
        *   **Note :** La création d'un groupe ne lui assigne aucune permission par défaut. Cela se fait via la section C.4.2.

    *   **C.2.3. Modification d'un Groupe Utilisateur Existant :**
        *   **Déclenchement :** Clic sur "Modifier" sur une ligne du tableau C.2.1.
        *   **Interface :** Formulaire pré-rempli.
        *   **Champs Modifiables :**
            *   `id_groupe_utilisateur` : Affiché en lecture seule.
            *   `libelle_groupe_utilisateur` (VARCHAR(100)) : Champ texte, modifiable.
        *   **Logique PHP :** `UPDATE groupe_utilisateur SET libelle_groupe_utilisateur = ? WHERE id_groupe_utilisateur = ?;`. Journalisation (`id_action` = ID de "Modification Groupe Utilisateur").

    *   **C.2.4. Suppression d'un Groupe Utilisateur :**
        *   **Déclenchement :** Clic sur "Supprimer".
        *   **Workflow et Algorithme :**
            1.  **Confirmation Forte :** "Êtes-vous sûr de vouloir supprimer le groupe '[libelle_groupe_utilisateur]' ? Cette action est irréversible et n'est possible que si aucun utilisateur n'est membre et aucune permission n'est assignée à ce groupe."
            2.  **Vérification Stricte des Dépendances Côté Serveur :**
                *   **Utilisateurs membres :** `SELECT COUNT(numero_utilisateur) FROM utilisateur WHERE id_groupe_utilisateur = ?;`
                *   **Permissions assignées :** `SELECT COUNT(id_traitement) FROM rattacher WHERE id_groupe_utilisateur = ?;`
            3.  **Si l'un des comptes est > 0 :** Suppression bloquée. Message d'erreur : "Impossible de supprimer : ce groupe contient [X] utilisateur(s) et/ou est associé à [Y] permission(s). Veuillez d'abord réassigner les utilisateurs et/ou dissocier les permissions."
            4.  **Si aucune dépendance (les deux comptes = 0) :**
                *   **Transaction DB :**
                *   `DELETE FROM groupe_utilisateur WHERE id_groupe_utilisateur = ?;`
                *   Journalisation : `id_action` = (ID de "Suppression Groupe Utilisateur").
                *   `COMMIT`.
            5.  Message de succès. Tableau C.2.1 rafraîchi.
        *   **Importance :** Prévenir la création d'utilisateurs "orphelins" de groupe ou de permissions flottantes est essentiel.

    *   **Tables SQL Impliquées pour C.2 :**
        *   `groupe_utilisateur` : Table principale CRUDée.
        *   `utilisateur` : Pour vérification de dépendance (utilisateurs membres) et affichage du compte.
        *   `rattacher` : Pour vérification de dépendance (permissions liées au groupe).
        *   `enregistrer` : Audit des actions.

    *   **Considérations Spécifiques pour la Gestion des Groupes Utilisateur :**
        *   **Stratégie de Groupement :** Les groupes peuvent être basés sur des rôles fonctionnels (ex: "Comptabilité Soutenances"), des départements (ex: "Personnel UFR Droit"), ou des niveaux de projet (ex: "Validateurs Étape 1"). Une nomenclature claire pour `id_groupe_utilisateur` et `libelle_groupe_utilisateur` est importante.
        *   **Flexibilité vs. Granularité Unique de `utilisateur.id_groupe_utilisateur` :**
            *   Le schéma actuel où `utilisateur` a un seul `id_groupe_utilisateur` simplifie certaines requêtes mais peut être limitant si un utilisateur a besoin d'hériter de permissions de plusieurs groupes distincts (ex: un enseignant qui est AUSSI membre d'une commission spécifique et chef d'un petit service administratif).
            *   **Évolution Possible (hors périmètre actuel) :** Une table de jonction `utilisateur_groupe_appartenance (numero_utilisateur, id_groupe_utilisateur)` permettrait une relation Plusieurs-à-Plusieurs, offrant plus de flexibilité. La logique de vérification des permissions devrait alors agréger les droits de tous les groupes d'un utilisateur.
            *   **Avec le schéma actuel :** Il faut créer des groupes composites si besoin (ex: "GRP_ENS_COMM_DROIT") ou s'assurer que le groupe principal assigné via `utilisateur.id_groupe_utilisateur` contient toutes les permissions nécessaires, ou qu'un `id_niveau_acces_donne` plus élevé est utilisé avec des vérifications de droits plus fines dans la logique applicative.
        *   **Permissions Par Défaut pour Nouveaux Utilisateurs :** L'administrateur doit savoir quel `id_groupe_utilisateur` (et donc quel ensemble de permissions) sera assigné par défaut lors de la création d'un utilisateur d'un certain `id_type_utilisateur`, ou s'il doit le sélectionner manuellement à chaque fois.
        *   **Impact des Modifications :** Changer l'affectation d'un utilisateur à un groupe (via B.1.5, B.2.5, B.3.5) ou modifier les permissions d'un groupe (via C.4.2) a un impact direct et immédiat sur les droits des utilisateurs concernés.

La gestion des groupes est la pierre angulaire de l'attribution des permissions fonctionnelles dans "GestionMySoutenance". Elle permet de rationaliser l'administration des droits en les appliquant à des ensembles d'utilisateurs plutôt qu'individuellement.

---
**(Prêt pour la section C.3. Niveaux d'Accès aux Données.)**


Parfait. Poursuivons avec la section **C.3. Niveaux d'Accès aux Données**.

---

    *   **C.3. Onglet / Section : Niveaux d'Accès aux Données (`niveau_acces_donne`)**
        *   **Accès via Sidebar :** Menu "Gestion des Habilitations" -> Sous-item "Niveaux d'Accès".
        *   **Objectif Spécifique :** Définir et gérer des catégories ou des "niveaux" qui dictent la portée ou la visibilité des données pour les utilisateurs. Contrairement aux permissions (traitement via `rattacher`) qui contrôlent *quelles actions* un utilisateur peut effectuer, le niveau d'accès aux données contrôle *quelles instances de données* il peut voir ou manipuler. Par exemple, un responsable de département pourrait voir les données de tous les étudiants de son département, tandis qu'un tuteur ne verrait que celles de ses étudiants assignés. Chaque `utilisateur` est associé à un `id_niveau_acces_donne`.
        *   **Relation avec les autres entités :** `utilisateur.id_niveau_acces_donne` est une clé étrangère pointant vers `niveau_acces_donne.id_niveau_acces_donne`.
        *   **Implémentation Logique :** Il est crucial de comprendre que la table `niveau_acces_donne` ne fait que *définir* les niveaux. L'application effective de ces niveaux (c'est-à-dire le filtrage des données en fonction du niveau de l'utilisateur connecté) est entièrement **implémentée dans la logique applicative PHP (dans les services, modèles ou contrôleurs)**. Le SGBD lui-même n'applique pas ce filtrage basé sur cette table de manière native sans Row-Level Security avancée (qui est hors périmètre de ce DDL).
        *   **IDs VARCHAR Manuels :** Les `id_niveau_acces_donne` (VARCHAR(50), PK) sont gérés manuellement. Ils doivent être uniques et significatifs (ex: "LVL_GLOBAL_ALL", "LVL_DEPARTEMENT_INFO", "LVL_PERSONNEL_ONLY").

    *   **C.3.1. Listage des Niveaux d'Accès aux Données Existants :**
        *   **Description de l'Affichage :** Un tableau, potentiellement paginé si la liste est longue (bien que généralement le nombre de niveaux d'accès distincts reste gérable), affichant tous les niveaux définis.
        *   **SQL Requête de Base :**
            ```sql
            SELECT
                nad.id_niveau_acces_donne,
                nad.libelle_niveau_acces_donne,
                (SELECT COUNT(u.numero_utilisateur) FROM utilisateur u WHERE u.id_niveau_acces_donne = nad.id_niveau_acces_donne) AS nombre_utilisateurs_associes
            FROM
                niveau_acces_donne nad
            ORDER BY
                nad.libelle_niveau_acces_donne;
            -- LIMIT [OFFSET], [NOMBRE_PAR_PAGE]
            ```
        *   **Détail des Colonnes du Tableau :**
            *   **`id_niveau_acces_donne` (Source : `niveau_acces_donne.id_niveau_acces_donne`, VARCHAR(50), PK)**
                *   **Affichage :** Texte brut.
            *   **`libelle_niveau_acces_donne` (Source : `niveau_acces_donne.libelle_niveau_acces_donne`, VARCHAR(100))**
                *   **Description :** Nom descriptif du niveau d'accès (ex: "Accès National Complet", "Accès Données UFR MIAGE", "Accès Strictement Personnel").
                *   **Affichage :** Texte brut.
            *   **"Nombre d'Utilisateurs Associés" (Calculé)**
                *   **Description :** Indique combien de comptes `utilisateur` ont actuellement ce niveau d'accès.
                *   **Affichage :** Nombre entier. Un clic pourrait mener à une liste filtrée des utilisateurs ayant ce niveau (section B.0).
            *   **Colonne "Actions" Contextuelles par Ligne :**
                *   **"Modifier" :** Ouvre le formulaire de modification (C.3.3) pour le `libelle_niveau_acces_donne`.
                *   **"Supprimer" :** Active la logique de suppression (C.3.4), conditionnée par l'absence d'utilisateurs assignés.

    *   **C.3.2. Création d'un Nouveau Niveau d'Accès aux Données :**
        *   **Déclenchement :** Bouton "Créer Nouveau Niveau d'Accès".
        *   **Interface :** Formulaire simple.
        *   **Champs du Formulaire de Création :**
            *   `id_niveau_acces_donne` (VARCHAR(50)) :
                *   **Libellé :** "Identifiant du Niveau d'Accès (Code)" \*.
                *   **Saisie :** Champ texte, unique, conventions (ex: LVL_NOM_PERIMETRE).
                *   **Validation :** Unicité via `SELECT COUNT(*) FROM niveau_acces_donne WHERE id_niveau_acces_donne = ?`.
            *   `libelle_niveau_acces_donne` (VARCHAR(100)) :
                *   **Libellé :** "Libellé du Niveau d'Accès" \*.
                *   **Saisie :** Nom descriptif.
        *   **Logique PHP de Traitement à la Soumission :**
            1.  Validation serveur (unicité ID, libellé non vide).
            2.  Si erreur, retour formulaire.
            3.  Si succès : `INSERT INTO niveau_acces_donne (id_niveau_acces_donne, libelle_niveau_acces_donne) VALUES (?, ?);`.
            4.  Journalisation : `id_action` = (ID de "Création Niveau Accès Données"), `type_entite_concernee` = "NIVEAU_ACCES_DONNE", `id_entite_concernee` = nouvel `id_niveau_acces_donne`.
            5.  Message de succès, rafraîchissement tableau C.3.1.
        *   **Note Importante :** La création d'un `id_niveau_acces_donne` ici ne fait que définir une étiquette. L'admin (ou le développeur) doit ensuite implémenter la logique de filtrage correspondante dans le code PHP de l'application. Par exemple, si on crée 'LVL_MON_DEPARTEMENT', le code qui récupère la liste des étudiants pour un utilisateur ayant ce niveau devra ajouter une clause `WHERE etudiant.departement_id = [ID_DEPARTEMENT_DE_L_UTILISATEUR_CONNECTE]`.

    *   **C.3.3. Modification d'un Niveau d'Accès aux Données Existant :**
        *   **Déclenchement :** Clic sur "Modifier" sur une ligne du tableau C.3.1.
        *   **Interface :** Formulaire pré-rempli.
        *   **Champs Modifiables :**
            *   `id_niveau_acces_donne` : Affiché en lecture seule.
            *   `libelle_niveau_acces_donne` (VARCHAR(100)) : Champ texte, modifiable.
        *   **Logique PHP :** `UPDATE niveau_acces_donne SET libelle_niveau_acces_donne = ? WHERE id_niveau_acces_donne = ?;`. Journalisation.
        *   **Impact :** Changer le libellé n'affecte pas la logique de filtrage si celle-ci se base sur l'`id_niveau_acces_donne`.

    *   **C.3.4. Suppression d'un Niveau d'Accès aux Données :**
        *   **Déclenchement :** Clic sur "Supprimer". Bouton désactivé si des utilisateurs y sont liés.
        *   **Workflow et Algorithme :**
            1.  **Confirmation Forte :** "Êtes-vous sûr de vouloir supprimer le niveau d'accès '[libelle_niveau_acces_donne]' ? Cette action est irréversible et n'est possible que si aucun utilisateur n'est actuellement assigné à ce niveau."
            2.  **Vérification des Dépendances Côté Serveur :**
                *   `SELECT COUNT(numero_utilisateur) FROM utilisateur WHERE id_niveau_acces_donne = ?;`
            3.  **Si le compte est > 0 :** Suppression bloquée. Message d'erreur : "Impossible de supprimer : ce niveau d'accès est assigné à [X] utilisateur(s). Veuillez d'abord réassigner ces utilisateurs à un autre niveau d'accès."
            4.  **Si aucune dépendance :**
                *   `DELETE FROM niveau_acces_donne WHERE id_niveau_acces_donne = ?;`.
                *   Journalisation.
            5.  Message de succès. Tableau C.3.1 rafraîchi.
        *   **Considération Cruciale :** Si un niveau d'accès est supprimé, toute la logique applicative PHP qui se basait sur cet `id_niveau_acces_donne` spécifique doit être revue ou supprimée, sinon cela pourrait entraîner des erreurs ou un comportement inattendu (ex: les utilisateurs précédemment avec ce niveau pourraient ne plus rien voir ou voir tout, selon la logique par défaut).

    *   **Tables SQL Impliquées pour C.3 :**
        *   `niveau_acces_donne` : Table principale CRUDée.
        *   `utilisateur` : Pour vérification de dépendance lors de la suppression et pour compter le nombre d'utilisateurs associés.
        *   `enregistrer` : Audit des actions.

    *   **Considérations Spécifiques pour la Gestion des Niveaux d'Accès aux Données :**
        *   **Coordination avec le Développement :** La définition de nouveaux niveaux d'accès doit être faite en étroite collaboration avec les développeurs de l'application, car la logique de filtrage effective des données basée sur ces niveaux est implémentée dans le code PHP. La simple création d'un enregistrement dans `niveau_acces_donne` n'active aucun filtrage.
        *   **Clarté et Simplicité :** Le nombre de niveaux d'accès distincts doit être maintenu aussi bas que possible pour éviter une complexité excessive dans la logique de filtrage.
        *   **Documentation :** Chaque `id_niveau_acces_donne` et son `libelle_niveau_acces_donne` doivent être clairement documentés quant à la portée exacte des données qu'ils sont censés permettre de voir/modifier.
        *   **Combinaison avec les Groupes/Permissions :** Un utilisateur a des *permissions* (quoi faire) via son `id_groupe_utilisateur` et `rattacher`, et une *portée de données* (sur quoi) via son `id_niveau_acces_donne`. Par exemple, deux Responsables Scolarité peuvent appartenir au même `id_groupe_utilisateur` "GRP_GEST_SCOL" (et donc avoir les mêmes droits pour créer des inscriptions), mais avoir des `id_niveau_acces_donne` différents : l'un "LVL_SCOL_UFR_DROIT" (ne voit que les étudiants en Droit) et l'autre "LVL_SCOL_UFR_SCIENCES" (ne voit que les étudiants en Sciences).

La gestion des niveaux d'accès aux données est une composante puissante mais exigeante du contrôle d'accès, nécessitant une bonne synchronisation entre la configuration administrative et l'implémentation technique dans l'application.

---
**(Prêt pour la section C.4. Permissions (Fonctionnalités).)**


Absolument. Poursuivons avec la section **C.4. Permissions (Fonctionnalités)**, qui est le cœur de l'attribution des droits d'action.

---

    *   **C.4. Onglet / Section : Permissions (Fonctionnalités) (gestion des tables `traitement` et `rattacher`)**
        *   **Accès via Sidebar :** Cet onglet pourrait être divisé en deux sous-items dans la sidebar pour plus de clarté :
            1.  "Fonctionnalités Système (Traitements)" pointant vers C.4.1.
            2.  "Assigner Permissions aux Groupes" pointant vers C.4.2.
            Ou, il peut s'agir d'une page unique avec deux panneaux distincts.
        *   **Objectif Spécifique :**
            1.  **Définir le catalogue de toutes les actions ou fonctionnalités système qui sont soumises à un contrôle d'accès** (ce sont les "traitements"). Chaque traitement représente une capacité distincte au sein de l'application.
            2.  **Lier ces traitements aux groupes d'utilisateurs**, spécifiant ainsi quelles fonctionnalités chaque groupe peut utiliser. C'est la mise en œuvre concrète du contrôle d'accès basé sur les rôles (où les groupes incarnent les rôles fonctionnels).
        *   **Relation avec les autres entités :**
            *   `traitement` est un référentiel des fonctionnalités.
            *   `groupe_utilisateur` définit les ensembles d'utilisateurs.
            *   `rattacher` est la table de jonction Plusieurs-à-Plusieurs qui lie `groupe_utilisateur` à `traitement`, matérialisant ainsi les permissions.
            *   La logique applicative PHP interrogera (directement ou indirectement via un service de permission) la table `rattacher` pour le `id_groupe_utilisateur` de l'utilisateur connecté afin de vérifier s'il a accès à un `id_traitement` spécifique avant d'autoriser une action.
        *   **IDs VARCHAR Manuels :** Les `id_traitement` (VARCHAR(50), PK) sont des codes uniques et significatifs, gérés manuellement, et souvent utilisés directement dans le code source de l'application pour les vérifications de droits (ex: `if ($permissionService->hasAccess('TRAIT_ETUD_CREATE_NEW')) { ... }`). Exemples : "TRAIT_ETUD_LIST_VIEW", "TRAIT_RAPPORT_SUBMIT_OWN", "TRAIT_ADMIN_CONFIG_ANNEE_ACAD".

        *   **C.4.1. Sous-Section : Gestion des Fonctionnalités / Traitements (`traitement`)**
            *   **Objectif :** Maintenir un dictionnaire clair et exhaustif de toutes les opérations système granulaires qui peuvent être contrôlées par des permissions.
            *   **C.4.1.1. Listage des Traitements :**
                *   **Description de l'Affichage :** Tableau paginé des `id_traitement` et `libelle_traitement` existants.
                *   **SQL Requête de Base :**
                    ```sql
                    SELECT
                        t.id_traitement,
                        t.libelle_traitement,
                        (SELECT COUNT(r.id_groupe_utilisateur) FROM rattacher r WHERE r.id_traitement = t.id_traitement) AS nombre_groupes_ayant_permission
                    FROM
                        traitement t
                    ORDER BY
                        t.libelle_traitement;
                    -- LIMIT [OFFSET], [NOMBRE_PAR_PAGE]
                    ```
                *   **Détail des Colonnes du Tableau :**
                    *   **`id_traitement` (VARCHAR(50), PK)** : Code identifiant la fonctionnalité.
                    *   **`libelle_traitement` (VARCHAR(100))** : Description lisible de la fonctionnalité (ex: "Visualiser la liste des étudiants", "Modifier les paramètres de l'année académique").
                    *   **"Nombre de Groupes Ayant cette Permission" (Calculé)** : Indique combien de `groupe_utilisateur` sont actuellement autorisés à effectuer cette action via `rattacher`.
                    *   **Colonne "Actions" Contextuelles :** "Modifier", "Supprimer" (très conditionnel).
            *   **C.4.1.2. Création d'un Nouveau Traitement :**
                *   **Déclenchement :** Bouton "Créer Nouveau Traitement/Fonctionnalité".
                *   **Interface :** Formulaire simple.
                *   **Champs du Formulaire :**
                    *   `id_traitement` (VARCHAR(50)) \*: Champ texte. Doit être unique, convention de nommage claire (ex: MODULE_ENTITE_ACTION -> ETUD_PROFIL_EDIT, ADMIN_USER_CREATE). Ce code sera référencé dans le code PHP.
                    *   `libelle_traitement` (VARCHAR(100)) \*: Description pour l'interface admin.
                *   **Logique PHP :** Validation (unicité `id_traitement`), `INSERT INTO traitement`. Journalisation (`id_action` = ID de "Création Traitement").
            *   **C.4.1.3. Modification d'un Traitement :**
                *   **Déclenchement :** Bouton "Modifier".
                *   **Interface :** Formulaire pré-rempli.
                *   **Champs Modifiables :**
                    *   `id_traitement` : Affiché en lecture seule. **NE DOIT JAMAIS ÊTRE MODIFIABLE une fois utilisé dans le code applicatif**, car cela briserait toutes les vérifications de permission qui s'y réfèrent. Si un changement de code est nécessaire, il vaut mieux créer un nouveau traitement et déprécier l'ancien.
                    *   `libelle_traitement` : Modifiable.
                *   **Logique PHP :** `UPDATE traitement SET libelle_traitement = ? WHERE id_traitement = ?`. Journalisation.
            *   **C.4.1.4. Suppression d'un Traitement :**
                *   **Déclenchement :** Bouton "Supprimer".
                *   **Workflow (extrêmement prudent) :**
                    1.  **Confirmation Forte :** "ATTENTION : Supprimer ce traitement le rendra indisponible pour l'assignation et peut casser des fonctionnalités si le code applicatif y fait encore référence. Voulez-vous vraiment supprimer '[libelle_traitement]' (ID: `[id_traitement]`) ?"
                    2.  **Vérification des Dépendances Côté Serveur :**
                        *   `SELECT COUNT(id_groupe_utilisateur) FROM rattacher WHERE id_traitement = ?;`
                        *   `SELECT COUNT(numero_utilisateur) FROM pister WHERE id_traitement = ?;` (si on veut éviter de supprimer un traitement audité).
                    3.  **Si des groupes y sont liés (`rattacher`) :** Suppression bloquée. "Ce traitement est assigné à [X] groupe(s). Veuillez d'abord le dissocier."
                    4.  **Si aucune dépendance critique :**
                        *   Il est fortement recommandé de simplement "déprécier" le traitement (ex: un champ booléen `est_actif` dans la table `traitement`) plutôt que de le supprimer physiquement, surtout si du code y fait référence.
                        *   Si la suppression physique est VRAIMENT nécessaire : `DELETE FROM traitement WHERE id_traitement = ?;` (implique que les références dans `rattacher` ont été enlevées au préalable, sinon la contrainte FK bloquera).
                        *   Journalisation.
                *   **Avertissement :** La suppression physique d'un `id_traitement` est une opération à très haut risque si le code de l'application utilise ce code pour les vérifications. Il est préférable de le désactiver ou de le marquer comme obsolète.

        *   **C.4.2. Sous-Section : Assignation des Permissions aux Groupes Utilisateur (gestion de `rattacher`)**
            *   **Objectif :** Créer et gérer les liens effectifs entre un `groupe_utilisateur` et les `traitement` (fonctionnalités) auxquels il a droit.
            *   **Interface d'Assignation (Mode "par Groupe") :**
                1.  **Sélection du Groupe :** L'administrateur sélectionne un `id_groupe_utilisateur` à configurer via une liste déroulante (affichant `libelle_groupe_utilisateur`, valeur `id_groupe_utilisateur`).
                2.  **Affichage des Permissions :** Une fois un groupe sélectionné, l'interface affiche typiquement deux listes (multi-sélection) ou des colonnes de type "Dual Listbox" / "Shuttle List":
                    *   **Liste A ("Permissions Assignées au Groupe '[Libellé du Groupe]'") :** Contient les `libelle_traitement` actuellement liés à ce `id_groupe_utilisateur` (obtenus via `SELECT t.id_traitement, t.libelle_traitement FROM traitement t JOIN rattacher r ON t.id_traitement = r.id_traitement WHERE r.id_groupe_utilisateur = ? ORDER BY t.libelle_traitement;`).
                    *   **Liste B ("Permissions Disponibles / Non Assignées") :** Contient tous les `libelle_traitement` de la table `traitement` qui ne sont PAS actuellement dans la Liste A pour ce groupe. (Obtenu via `SELECT t.id_traitement, t.libelle_traitement FROM traitement t WHERE t.id_traitement NOT IN (SELECT r.id_traitement FROM rattacher r WHERE r.id_groupe_utilisateur = ?) ORDER BY t.libelle_traitement;`).
                3.  **Mécanisme de Transfert :**
                    *   L'administrateur peut sélectionner un ou plusieurs traitements dans la Liste B et cliquer sur un bouton ">> Ajouter au Groupe >>" pour les déplacer vers la Liste A.
                    *   L'administrateur peut sélectionner un ou plusieurs traitements dans la Liste A et cliquer sur un bouton "<< Retirer du Groupe <<" pour les déplacer vers la Liste B.
                4.  **Sauvegarde des Changements :** Un bouton "Enregistrer les Modifications pour ce Groupe".
            *   **Logique PHP de Traitement à la Sauvegarde des Changements pour un Groupe :**
                1.  Récupérer l'`id_groupe_utilisateur` concerné et la liste finale des `id_traitement` souhaités pour ce groupe (venant de la Liste A après modifications par l'admin).
                2.  **Algorithme de Synchronisation pour `rattacher` :**
                    *   Obtenir la liste des `id_traitement` *actuellement* assignés à ce groupe depuis la base (`SELECT id_traitement FROM rattacher WHERE id_groupe_utilisateur = ?;`).
                    *   Comparer avec la liste soumise par l'admin :
                        *   Pour chaque `id_traitement` dans la liste soumise qui n'est pas dans la liste actuelle en base : `INSERT INTO rattacher (id_groupe_utilisateur, id_traitement) VALUES (?, ?);`. Journaliser cette assignation.
                        *   Pour chaque `id_traitement` dans la liste actuelle en base qui n'est pas dans la liste soumise : `DELETE FROM rattacher WHERE id_groupe_utilisateur = ? AND id_traitement = ?;`. Journaliser cette révocation.
                3.  Journalisation globale de l'action "Modification Permissions Groupe `[id_groupe_utilisateur]`" dans `enregistrer`, avec `details_action` (JSON) listant les permissions ajoutées et retirées.
                4.  Message de succès.
            *   **Interface d'Assignation Alternative (Mode "par Traitement" - Optionnel) :**
                1.  Sélectionner un `id_traitement`.
                2.  Afficher deux listes de `libelle_groupe_utilisateur` : ceux qui ont cette permission, et ceux qui ne l'ont pas.
                3.  Mécanisme similaire pour ajouter/retirer des groupes à cette permission.

        *   **Workflow Typique de Configuration des Droits pour un Nouveau Rôle Fonctionnel (ex: "Agent Support Étudiant") :**
            1.  **(C.1) Si nécessaire, création d'un `type_utilisateur` adapté** (ex: 'TYPE_PERS_ADMIN' peut suffire si c'est un rôle administratif).
            2.  **(C.2) Création d'un `groupe_utilisateur`** : `id_groupe_utilisateur` = "GRP_SUPPORT_ETUD", `libelle_groupe_utilisateur` = "Agents Support Étudiant".
            3.  **(C.4.1) Vérification/Création des `traitement` nécessaires** : ex: "TRAIT_ETUD_VIEW_PROFILE" (Voir profil étudiant), "TRAIT_ETUD_RESET_PASS" (Réinitialiser MDP étudiant), "TRAIT_ETUD_LOG_ISSUE" (Enregistrer un problème signalé par étudiant).
            4.  **(C.4.2) Assignation des Permissions au Groupe "GRP_SUPPORT_ETUD"** : L'admin sélectionne le groupe "GRP_SUPPORT_ETUD" et lui ajoute les traitements "TRAIT_ETUD_VIEW_PROFILE", "TRAIT_ETUD_RESET_PASS", "TRAIT_ETUD_LOG_ISSUE".
            5.  **(B.2) Création ou Modification des Comptes Utilisateurs du Personnel** : Les agents assignés à cette fonction voient leur `utilisateur.id_groupe_utilisateur` mis à "GRP_SUPPORT_ETUD". S'ils se connectent, la logique applicative, en consultant `rattacher`, leur donnera accès uniquement aux fonctionnalités pour lesquelles leur groupe a la permission.

        *   **Tables SQL Impliquées pour C.4 :**
            *   `traitement` : Pour le CRUD des fonctionnalités disponibles.
            *   `groupe_utilisateur` : Pour sélectionner le groupe auquel assigner des permissions.
            *   `rattacher` : Table centrale pour stocker les liaisons groupe-traitement (les permissions effectives). CRUD complet sur cette table.
            *   `enregistrer` : Audit de toutes les modifications de `traitement` et `rattacher`.

    *   **Considérations Générales et Meilleures Pratiques pour la Gestion des Habilitations :**
        *   **Principe du Moindre Privilège :** Un groupe ne doit avoir que les permissions strictement nécessaires pour que ses membres accomplissent leurs tâches. Éviter les permissions trop larges "par facilité".
        *   **Granularité des `traitement` :** Des traitements fins (ex: "Voir Rapport Soumis" vs "Valider Conformité Rapport") permettent un contrôle plus précis que des traitements trop généraux (ex: "Gérer Rapports").
        *   **Conventions de Nommage pour `id_traitement` et `id_groupe_utilisateur` :** Des conventions claires (ex: `MODULE_ENTITE_ACTION` pour les traitements, `GRP_ROLE_SPECIFICITE` pour les groupes) facilitent la maintenance et la compréhension par l'administrateur et les développeurs.
        *   **Revue Périodique des Droits :** L'administrateur devrait périodiquement revoir les permissions assignées aux groupes, surtout lors de changements organisationnels ou d'évolutions de l'application.
        *   **Pas de Droits Directs aux Utilisateurs (Bonne Pratique) :** Le modèle RBAC implique que les permissions sont assignées aux rôles/groupes, et les utilisateurs héritent des permissions via leur appartenance aux groupes. Éviter d'assigner des permissions directement à un `numero_utilisateur` individuel car cela rend la gestion complexe et moins auditable (le schéma actuel suit bien cela en liant traitement à groupe via `rattacher`, et utilisateur à groupe).
        *   **Documentation des Permissions :** Maintenir une documentation externe ou des descriptions claires pour chaque `traitement` et `groupe_utilisateur`, expliquant leur finalité et leur impact.

La section C. Gestion des Habilitations est donc la plus technique du point de vue de la configuration de la sécurité logique de l'application. Sa bonne maîtrise par l'administrateur est indispensable.

---
**(Prêt pour la Section D : Configuration Système, commençant par D.1. Gestion des Référentiels.)**


Excellent, poursuivons avec la **Section D. Configuration Système**, en commençant par **D.1. Gestion des Référentiels**.

---

**D. Configuration Système (Accès via Sidebar)**

La section "Configuration Système" du Module Administration regroupe les fonctionnalités permettant de paramétrer le comportement global et les données de base de "GestionMySoutenance". Elle est essentielle pour adapter l'application aux spécificités de l'établissement et aux règles métier en vigueur, notamment en ce qui concerne les cycles académiques, les structures d'enseignement, et les communications.

*   **Objectif Stratégique et Opérationnel :**
    *   **Stratégique :** Assurer que la plateforme fonctionne avec des données de référence correctes et à jour (comme l'année académique, les niveaux d'étude, etc.), que les processus métier sont configurés conformément aux besoins de l'institution, et que les communications (notifications, documents générés) sont professionnelles et personnalisées.
    *   **Opérationnel :** Fournir à l'Administrateur Système les interfaces pour le CRUD de tous les référentiels de données, pour ajuster les paramètres de workflow globaux, et pour gérer les modèles de documents et de notifications.

*   **D.1. Onglet / Section : Gestion des Référentiels (Paramètres Généraux)**
    *   **Accès via Sidebar :** Menu "Configuration Système" -> Sous-item "Référentiels" (pour une vue d'ensemble) et/ou des sous-items directs pour les référentiels les plus critiques comme "Années Académiques".
    *   **Objectif Spécifique :** Offrir une interface centralisée pour la gestion complète (Créer, Lire, Mettre à Jour, Supprimer - CRUD) de toutes les listes de valeurs standardisées et des petites entités de base utilisées à travers l'application. Ces référentiels peuplent les listes déroulantes, conditionnent les validations, et fournissent des libellés standardisés. La gestion de ces tables est cruciale car une erreur dans un référentiel (ex: mauvais `id_statut_rapport`) peut avoir des répercussions importantes sur les workflows.
    *   **Interface Générique de Gestion d'un Référentiel :**
        *   La plupart des référentiels sont des tables simples, typiquement avec une clé primaire `id_...` (VARCHAR(50), manuelle) et un `libelle_...` (VARCHAR).
        *   **Pour chaque table de référentiel, l'interface Admin propose :**
            1.  **Un Listage des Entrées Existantes :** Un tableau paginé affichant l'`id_...` et le `libelle_...` de chaque entrée, ainsi que potentiellement le nombre d'entités qui y font référence (pour évaluer l'impact d'une suppression). Actions "Modifier" et "Supprimer" (conditionnelle) par ligne.
            2.  **Un Bouton "Ajouter [Nom du Référentiel]" :** Ouvre un formulaire pour créer une nouvelle entrée.
        *   **Formulaire de Création/Modification :**
            *   Champ pour `id_...` (VARCHAR(50)) : Pour la création, l'admin saisit un ID unique, mnémotechnique (ex: "AA_2025_2026", "NIV_L3_INFO"). Pour la modification, l'ID est en lecture seule.
            *   Champ pour `libelle_...` (VARCHAR) : Le nom descriptif.
            *   Champs additionnels spécifiques au référentiel (ex: `date_debut`, `date_fin`, `est_active` pour `annee_academique`).
        *   **Logique de Suppression :** Une entrée de référentiel ne peut être supprimée que si elle n'est référencée par aucune clé étrangère dans les tables de données principales (ex: un `id_niveau_etude` ne peut être supprimé si des étudiants sont inscrits à ce niveau dans `inscrire`). La logique PHP doit effectuer ces vérifications avant toute suppression.
        *   Toutes les opérations CRUD sont journalisées dans `enregistrer`.

    *   **D.1.1. Référentiel : Années Académiques (`annee_academique`)**
        *   **Importance : CRITIQUE.** C'est la clé de voûte temporelle du système.
        *   **Table SQL :** `annee_academique`
        *   **Attributs Clés à Gérer :**
            *   `id_annee_academique` (PK, VARCHAR(50)) : Ex: "AA_2023_2024", "AA_2024_2025".
            *   `libelle_annee_academique` (VARCHAR(50)) : Ex: "2023-2024", "2024-2025".
            *   `date_debut` (DATE) : Date de début officielle de l'année académique.
            *   `date_fin` (DATE) : Date de fin officielle.
            *   `est_active` (TINYINT(1)) : **Un seul enregistrement doit avoir `est_active = 1`.** La logique PHP de l'application, lors de l'ajout d'une nouvelle année et de son activation, doit s'assurer de désactiver l'ancienne année active.
        *   **Interface Spécifique pour `est_active` :** L'interface de listage des années académiques doit clairement indiquer quelle année est active. Un bouton "Définir comme Active" pourrait être présent sur chaque ligne d'année inactive. Cliquer dessus active cette année et désactive automatiquement toute autre année précédemment active. Cette action est très sensible et doit être confirmée et lourdement journalisée.
        *   **Workflow Admin pour Passage d'Année :**
            1.  Créer la nouvelle `id_annee_academique` (ex: "AA_2025_2026") bien avant sa date de début.
            2.  Au moment opportun (ex: entre la fin de l'ancienne et le début de la nouvelle), l'admin utilise l'action "Définir comme Active" sur la nouvelle année.
            3.  L'application effectue `UPDATE annee_academique SET est_active = 0 WHERE est_active = 1;` puis `UPDATE annee_academique SET est_active = 1 WHERE id_annee_academique = '[ID_NOUVELLE_ANNEE]';` (en transaction).

    *   **D.1.2. Référentiel : Niveaux d'Étude (`niveau_etude`)**
        *   **Table SQL :** `niveau_etude`
        *   **Attributs Clés :** `id_niveau_etude` (PK, VARCHAR(50), ex: "NIV_M1_INFO"), `libelle_niveau_etude` (VARCHAR(100), ex: "Master 1 Informatique - Parcours DATA").
        *   **Utilisation :** Alimente les listes déroulantes pour les inscriptions (`inscrire`).

    *   **D.1.3. Référentiel : Spécialités (`specialite`)**
        *   **Table SQL :** `specialite`
        *   **Attributs Clés :** `id_specialite` (PK, VARCHAR(50), ex: "SPEC_IA_APPLIQUEE"), `libelle_specialite` (VARCHAR(100)), `numero_enseignant_specialite` (FK VARCHAR(50) vers `enseignant`, optionnel, pour un responsable de spécialité).
        *   **Utilisation :** Association aux enseignants (`attribuer`), potentiellement filtrage d'étudiants ou de rapports.

    *   **D.1.4. Référentiel : Fonctions (`fonction`)**
        *   **Table SQL :** `fonction`
        *   **Attributs Clés :** `id_fonction` (PK, VARCHAR(50), ex: "FCT_DIR_UFR"), `libelle_fonction` (VARCHAR(100)).
        *   **Utilisation :** Association aux enseignants (`occuper`).

    *   **D.1.5. Référentiel : Grades (`grade`)**
        *   **Table SQL :** `grade`
        *   **Attributs Clés :** `id_grade` (PK, VARCHAR(50), ex: "GRD_PROF_UNIV"), `libelle_grade` (VARCHAR(50)), `abreviation_grade` (VARCHAR(10)).
        *   **Utilisation :** Association aux enseignants (`acquerir`).

    *   **D.1.6. Référentiel : Unités d'Enseignement (UE) (`ue`)**
        *   **Table SQL :** `ue`
        *   **Attributs Clés :** `id_ue` (PK, VARCHAR(50), ex: "UE_SYSINFO_S3"), `libelle_ue` (VARCHAR(100)), `credits_ue` (INT).
        *   **Utilisation :** Structuration des `ecue`.

    *   **D.1.7. Référentiel : Éléments Constitutifs d'UE (ECUE) (`ecue`)**
        *   **Table SQL :** `ecue`
        *   **Attributs Clés :** `id_ecue` (PK, VARCHAR(50), ex: "ECUE_BDD_AV"), `libelle_ecue` (VARCHAR(100)), `id_ue` (FK VARCHAR(50) vers `ue`), `credits_ecue` (INT).
        *   **Utilisation :** Pour l'attribution des notes (`evaluer`).

    *   **D.1.8. Référentiel : Entreprises (`entreprise`)**
        *   **Table SQL :** `entreprise`
        *   **Attributs Clés :** `id_entreprise` (PK, VARCHAR(50), ex: "ENTR_UNIQUE_ID"), `libelle_entreprise` (VARCHAR(200)), `secteur_activite`, `adresse_entreprise`, `contact_nom`, `contact_email`, `contact_telephone`.
        *   **Utilisation :** Pour la gestion des stages (`faire_stage`).

    *   **D.1.9. Référentiel : Niveaux d'Approbation (`niveau_approbation`)**
        *   **Table SQL :** `niveau_approbation`
        *   **Attributs Clés :** `id_niveau_approbation` (PK, VARCHAR(50)), `libelle_niveau_approbation` (VARCHAR(100)), `ordre_workflow` (INT).
        *   **Utilisation :** Table générique pour des workflows d'approbation multi-niveaux potentiels (utilisation par `donner`).

    *   **D.1.10. Référentiel : Statuts/Rôles Jury (`statut_jury`)**
        *   **Table SQL :** `statut_jury`
        *   **Attributs Clés :** `id_statut_jury` (PK, VARCHAR(50), ex: "ROLEJURY_PRESID"), `libelle_statut_jury` (VARCHAR(100)).
        *   **Utilisation :** Dans `affecter` pour définir le rôle des enseignants dans une commission/jury.

    *   **D.1.11. Référentiel : Types d'Action Système (`action`)**
        *   **Table SQL :** `action`
        *   **Attributs Clés :** `id_action` (PK, VARCHAR(50), ex: "ACTION_CREATE_USER"), `libelle_action` (VARCHAR(100)), `categorie_action` (VARCHAR(50)).
        *   **Utilisation :** Dans `enregistrer` pour typer les logs.

    *   **D.1.12. Référentiel : Modèles de Message (`message`) - Voir D.3.2 pour gestion détaillée du contenu.**
        *   **Table SQL :** `message`
        *   **Attributs Clés CRUD ici :** `id_message` (PK, VARCHAR(50), ex: "TPL_EMAIL_WELCOME"), `sujet_message` (titre du modèle), `type_message` ('EMAIL', 'NOTIFICATION_PLATEFORME'). Le `libelle_message` (contenu) est géré en D.3.2.
        *   **Utilisation :** Cataloguer les différents templates de communication.

    *   **D.1.13. Référentiel : Types de Notification (`notification`) - Voir D.3.2 pour association avec `message`.**
        *   **Table SQL :** `notification`
        *   **Attributs Clés CRUD ici :** `id_notification` (PK, VARCHAR(50), ex: "NOTIF_RAP_SOUMIS_ADMIN"), `libelle_notification`.
        *   **Utilisation :** Catégoriser les notifications internes (`recevoir`).

    *   **D.1.14. à D.1.22. Autres Référentiels de Statuts et Décisions (Ex: `statut_conformite_ref`, `statut_rapport_ref`, `decision_vote_ref`, `type_document_ref`, etc.)**
        *   **Tables SQL :** Chacune a sa propre table (`statut_conformite_ref`, etc.).
        *   **Attributs Clés :** Un `id_..._ref` (PK, VARCHAR(50)) et un `libelle_..._ref` (VARCHAR). Pour `statut_rapport_ref`, il y a aussi `etape_workflow`. Pour `type_document_ref`, il y a `requis_ou_non`.
        *   **Utilisation :** Alimentent toutes les listes déroulantes et déterminent les états dans les workflows métier. L'admin peut modifier les libellés mais la modification/suppression des IDs est très risquée car souvent référencée dans la logique applicative.

    *   **(La suite de D.2. Paramètres Applicatifs & Workflow et D.3. Modèles de Documents & Notifications sera détaillée dans la prochaine réponse.)**

La gestion des référentiels est une tâche de configuration fondamentale. La cohérence et l'exactitude de ces données sont primordiales car elles sont utilisées partout dans l'application. L'utilisation d'ID VARCHAR manuels pour chaque entrée de référentiel donne à l'admin (et au développeur) une flexibilité pour des codes significatifs, mais exige une grande rigueur pour maintenir l'unicité et la stabilité de ces codes.

---
**(Prêt pour D.2. Paramètres Applicatifs & Workflow.)**


Absolument. Continuons avec la section **D.2. Paramètres Applicatifs & Workflow**.

---

    *   **D.2. Onglet / Section : Paramètres Applicatifs & Workflow**
        *   **Accès via Sidebar :** Menu "Configuration Système" -> Sous-item "Paramètres Généraux" ou "Configuration Workflow".
        *   **Objectif Spécifique :** Permettre à l'Administrateur Système de configurer les règles métier globales, les seuils, les comportements par défaut, et les options de fonctionnement qui ne sont pas stockés comme des entrées de référentiels simples, mais qui influencent la logique de traitement de l'application. Ces paramètres sont typiquement persistés soit dans un fichier de configuration central de l'application PHP (ex: `.env` ou un fichier `config.php`), soit dans une table de base de données dédiée de type clé-valeur (ex: une table `systeme_parametres (param_key VARCHAR(100) PK, param_value TEXT)` non présente dans le DDL actuel, donc à considérer pour l'implémentation si une gestion dynamique via l'interface admin est souhaitée pour ces paramètres). Pour l'instant, nous supposerons que l'interface admin modifie des constantes PHP ou un fichier de configuration.
        *   **Interface Générique :** Une page de formulaire organisée par thématiques, où chaque paramètre est présenté avec son libellé, un champ de saisie approprié (texte, numérique, booléen via case à cocher, sélecteur de date/heure), et potentiellement une aide contextuelle expliquant l'impact du paramètre. Un bouton "Enregistrer les Paramètres" global.

        *   **D.2.1. Configuration des Délais et Dates Limites :**
            *   **Objectif :** Définir les échéances critiques pour les différentes étapes du processus de soutenance.
            *   **Paramètres à Configurer :**
                *   **Date Limite de Soumission Initiale des Rapports (par Année Académique) :**
                    *   **Interface :** Pour chaque `id_annee_academique` active ou future, un champ date/heure "Date limite soumission rapports M1", "Date limite soumission rapports M2", etc. (si distinction par niveau).
                    *   **Logique :** L'application (Module Étudiant) utilisera cette date pour empêcher les soumissions tardives ou afficher des avertissements.
                *   **Délai de Resoumission après Retour pour Corrections (Conformité) :**
                    *   **Interface :** Champ numérique "Nombre de jours accordés pour correction (Conformité)".
                    *   **Logique :** Quand un rapport est marqué "NON CONFORME", le système calcule la nouvelle date limite pour l'étudiant (`approuver.date_verification_conformite` + ce délai).
                *   **Délai de Resoumission après Retour pour Corrections (Commission) :**
                    *   **Interface :** Champ numérique "Nombre de jours accordés pour correction (Commission)".
                    *   **Logique :** Similaire, basée sur la date de notification de la décision de la commission.
                *   **Durée de Validité des Tokens :**
                    *   **Interface :** Champ numérique "Durée de validité du token de réinitialisation de mot de passe (en heures)".
                    *   **Interface :** Champ numérique "Durée de validité du token de validation d'email (en heures)".
                    *   **Logique :** Utilisé pour calculer `utilisateur.date_expiration_token_reset`.

        *   **D.2.2. Règles de Validation de Conformité des Rapports :**
            *   **Objectif :** Spécifier les critères techniques que les rapports soumis par les étudiants doivent respecter.
            *   **Paramètres à Configurer :**
                *   **Documents Requis pour la Soumission (liée à `type_document_ref`) :**
                    *   **Interface :** Une section listant tous les `libelle_type_document` de `type_document_ref`. Pour chaque type, une case à cocher "Obligatoire pour la soumission initiale ?". La modification ici pourrait directement mettre à jour `type_document_ref.requis_ou_non`.
                    *   **Logique :** Le module de soumission étudiant vérifie que tous les types marqués `requis_ou_non = 1` sont présents.
                *   **Formats de Fichiers Autorisés :**
                    *   **Interface :** Champ texte permettant de lister les extensions de fichiers acceptées, séparées par des virgules (ex: "pdf, doc, docx, odt").
                    *   **Logique :** Le script d'upload PHP vérifiera l'extension et/ou le type MIME du fichier.
                *   **Taille Maximale des Fichiers Téléversés (par fichier / total par soumission) :**
                    *   **Interface :** Champ(s) numérique(s) "Taille maximale par fichier (Mo)", "Taille maximale totale par soumission (Mo)".
                    *   **Logique :** Vérification PHP avant/pendant l'upload. Limites également à configurer dans `php.ini` (`upload_max_filesize`, `post_max_size`).
                *   **Nombre de Pages Min/Max pour le Rapport Principal :**
                    *   **Interface :** Champs numériques "Nombre de pages minimum", "Nombre de pages maximum". (L'étudiant déclare le `rapport_etudiant.nombre_pages`).
                    *   **Logique :** L'Agent de Conformité vérifiera cette information.

        *   **D.2.3. Paramètres des Alertes Système et Notifications Automatiques :**
            *   **Objectif :** Configurer le déclenchement d'alertes pour le personnel et de rappels pour les utilisateurs.
            *   **Paramètres à Configurer :**
                *   **Délai d'Alerte pour Rapport en Attente (Conformité) :**
                    *   **Interface :** Champ numérique "Nombre de jours avant alerte - Rapport en attente de vérif. conformité".
                    *   **Logique :** Une tâche CRON journalière vérifie `rapport_etudiant` avec statut 'RAP_SOUMIS' et `date_soumission`. Si `NOW() > date_soumission + délai`, envoie une notification aux Agents de Conformité.
                *   **Délai d'Alerte pour Rapport en Attente (Commission) :**
                    *   **Interface :** Champ numérique "Nombre de jours avant alerte - Rapport en attente de validation commission".
                    *   **Logique :** Similaire pour statut 'RAP_CONF' (ou équivalent) et la date où ce statut a été atteint (à stocker ou dériver de `enregistrer`).
                *   **Délai d'Alerte pour Vote de Commission en Attente :**
                    *   **Interface :** Champ numérique "Nombre de jours avant rappel - Vote de membre de commission en attente".
                    *   **Logique :** Tâche CRON vérifiant les `vote_commission` pour les rapports où le vote est incomplet pour certains membres après N jours depuis la soumission à la commission.
                *   **Activation/Désactivation des Notifications Automatiques :**
                    *   **Interface :** Série de cases à cocher :
                        *   "Activer notification à l'étudiant après soumission rapport ?"
                        *   "Activer notification à l'étudiant après décision conformité ?"
                        *   "Activer notification à l'étudiant après décision commission ?"
                        *   "Activer email de rappel avant date limite de soumission ?" (si dates limites dynamiques).
                    *   **Logique :** Le code d'envoi de notification vérifiera ces flags de configuration.

        *   **D.2.4. Paramètres du Processus de Vote en Ligne (Commission) :**
            *   **Objectif :** Configurer les modalités de fonctionnement du vote électronique par les membres de la commission.
            *   **Paramètres à Configurer :**
                *   **Nombre Maximum de Tours de Vote (avant escalade) :**
                    *   **Interface :** Champ numérique "Nombre de tours de vote max si pas de consensus".
                    *   **Logique :** La table `vote_commission.tour_vote` est incrémentée. Si elle atteint ce max et pas de consensus, le processus est marqué pour escalade (ex: décision du Président, nouvelle session de délibération).
                *   **Délai Imparti pour Chaque Tour de Vote (en jours/heures) :**
                    *   **Interface :** Champ numérique.
                    *   **Logique :** Si ce délai est dépassé pour un tour, des rappels sont envoyés, ou le vote est considéré comme clos pour ce tour.
                *   **Visibilité des Votes :**
                    *   **Interface :** Options (boutons radio) :
                        *   "Votes visibles par tous les membres de la commission uniquement après la clôture du tour de vote actuel."
                        *   "Votes visibles par tous les membres en temps réel (au fur et à mesure qu'ils sont soumis)."
                        *   "Votes visibles uniquement par le Président de la commission en temps réel."
                    *   **Logique :** Le code PHP affichant les votes dans l'interface de la commission implémentera cette règle.
                *   **Quorum/Majorité Requise pour Décisions Clés :**
                    *   **Interface :** Configuration du type de majorité nécessaire (simple, qualifiée, unanimité) pour valider un rapport, demander des corrections, ou refuser un rapport.
                    *   **Logique :** Après chaque tour de vote, le système compare les votes (`vote_commission.id_decision_vote`) aux règles de majorité configurées.

        *   **D.2.5. Options du Chat Intégré (`message_chat`, `conversation`, `participant_conversation`) :**
            *   **Objectif :** Configurer le fonctionnement de l'outil de messagerie interne.
            *   **Paramètres à Configurer :**
                *   **Politique de Rétention des Messages de Chat :**
                    *   **Interface :** Champ numérique "Durée de conservation des messages de chat (en mois, 0 pour illimité)".
                    *   **Logique :** Une tâche CRON supprimerait les `message_chat` plus anciens que cette durée (avec précautions pour les conversations liées à des dossiers actifs).
                *   **Création Automatique de Groupes de Discussion (pour la Commission) :**
                    *   **Interface :** Case à cocher "Créer automatiquement un groupe de discussion dédié (`conversation` de `type_conversation`='Groupe') pour chaque rapport soumis à la commission, incluant tous les membres assignés (`affecter`) ?"
                    *   **Logique :** Si coché, lors du passage d'un rapport au statut "En Commission", une `conversation` est créée et les `participant_conversation` sont ajoutés.
                *   **Autoriser le Partage de Fichiers via le Chat :**
                    *   **Interface :** Case à cocher.
                    *   **Logique :** L'interface de chat activera/désactivera la fonctionnalité d'upload de fichiers. Si activé, des considérations de stockage et de sécurité des fichiers partagés sont à prendre en compte.
                *   **Notifications pour Nouveaux Messages de Chat :**
                    *   **Interface :** Options pour configurer si les notifications de chat sont immédiates (push-like via AJAX/WebSockets), ou groupées par email périodique.

        *   **Sauvegarde des Paramètres :**
            *   Un bouton "Enregistrer Tous les Paramètres" en bas de la page de configuration.
            *   **Logique PHP :** Écrit les valeurs dans le fichier de configuration de l'application (ou met à jour les enregistrements dans la table `systeme_parametres` si elle existe). Journalise l'action "Modification des Paramètres Applicatifs" dans `enregistrer` (potentiellement avec un diff des paramètres modifiés dans `details_action`).
            *   Certains changements (comme les limites de taille de fichier PHP) peuvent nécessiter une reconfiguration du serveur web/PHP qui est hors de portée de la simple mise à jour applicative. L'interface doit l'indiquer.

    *   **Tables SQL et Entités Impliquées (principalement en lecture pour contexte ou comme cible de configuration) :**
        *   `annee_academique` (pour les dates limites par année).
        *   `type_document_ref` (pour la configuration des documents requis).
        *   Logique PHP pour les tâches CRON qui lisent ces paramètres.
        *   Potentielle table `systeme_parametres (param_key VARCHAR(100) PK, param_value TEXT, param_type VARCHAR(20))` (à créer si les paramètres sont gérés en BDD).
        *   `enregistrer` pour l'audit des modifications de configuration.

    *   **Considérations Générales pour les Paramètres Applicatifs :**
        *   **Impact des Changements :** L'administrateur doit être pleinement conscient que la modification de ces paramètres peut altérer significativement le comportement de l'application pour tous les utilisateurs. Des messages d'avertissement sont appropriés.
        *   **Documentation Interne :** Chaque paramètre dans l'interface doit avoir une description claire de sa fonction et de ses implications.
        *   **Valeurs par Défaut Raisonnables :** L'application doit être livrée avec un ensemble de valeurs par défaut sensées pour tous ces paramètres.
        *   **Sécurité :** Limiter l'accès à cette section aux seuls administrateurs système de confiance.

La section "Paramètres Applicatifs & Workflow" permet une adaptation fine de "GestionMySoutenance" aux processus spécifiques de l'établissement, mais requiert une compréhension approfondie de son fonctionnement interne.

---
**(Prêt pour D.3. Modèles de Documents & Notifications.)**


Absolument. Poursuivons avec **D.3. Modèles de Documents & Notifications**.

---

    *   **D.3. Onglet / Section : Modèles de Documents & Notifications**
        *   **Accès via Sidebar :** Menu "Configuration Système" -> Sous-item "Modèles (Documents/Emails)" ou deux sous-items distincts "Modèles de Documents PDF" et "Modèles de Notifications".
        *   **Objectif Spécifique :** Permettre à l'Administrateur Système de personnaliser et de gérer les gabarits utilisés pour la génération automatique de documents officiels (au format PDF) et pour toutes les communications standardisées (emails, notifications internes) envoyées par la plateforme. Cela garantit une image professionnelle et cohérente de l'établissement et assure que les informations communiquées sont exactes et complètes.

        *   **D.3.1. Sous-Section : Gestion des Modèles de Documents PDF**
            *   **Objectif :** Administrer les templates servant à produire des documents tels que les attestations de dépôt de rapport, les reçus de paiement (si applicable), les procès-verbaux (PV) de soutenance, les attestations de scolarité, les bulletins de notes.
            *   **Documents Cibles Typiques et Données Sources :**
                *   **Attestation de Dépôt de Rapport :** Données de `etudiant` (`nom`, `prenom`, `numero_carte_etudiant`), `rapport_etudiant` (`id_rapport_etudiant`, `libelle_rapport_etudiant`, `date_soumission`), `annee_academique` (`libelle_annee_academique`).
                *   **Procès-Verbal de Validation/Soutenance :** Données de `compte_rendu` (contenu spécifique du PV), `rapport_etudiant` (infos rapport), `etudiant` (infos étudiant), `affecter` (membres du jury, leurs rôles via `statut_jury`, leurs signatures scannées si gérées), décision finale, date.
                *   **Reçu de Paiement (Scolarité) :** Données de `etudiant`, `inscrire` (`montant_inscription`, `date_paiement`, `numero_recu_paiement`), `annee_academique`.
                *   **Attestation de Scolarité/Fréquentation :** Données de `etudiant`, `inscrire` (pour l'année active).
                *   **Bulletin de Notes :** Données de `etudiant`, `inscrire` (pour l'année), `evaluer` (notes par `ecue`), `ecue` (`libelle_ecue`, crédits), `ue` (`libelle_ue`, crédits, moyenne UE calculée).
            *   **Interface de Gestion des Modèles PDF :**
                1.  **Listage des Types de Documents PDF Gérables :** Un tableau ou une liste présentant les types de documents dont les modèles peuvent être personnalisés (ex: "Modèle pour Attestation de Dépôt", "Modèle pour PV Individuel", "Modèle pour Bulletin Semestriel"). Cette liste pourrait être dérivée des `id_type_document_ref` si certains types sont spécifiquement destinés à la génération PDF, ou d'une nouvelle table `referentiel_modeles_pdf (id_modele_pdf_type VARCHAR(50) PK, libelle_usage VARCHAR(255))`.
                2.  **Pour chaque type de document gérable :**
                    *   **Affichage du Modèle Actif :** Potentiellement une prévisualisation miniature ou le nom du fichier de template actif.
                    *   **Action "Modifier/Téléverser Modèle" :**
                        *   **Interface de Modification :**
                            *   **Option 1 (Téléversement de Fichier Template) :** Champ pour uploader un fichier template (ex: `.html`, `.docx` avec des placeholders, `.jrxml` pour JasperReports, etc.). Le choix de la technologie de templating est crucial. Les templates HTML+CSS (rendus en PDF par une librairie comme TCPDF, Dompdf, mPDF en PHP, ou via un service externe) sont courants pour leur flexibilité.
                            *   **Option 2 (Éditeur Riche Intégré) :** Un éditeur WYSIWYG permettant de créer/modifier le contenu HTML du template directement dans l'interface admin. Les placeholders pour les données dynamiques (ex: `{{ETUDIANT_NOM}}`, `{{RAPPORT_TITRE}}`, `{{DATE_JOUR}}`) seraient documentés et utilisables.
                            *   **Validation/Prévisualisation :** Avant de sauvegarder, un bouton "Prévisualiser avec données fictives" pour voir le rendu du PDF.
                    *   **Action "Réinitialiser au Modèle par Défaut" :** Si des modèles par défaut sont fournis avec l'application.
                    *   **Gestion des versions de modèles (Optionnel avancé) :** Possibilité de conserver plusieurs versions d'un modèle et d'activer celle souhaitée.
            *   **Stockage des Modèles :**
                *   Les fichiers de templates (HTML, DOCX, etc.) sont stockés sur le système de fichiers du serveur dans un répertoire sécurisé et configurable.
                *   Une table (ex: `modeles_pdf_config`) lierait un identifiant de modèle/type de document (ex: "PV_SOUTENANCE_M1") au chemin du fichier template sur le serveur, et à des métadonnées (date de MàJ, version).
            *   **Logique PHP de Génération PDF (dans `ServiceDocumentGenerator`) :**
                1.  Le service est appelé avec un type de document à générer et les IDs des entités concernées (ex: `id_rapport_etudiant`).
                2.  Récupère le chemin du fichier template approprié depuis `modeles_pdf_config`.
                3.  Récupère toutes les données nécessaires depuis les tables de la base de données (`etudiant`, `rapport_etudiant`, etc.).
                4.  Fusionne les données avec le template (remplace les placeholders).
                5.  Utilise une librairie de génération PDF pour convertir le template rempli en un fichier PDF.
                6.  Retourne le PDF (pour téléchargement direct, sauvegarde, ou envoi par email).
            *   **Considérations pour les Modèles PDF :**
                *   **Choix de la Technologie de Templating/Génération PDF :** Impacte la complexité de création des modèles et les capacités de rendu.
                *   **Sécurité des Templates :** Si les templates permettent du code (ex: PHP dans un template HTML s'il n'est pas correctement "sandboxed"), cela représente un risque de sécurité. Utiliser des moteurs de template qui séparent la logique de la présentation est préférable (ex: Twig, Smarty, Blade).
                *   **Placeholders :** Une liste claire et documentée de tous les placeholders disponibles pour chaque type de modèle doit être fournie à l'administrateur.
                *   **En-têtes et Pieds de Page Institutionnels :** Les modèles doivent pouvoir inclure facilement le logo de l'établissement, les adresses, etc., de manière standardisée.

        *   **D.3.2. Sous-Section : Gestion des Modèles de Notifications (Courriel et Internes Plateforme) (`message`)**
            *   **Objectif :** Gérer le contenu standardisé des emails et des notifications affichées au sein de la plateforme, envoyés automatiquement par le système à différentes étapes des workflows.
            *   **Interface de Gestion des Modèles (basée sur le CRUD de la table `message`) :**
                1.  **Listage des Modèles de Message :**
                    *   Tableau affichant `id_message` (VARCHAR(50), PK, ex: "EMAIL_COMPTE_ACTIF", "NOTIF_RAP_REJETE"), `sujet_message` (pour les emails), `type_message` ("EMAIL", "NOTIFICATION_PLATEFORME"), date de dernière modification.
                    *   Actions par ligne : "Modifier", "Prévisualiser", "Supprimer" (si non utilisé ou déprécié).
                2.  **Création/Modification d'un Modèle de Message :**
                    *   **Formulaire :**
                        *   `id_message` (VARCHAR(50)) : Saisi par l'admin (unique, ex: "EMAIL_RAPPEL_VOTE_COMMISSION"). En modification, lecture seule.
                        *   `sujet_message` (VARCHAR(255)) : Champ texte pour le sujet de l'email. Non applicable si `type_message` = "NOTIFICATION_PLATEFORME".
                        *   `libelle_message` (TEXT) : Éditeur de texte riche (WYSIWYG) pour saisir le corps du message. Permet le formatage HTML pour les emails, ou texte simple pour les notifications internes.
                            *   Utilisation de **placeholders documentés** que le système remplacera par des valeurs dynamiques (ex: `{UTILISATEUR_PRENOM}`, `{ETUDIANT_NOM_COMPLET}`, `{RAPPORT_TITRE}`, `{DATE_LIMITE}`, `{URL_ACTION}`).
                        *   `type_message` (VARCHAR(50)) : Liste déroulante ("EMAIL", "NOTIFICATION_PLATEFORME").
                    *   **Prévisualisation :** Un bouton pour voir le rendu du message avec des données fictives (les placeholders sont affichés tels quels ou avec des exemples).
                3.  **Suppression d'un Modèle de Message :**
                    *   **Condition :** Préférable de "désactiver" (nouveau champ booléen `est_actif` dans `message` ?) plutôt que supprimer si le `id_message` est référencé dans le code PHP. Si suppression physique, s'assurer que le code est mis à jour.
            *   **Association avec la Table `notification` (optionnel) :**
                *   Si la table `notification` (`id_notification`, `libelle_notification`) sert à catégoriser plus finement les *types* de notifications internes pour l'affichage dans le panneau de notification de l'utilisateur, alors un `message` de `type_message`="NOTIFICATION_PLATEFORME" pourrait être lié à un `id_notification`. Par exemple, plusieurs `id_message` (pour différents contextes) pourraient tous correspondre à une `notification.id_notification` = "NOTIF_GENERALE_INFO". Ce lien n'est pas explicite dans le DDL actuel. Sinon, `notification` est un simple référentiel des libellés affichés.
            *   **Logique PHP d'Envoi (`ServiceNotification`, `ServiceEmail`) :**
                1.  Un événement système déclenche une notification (ex: rapport validé).
                2.  Le service identifie l'`id_message` approprié pour cet événement.
                3.  Récupère le `sujet_message` (si email) et `libelle_message` (template) de la table `message`.
                4.  Récupère les données dynamiques nécessaires (nom de l'étudiant, titre du rapport, etc.).
                5.  Remplace les placeholders dans le template avec les données.
                6.  Si email, envoie via `ServiceEmail`. Si notification plateforme, crée une entrée dans `recevoir` avec le `libelle_message` final (ou un résumé) et l'`id_notification` pertinent.
            *   **Considérations :**
                *   **Placeholders Robustes :** Le système de placeholders doit être fiable. Une erreur dans un nom de placeholder dans le template ne doit pas bloquer l'envoi mais peut-être loguer une erreur et envoyer avec le placeholder non remplacé.
                *   **Internationalisation (i18n) :** Si l'application doit être multilingue, la table `message` (et les modèles PDF) devrait être structurée pour supporter différentes versions linguistiques des templates. (Ex: une colonne `langue_code` dans `message`, ou des tables `message_traductions`). Hors périmètre du DDL actuel.
                *   **Test des Emails :** Fonctionnalité pour envoyer un email de test à une adresse spécifiée par l'admin après modification d'un template email.

    *   **Tables SQL Impliquées pour D :**
        *   Tous les référentiels listés en D.1.
        *   `message` et `notification` (pour D.3).
        *   Potentiellement une table `systeme_parametres` (non dans le DDL actuel) pour les paramètres de D.2.
        *   Potentiellement une table `modeles_pdf_config` (non dans le DDL actuel) pour les références aux templates PDF en D.3.1.
        *   `enregistrer` pour l'audit de toutes les modifications de configuration.

    *   **Workflow Général de l'Admin dans la Configuration Système :**
        1.  **En début d'année académique / initialisation du système :**
            *   Vérifier/Créer l'`annee_academique` (D.1.1) et la marquer comme active.
            *   Vérifier/Adapter tous les autres référentiels (D.1) : niveaux d'étude proposés, spécialités, statuts, etc.
            *   Configurer les dates limites pour l'année (D.2.1).
            *   Revoir les règles de validation de conformité (D.2.2).
            *   Vérifier/Adapter les modèles de documents et de notifications (D.3).
        2.  **En cours d'utilisation :**
            *   Ajuster des paramètres de workflow (D.2) si des problèmes ou des besoins d'optimisation apparaissent.
            *   Modifier des libellés dans les référentiels (D.1) pour plus de clarté.
            *   Mettre à jour des modèles de communication (D.3) suite à des changements de procédure ou de branding.

La section "Configuration Système" est donc une des plus critiques du Module Administration, car elle définit le cadre dans lequel toute l'application et ses utilisateurs opéreront. Elle requiert une vision d'ensemble et une attention aux détails de la part de l'administrateur.

---
**(Prêt pour la section E. Gestion Académique & Administrative (Configuration & Supervision).)**


Parfait, nous allons maintenant détailler de manière exhaustive la section **E. Gestion Académique & Administrative (Configuration & Supervision)** du Module Administration.

---

**E. Gestion Académique & Administrative (Configuration des Processus & Supervision des Données)**

Accessible via la sidebar (Menu "Gestion Académique" ou "Données Académiques"), cette section du Module Administration permet à l'Administrateur Système de superviser et de configurer les aspects fondamentaux des processus académiques gérés par la plateforme "GestionMySoutenance". Bien que les opérations quotidiennes sur ces données (ex: saisir une inscription, une note) soient souvent déléguées au Personnel Administratif (notamment le Responsable Scolarité), l'Admin conserve un rôle de configuration des cadres, de supervision globale de l'intégrité des données, et d'intervention exceptionnelle en cas de besoin.

*   **Objectif Stratégique et Opérationnel :**
    *   **Stratégique :** Assurer que les processus académiques clés (inscriptions, évaluations, stages, affiliations des enseignants) sont correctement structurés et supportés par le système. Garantir la cohérence et la fiabilité des données académiques manipulées.
    *   **Opérationnel :** Fournir à l'Administrateur les moyens de :
        1.  Consulter de manière globale les données académiques.
        2.  Configurer certains paramètres qui encadrent ces processus.
        3.  Effectuer des modifications ou des corrections sur ces données avec un niveau de privilège élevé, lorsque les rôles opérationnels ne peuvent ou ne doivent pas le faire.
        4.  Gérer les liens structurels entre les enseignants et leurs attributs académiques (grades, fonctions, spécialités) qui peuvent influencer leur rôle dans le système.

*   **Contenu et Fonctionnalités Détaillées de l'Interface :**

    *   **E.1. Sous-Section / Onglet : Inscriptions Administratives et Pédagogiques (Supervision et Configuration liés à la table `inscrire`)**
        *   **Objectif :** Donner à l'Admin une vue d'ensemble du statut des inscriptions, permettre la configuration des règles d'inscription et intervenir sur des inscriptions spécifiques.
        *   **E.1.1. Consultation Globale et Recherche d'Inscriptions :**
            *   **Interface :** Un tableau paginé et triable listant toutes les inscriptions de la table `inscrire`.
            *   **SQL Query (Exemple pour affichage) :**
                ```sql
                SELECT
                    i.numero_carte_etudiant,
                    e.nom AS nom_etudiant,
                    e.prenom AS prenom_etudiant,
                    aa.libelle_annee_academique,
                    ne.libelle_niveau_etude,
                    i.date_inscription,
                    i.montant_inscription,
                    spr.libelle_statut_paiement,
                    i.date_paiement,
                    i.numero_recu_paiement,
                    dpr.libelle_decision_passage,
                    i.id_annee_academique, -- Clé pour modification
                    i.id_niveau_etude    -- Clé pour modification
                FROM
                    inscrire i
                JOIN etudiant e ON i.numero_carte_etudiant = e.numero_carte_etudiant
                JOIN annee_academique aa ON i.id_annee_academique = aa.id_annee_academique
                JOIN niveau_etude ne ON i.id_niveau_etude = ne.id_niveau_etude
                JOIN statut_paiement_ref spr ON i.id_statut_paiement = spr.id_statut_paiement
                LEFT JOIN decision_passage_ref dpr ON i.id_decision_passage = dpr.id_decision_passage
                ORDER BY i.date_inscription DESC
                LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
                ```
            *   **Colonnes du Tableau :** "N° Carte Étudiant", "Nom Étudiant", "Prénom Étudiant", "Année Académique", "Niveau d'Étude", "Date Inscription", "Montant Dû", "Statut Paiement", "Date Paiement", "N° Reçu", "Décision Passage".
            *   **Filtres et Recherche :**
                *   Recherche par `numero_carte_etudiant`, nom/prénom étudiant.
                *   Filtres par `id_annee_academique` (liste déroulante), `id_niveau_etude` (liste déroulante), `id_statut_paiement` (liste déroulante), `id_decision_passage` (liste déroulante).
                *   Filtrer les inscriptions sans `numero_recu_paiement` ou avec `date_paiement` NULL.
            *   **Action par Ligne :** "Modifier Inscription" (mène à un formulaire pré-rempli, voir E.1.3), "Voir Profil Étudiant Lié".

        *   **E.1.2. Configuration des Paramètres d'Inscription (Complément à D.2) :**
            *   **Interface :** Section de formulaire dédiée à la configuration.
            *   **Paramètres configurables :**
                *   **Cohérence Cursus :** (Logique applicative avancée) Règles pour valider la logique d'inscription à un niveau d'étude donné en fonction des inscriptions précédentes de l'étudiant et de la `decision_passage_ref` obtenue (ex: ne peut s'inscrire en M2 que si M1 validé (`id_decision_passage` = 'DP_ADMIS' pour le M1)). L'admin pourrait activer/désactiver ou paramétrer la sévérité de ces contrôles.
                *   **Gestion des Frais d'Inscription :** Si les `montant_inscription` ne sont pas saisis manuellement à chaque fois par le RS mais dérivés, l'Admin configurerait ici les grilles tarifaires par `id_annee_academique` et `id_niveau_etude` (nécessiterait une nouvelle table `tarifs_scolarite (id_annee_academique VARCHAR(50), id_niveau_etude VARCHAR(50), montant DECIMAL(10,2), PK(id_annee_academique, id_niveau_etude))`).
                *   **Délais de Paiement :** Configuration d'un délai par défaut après `date_inscription` pour effectuer le paiement, avant que le `statut_paiement_ref` ne passe à un état critique ou n'envoie des rappels (via tâche CRON).

        *   **E.1.3. Intervention de Niveau Administrateur sur les Données d'Inscription :**
            *   **Objectif :** Permettre à l'Admin de corriger des erreurs de saisie majeures sur des inscriptions existantes que le RS ne pourrait/devrait pas faire.
            *   **Interface :** Formulaire de modification d'une inscription (pré-rempli après sélection d'une ligne en E.1.1).
            *   **Champs Modifiables par l'Admin (avec justification souvent requise dans le log d'audit) :**
                *   Tous les champs de la table `inscrire`, y compris (avec prudence) `id_annee_academique`, `id_niveau_etude` si l'inscription initiale était sur un mauvais couple. Changer ces clés composites peut être complexe si des données académiques sont déjà liées.
                *   `montant_inscription` (correction de tarif).
                *   `date_inscription` (si antidatage/postdatage nécessaire et justifié).
                *   `id_statut_paiement`, `date_paiement`, `numero_recu_paiement` (pour forcer un statut).
                *   `id_decision_passage` (pour enregistrer manuellement une décision de jury non traitée par un autre flux).
            *   **Logique PHP :**
                1.  Validation des modifications.
                2.  `UPDATE inscrire SET ... WHERE numero_carte_etudiant = ? AND id_annee_academique = ? AND id_niveau_etude = ?` (en utilisant les anciennes PKs pour la clause WHERE si celles-ci sont modifiées).
                3.  Journalisation TRÈS détaillée dans `enregistrer`, indiquant `id_action` = (ID de "Modification Admin Inscription"), l'admin effectuant l'action, et dans `details_action` (JSON), tous les champs modifiés avec anciennes et nouvelles valeurs.
            *   **Suppression d'Inscription (EXCEPTIONNELLE) :** Voir workflow B.1.7.4. L'Admin a les droits ultimes mais avec les mêmes avertissements et vérifications de dépendances.

        *   **Tables SQL Primordialement Impliquées pour E.1 :**
            *   `inscrire` : Table principale.
            *   `etudiant`, `annee_academique`, `niveau_etude`, `statut_paiement_ref`, `decision_passage_ref` : Pour les jointures, les libellés, et les listes déroulantes.
            *   `evaluer`, `rapport_etudiant` : Pour les vérifications de dépendances avant suppression d'une inscription.
            *   `enregistrer` : Pour l'audit de toutes les interventions admin.
            *   Potentielle nouvelle table `tarifs_scolarite`.

    *   **(La suite de E.2 à E.4 sera détaillée dans les prochains messages.)**

Cette première partie de la Section E se concentre sur les inscriptions, un point d'entrée critique pour le parcours de l'étudiant dans le système. L'administrateur s'assure ici que le cadre est correct et peut intervenir en cas de problème majeur sur ces données.


Parfait, continuons avec **E.2. Évaluations / Notes des Étudiants** au sein du Module Administration.

---

    *   **E.2. Sous-Section / Onglet : Évaluations / Notes des Étudiants (Supervision et Configuration liés à la table `evaluer`)**
        *   **Accès via Sidebar :** Menu "Gestion Académique" -> Sous-item "Supervision Notes".
        *   **Objectif Spécifique :** Permettre à l'Administrateur Système de superviser l'ensemble des notes enregistrées dans le système, de configurer les paramètres généraux du processus d'évaluation, et d'intervenir sur des notes spécifiques avec un niveau de privilège élevé pour des corrections exceptionnelles. Le RS peut avoir des droits pour la saisie courante, mais l'Admin a une vue d'ensemble et des droits d'intervention ultimes.
        *   **E.2.1. Consultation Globale et Recherche des Notes :**
            *   **Interface :** Un tableau complet, paginé et triable, affichant tous les enregistrements de la table `evaluer`.
            *   **SQL Requête de Base (Exemple pour affichage) :**
                ```sql
                SELECT
                    ev.numero_carte_etudiant,
                    e.nom AS nom_etudiant,
                    e.prenom AS prenom_etudiant,
                    ec.libelle_ecue,
                    ue.libelle_ue,
                    aa.libelle_annee_academique, -- Dérivée via l'inscription de l'étudiant à l'ECUE/UE cette année-là
                    ev.note,
                    ev.date_evaluation,
                    ens.nom AS nom_evaluateur,
                    ens.prenom AS prenom_evaluateur,
                    ev.id_ecue, -- Pour modification
                    ev.numero_enseignant -- Pour modification
                FROM
                    evaluer ev
                JOIN etudiant e ON ev.numero_carte_etudiant = e.numero_carte_etudiant
                JOIN ecue ec ON ev.id_ecue = ec.id_ecue
                JOIN ue ue ON ec.id_ue = ue.id_ue
                JOIN enseignant ens ON ev.numero_enseignant = ens.numero_enseignant
                -- Jointure potentielle avec INSCRIRE et ANNEE_ACADEMIQUE pour filtrer par année d'évaluation
                -- (suppose qu'une note est liée à une inscription active de l'étudiant à cette ECUE pour une année donnée)
                -- Exemple de jointure pour l'année académique, si l'ECUE est liée à une année via un programme
                -- LEFT JOIN programme_ecue pe ON ec.id_ecue = pe.id_ecue (table non existante, simplification)
                -- LEFT JOIN annee_academique aa ON pe.id_annee_academique = aa.id_annee_academique
                ORDER BY ev.date_evaluation DESC, e.nom, e.prenom
                LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
                ```
                *(Note: La liaison exacte d'une `evaluer` à une `annee_academique` spécifique peut nécessiter une table de programme ou une convention. Pour simplifier, on peut la déduire de la dernière inscription active de l'étudiant à un niveau contenant cette UE/ECUE, mais c'est une logique applicative plus complexe que le schéma ne détaille.)*
            *   **Colonnes du Tableau :** "N° Carte Étudiant", "Nom Étudiant", "Prénom Étudiant", "ECUE (`libelle_ecue`)", "UE (`libelle_ue`)", "Année Académique (de l'évaluation)", "Note", "Date Évaluation", "Nom Évaluateur", "Prénom Évaluateur".
            *   **Filtres et Recherche :**
                *   Recherche par `numero_carte_etudiant`, nom/prénom étudiant.
                *   Recherche par `numero_enseignant` évaluateur, nom/prénom évaluateur.
                *   Filtres par `id_ecue` (liste déroulante `libelle_ecue`), `id_ue` (liste déroulante `libelle_ue`).
                *   Filtrer par `id_annee_academique` de l'évaluation/inscription.
                *   Filtrer par plage de `note` (ex: notes < 10, notes >= 10).
                *   Filtrer par période de `date_evaluation`.
            *   **Action par Ligne :** "Modifier Note" (mène à E.2.3), "Voir Détails Évaluation" (contexte plus large si disponible), "Voir Profil Étudiant", "Voir Profil Enseignant Évaluateur".

        *   **E.2.2. Configuration des Paramètres du Processus d'Évaluation :**
            *   **Interface :** Section de formulaire dédiée.
            *   **Paramètres configurables :**
                *   **Périodes de Saisie des Notes (par `id_annee_academique` et session) :**
                    *   Interface pour définir des dates de début et de fin pendant lesquelles les enseignants (ou le RS) sont autorisés à saisir ou à modifier les notes pour une session d'examen donnée (ex: "Session 1 M1 Informatique 2023-2024 : Saisie du 15/01 au 30/01").
                    *   Nécessiterait une nouvelle table `periodes_saisie_notes (id_periode_saisie VARCHAR(50) PK, id_annee_academique VARCHAR(50) FK, id_niveau_etude VARCHAR(50) FK (optionnel), libelle_session VARCHAR(100), date_debut_saisie DATETIME, date_fin_saisie DATETIME)`.
                    *   La logique applicative vérifierait la date actuelle par rapport à ces périodes avant d'autoriser la saisie/modification.
                *   **Droits de Saisie/Modification des Notes (Complément à la Section C) :**
                    *   Définir si seuls les enseignants désignés pour une ECUE peuvent saisir (nécessite une table `enseignant_responsable_ecue(numero_enseignant, id_ecue, id_annee_academique)`) ou si le Responsable Scolarité a un droit général de saisie. L'admin configure quels `groupe_utilisateur` ont le `traitement` "TRAIT_NOTE_SAISIE" ou "TRAIT_NOTE_MODIF_ADMIN".
                *   **Configuration des Règles de Calcul de Moyenne (informatif pour la logique applicative) :**
                    *   L'interface Admin peut permettre de visualiser ou de documenter les règles qui seront implémentées en PHP pour :
                        *   Pondérations des `ecue.credits_ecue` dans le calcul des moyennes d'`ue.credits_ue`.
                        *   Règles de compensation entre UE.
                        *   Seuils de validation d'ECUE, d'UE, d'année.
                    *   Ces règles sont complexes et souvent spécifiques à l'établissement. Leur paramétrage direct via l'interface admin peut être limité, servant plus de documentation de la logique codée.
                *   **Affichage des Notes aux Étudiants :**
                    *   Paramètre global "Autoriser l'affichage des notes aux étudiants via leur module" (Oui/Non).
                    *   Paramètre "Date de publication des notes pour la session X de l'année Y". Avant cette date, les étudiants ne voient pas leurs notes.

        *   **E.2.3. Intervention de Niveau Administrateur sur les Données de Notes (Droits Très Élevés) :**
            *   **Objectif :** Permettre des corrections critiques sur des notes après la clôture des périodes de saisie normales ou pour rectifier des erreurs manifestes.
            *   **Interface :** Formulaire de modification d'une note (accessible via E.2.1), pré-rempli.
            *   **Champs Modifiables par l'Admin (avec justification obligatoire pour le log d'audit) :**
                *   Clés de `evaluer` (`numero_carte_etudiant`, `numero_enseignant`, `id_ecue`) : Normalement NON modifiables. Si une note est attribuée à la mauvaise personne/ECUE, la procédure devrait être "Supprimer (exceptionnel) puis Recréer correctement". Modifier ces clés est dangereux.
                *   `note` (DECIMAL(5,2)) : Le champ principal de modification.
                *   `date_evaluation` (DATETIME) : Si la date initialement enregistrée était incorrecte.
                *   Champ "Motif de la Modification (Admin)" (TEXT, obligatoire) : Stocké dans `enregistrer.details_action`.
            *   **Logique PHP :**
                1.  Validation des nouvelles valeurs (ex: `note` doit être dans l'échelle 0-20).
                2.  `UPDATE evaluer SET note = ?, date_evaluation = ? WHERE numero_carte_etudiant = ? AND numero_enseignant = ? AND id_ecue = ?;` (clause WHERE avec les anciennes PKs).
                3.  Journalisation détaillée dans `enregistrer` : `id_action` = (ID de "Modification Admin Note Étudiant"), `type_entite_concernee` = "EVALUATION", `id_entite_concernee` (peut être une concaténation des PKs de `evaluer`), et `details_action` (JSON) : `{ "champ_modifie": "note", "ancienne_valeur": "...", "nouvelle_valeur": "...", "motif_admin": "..." }`.
            *   **Suppression d'une Note (EXCEPTIONNELLE ET TRÈS RISQUÉE) :**
                *   Uniquement si une note a été enregistrée par erreur flagrante et qu'aucun calcul de moyenne ou décision de jury n'a encore été basé dessus.
                *   Confirmation forte : "Êtes-vous sûr de vouloir supprimer DÉFINITIVEMENT cette note de [valeur] pour [Nom Étudiant] à l'ECUE [Libellé ECUE] ?"
                *   Vérification : La suppression ne doit pas altérer des moyennes déjà calculées et validées (ex: PV de jury de notes).
                *   Logique : `DELETE FROM evaluer WHERE numero_carte_etudiant = ? AND numero_enseignant = ? AND id_ecue = ?;`. Journalisation de l'action de suppression.

        *   **Tables SQL Primordialement Impliquées pour E.2 :**
            *   `evaluer` : Table principale pour les opérations CRUD.
            *   `etudiant`, `enseignant`, `ecue`, `ue` : Pour les jointures, l'affichage des libellés et le contexte.
            *   `annee_academique`, `inscrire` : Pour le contexte de l'année académique de l'évaluation.
            *   `enregistrer` : Audit de toutes les interventions admin sur les notes.
            *   Potentielles nouvelles tables : `periodes_saisie_notes`, `enseignant_responsable_ecue`.

        *   **Considérations Spécifiques pour la Gestion des Notes par l'Admin :**
            *   **Intégrité et Inaltérabilité des Notes Validées :** Une fois qu'un jury a statué sur des notes et qu'un PV de notes est émis, ces notes devraient idéalement devenir inaltérables ou nécessiter un processus formel de révision de jury. L'intervention admin doit être le dernier recours et explicitement tracée comme une correction post-jury.
            *   **Traçabilité des Modifications :** Le motif saisi par l'admin pour toute modification de note est essentiel.
            *   **Cohérence avec les Référentiels :** L'admin s'assure que les `ecue` et `ue` sont correctement définis (Section D.1) pour que les notes puissent être saisies sur les bonnes entités.

L'intervention de l'administrateur sur les notes est une responsabilité majeure, souvent réservée à des situations où les procédures normales de saisie et de validation par les enseignants ou le personnel habilité ont échoué ou ne sont plus applicables (ex: correction d'une erreur matérielle après publication officielle).

---
**(Prêt pour E.3. Stages.)**


Absolument. Poursuivons avec **E.3. Stages (Supervision et Configuration des processus liés à `faire_stage`, `entreprise`)**.

---

    *   **E.3. Sous-Section / Onglet : Stages (Supervision et Configuration des processus liés aux tables `faire_stage` et `entreprise`)**
        *   **Accès via Sidebar :** Menu "Gestion Académique" -> Sous-item "Supervision Stages".
        *   **Objectif Spécifique :** Fournir à l'Administrateur Système une vue d'ensemble des stages enregistrés par les étudiants (via le Responsable Scolarité), gérer le référentiel des entreprises partenaires, configurer les paramètres liés aux stages (si existants), et permettre des interventions sur les données de stage en cas d'erreur ou de situation exceptionnelle. Le stage est un prérequis pour la génération du compte étudiant et la soumission du rapport.
        *   **E.3.1. Consultation Globale et Recherche des Stages Enregistrés :**
            *   **Interface :** Un tableau paginé et triable listant tous les enregistrements de la table `faire_stage`.
            *   **SQL Requête de Base (Exemple pour affichage) :**
                ```sql
                SELECT
                    fs.numero_carte_etudiant,
                    e.nom AS nom_etudiant,
                    e.prenom AS prenom_etudiant,
                    ent.libelle_entreprise,
                    fs.id_entreprise, -- Clé pour modification/lien
                    fs.date_debut_stage,
                    fs.date_fin_stage,
                    fs.sujet_stage,
                    fs.nom_tuteur_entreprise
                    -- Potentiellement joindre avec inscrire/annee_academique pour contextualiser l'année du stage
                FROM
                    faire_stage fs
                JOIN etudiant e ON fs.numero_carte_etudiant = e.numero_carte_etudiant
                JOIN entreprise ent ON fs.id_entreprise = ent.id_entreprise
                -- WHERE ... (filtres)
                ORDER BY fs.date_debut_stage DESC, e.nom
                LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
                ```
            *   **Colonnes du Tableau :** "N° Carte Étudiant", "Nom Étudiant", "Prénom Étudiant", "Entreprise d'Accueil (`libelle_entreprise`)", "Date Début Stage", "Date Fin Stage", "Sujet du Stage (résumé)", "Nom Tuteur Entreprise".
            *   **Filtres et Recherche :**
                *   Recherche par `numero_carte_etudiant`, nom/prénom étudiant.
                *   Recherche par `libelle_entreprise` ou `id_entreprise`.
                *   Filtre par `id_annee_academique` (si le stage est lié à une année d'inscription, nécessite une jointure via `inscrire`).
                *   Filtrer les stages sans `date_fin_stage` (stages en cours).
                *   Filtrer par période (`date_debut_stage`, `date_fin_stage`).
            *   **Action par Ligne :** "Modifier Données du Stage" (mène à E.3.4), "Voir Profil Étudiant Lié", "Voir Fiche Entreprise Liée".

        *   **E.3.2. Gestion du Référentiel d'Entreprises (`entreprise`) :**
            *   **Redirection/Lien :** Cette fonctionnalité est principalement gérée dans la section D.1.8 (Gestion des Référentiels). L'onglet "Supervision Stages" peut fournir un lien direct vers cette section D.1.8 pour la commodité de l'administrateur.
            *   **Rappel des Fonctionnalités (Admin via D.1.8) :**
                *   **Lister les Entreprises :** `id_entreprise`, `libelle_entreprise`, `secteur_activite`, coordonnées.
                *   **Créer une Nouvelle Entreprise :** Saisie de `id_entreprise` (VARCHAR(50), unique), `libelle_entreprise`, et autres détails.
                *   **Modifier une Entreprise :** Mettre à jour les informations d'une entreprise existante.
                *   **Supprimer une Entreprise :** Possible seulement si aucune entrée dans `faire_stage` ne référence cet `id_entreprise`. Une fusion de doublons d'entreprises pourrait être une fonctionnalité avancée (mettre à jour `faire_stage.id_entreprise` puis supprimer le doublon).
            *   **Workflow de Validation (si entreprises ajoutées par RS/étudiants) :** L'admin pourrait avoir une liste d'entreprises "en attente de validation" si d'autres rôles peuvent en proposer de nouvelles, avant qu'elles ne deviennent utilisables globalement.

        *   **E.3.3. Configuration des Paramètres Relatifs aux Stages (Complément à D.2) :**
            *   **Interface :** Section de formulaire dans les paramètres applicatifs.
            *   **Paramètres configurables :**
                *   **Prérequis de Stage pour Accès Plateforme :**
                    *   Case à cocher : "La validation d'un enregistrement de stage dans `faire_stage` est requise pour la génération/activation du compte étudiant". (Confirme la règle métier déjà énoncée).
                *   **Documents Justificatifs pour le Stage (non modélisé par des uploads spécifiques, mais par existence de l'enregistrement `faire_stage`) :**
                    *   L'admin peut spécifier (informativement pour le RS) quels documents l'étudiant doit fournir au RS pour que ce dernier enregistre le stage (ex: convention de stage signée). Le système lui-même ne gère pas ces documents de convention, seulement l'attestation de stage parfois jointe au rapport (`document_soumis`).
                *   **Périodes Minimales/Maximales de Stage (par `id_niveau_etude` et `id_annee_academique`) :**
                    *   **Interface :** Champs numériques "Durée minimale stage (en semaines/mois)", "Durée maximale stage".
                    *   **Logique :** Utilisé par le RS lors de la saisie dans `faire_stage` pour validation (ou affichage d'un avertissement). `DATEDIFF(fs.date_fin_stage, fs.date_debut_stage)`.
                *   **Règles pour la validation du sujet de stage (processus métier externe) :** Le système ne gère pas un workflow de validation de sujet de stage avant l'enregistrement du stage lui-même. Si un tel processus existe, l'admin documente ici les prérequis.

        *   **E.3.4. Intervention de Niveau Administrateur sur les Données de Stage (`faire_stage`) :**
            *   **Objectif :** Corriger des erreurs de saisie sur les enregistrements de stage ou gérer des cas exceptionnels.
            *   **Interface :** Formulaire de modification d'un enregistrement `faire_stage` (accessible via E.3.1), pré-rempli.
            *   **Champs Modifiables par l'Admin (avec justification) :**
                *   Les clés (`id_entreprise`, `numero_carte_etudiant`) sont les identifiants de la relation. Leur modification équivaut à réassigner le stage. Si `id_entreprise` doit être changé parce que la mauvaise entreprise a été sélectionnée, c'est un `UPDATE`. Si le `numero_carte_etudiant` est erroné, il s'agit plus probablement d'une suppression/recréation.
                *   `date_debut_stage`, `date_fin_stage` (ex: pour corriger une erreur de saisie, prolongation de stage).
                *   `sujet_stage` (TEXT) : Si le sujet a été mal retranscrit.
                *   `nom_tuteur_entreprise` (VARCHAR(100)).
                *   Champ "Motif de la Modification (Admin)".
            *   **Logique PHP :**
                1.  Validation des modifications (ex: `date_fin_stage` > `date_debut_stage`).
                2.  `UPDATE faire_stage SET ... WHERE id_entreprise = ? AND numero_carte_etudiant = ?` (ou basée sur une PK simple si `faire_stage` en avait une, mais le DDL actuel est PK(id_entreprise, numero_carte_etudiant)).
                3.  Journalisation dans `enregistrer` : `id_action` = (ID de "Modification Admin Info Stage"), `type_entite_concernee` = "STAGE_ETUDIANT", `id_entite_concernee` (concaténation des PKs ou référence unique si créée pour `faire_stage`), `details_action` (JSON) avec anciennes/nouvelles valeurs.
            *   **Suppression d'un Enregistrement de Stage (EXCEPTIONNELLE) :**
                *   Si le stage a été enregistré par erreur et n'a aucun `rapport_etudiant` lié ou n'a pas servi à activer un compte étudiant.
                *   Confirmation forte.
                *   Vérification : `SELECT COUNT(*) FROM rapport_etudiant r JOIN inscrire i ON r.numero_carte_etudiant = i.numero_carte_etudiant WHERE r.numero_carte_etudiant = ? AND i.id_annee_academique = [annee_du_stage]`. Si >0, suppression bloquée.
                *   Logique : `DELETE FROM faire_stage WHERE id_entreprise = ? AND numero_carte_etudiant = ?;`. Journalisation.

        *   **Tables SQL Primordialement Impliquées pour E.3 :**
            *   `faire_stage` : Table principale pour les informations de stage.
            *   `entreprise` : Référentiel des entreprises.
            *   `etudiant` : Pour lier le stage à l'étudiant.
            *   `rapport_etudiant`, `inscrire` : Pour le contexte de l'année académique du stage et les vérifications de dépendances.
            *   `enregistrer` : Audit des interventions admin.

        *   **Considérations Spécifiques pour la Gestion des Stages par l'Admin :**
            *   **Rôle du Responsable Scolarité :** Le RS est généralement l'acteur principal pour la saisie et la mise à jour des données de `faire_stage` basées sur les documents fournis par l'étudiant. L'Admin intervient pour la configuration, la supervision, et les cas complexes.
            *   **Impact sur Accès Étudiant :** La présence d'un enregistrement valide dans `faire_stage` (avec potentiellement une validation de la part du RS) est un critère pour que le RS puisse créer/activer le compte `utilisateur` de l'étudiant.
            *   **Lien avec le Rapport de Soutenance :** Bien que le schéma ne lie pas explicitement `rapport_etudiant` à un `id_stage` spécifique dans `faire_stage`, la logique métier implique que le rapport porte sur le stage enregistré pour l'année académique pertinente. L'admin pourrait avoir des vues pour s'assurer de cette cohérence.

La supervision des stages par l'administrateur garantit que ce prérequis essentiel au processus de soutenance est correctement géré et que les données associées sont fiables.

---
**(Prêt pour E.4. Associations Enseignants.)**


Parfait. Concluons la section E avec **E.4. Associations Enseignants**.

---

    *   **E.4. Sous-Section / Onglet : Associations Enseignants (Configuration des affiliations académiques : `acquerir`, `occuper`, `attribuer`)**
        *   **Accès via Sidebar :** Menu "Gestion Académique" -> Sous-item "Associations Enseignants". Alternativement, ces fonctionnalités peuvent être intégrées directement dans l'interface de modification d'un profil enseignant (B.3.6), mais une section dédiée peut offrir une vue plus globale ou des outils de gestion en masse si nécessaire.
        *   **Objectif Spécifique :** Permettre à l'Administrateur Système (ou un rôle RH/académique délégué) de gérer et de maintenir à jour les informations structurelles relatives aux qualifications et fonctions des enseignants : leurs grades académiques, les fonctions qu'ils occupent, et les spécialités auxquelles ils sont rattachés. Ces informations, bien que ne donnant pas directement d'accès interactif à la majorité des enseignants (sauf membres de commission), sont cruciales comme **données de référence pour la Commission Pédagogique** lors de la sélection ou validation des directeurs de mémoire et pour la composition des jurys.
        *   **Interface Générale :** Souvent, cette section est organisée par type d'association (Grades, Fonctions, Spécialités), et pour chaque type, elle permet de sélectionner un enseignant puis de gérer ses associations.

        *   **E.4.1. Gestion des Associations Enseignant-Grade (table `acquerir`, liée à `enseignant` et `grade`)**
            *   **Objectif :** Enregistrer et suivre les différents grades académiques obtenus par chaque enseignant au fil du temps.
            *   **Interface :**
                1.  **Sélection de l'Enseignant :** Une liste déroulante ou un champ de recherche pour sélectionner le `numero_enseignant` (affichant `nom` et `prenom`).
                2.  **Affichage des Grades Actuels de l'Enseignant Sélectionné :** Un tableau listant les enregistrements de `acquerir` pour cet enseignant.
                    *   **Colonnes :** `libelle_grade` (jointure avec `grade`), `date_acquisition`.
                    *   **Action par ligne :** "Modifier Date", "Supprimer Association".
                3.  **Ajout d'une Nouvelle Association de Grade :**
                    *   **Formulaire :**
                        *   `id_grade` (VARCHAR(50), FK) : Liste déroulante des `libelle_grade` (valeur = `id_grade`) issus de la table `grade`.
                        *   `date_acquisition` (DATE) : Sélecteur de date.
                    *   **Logique PHP :**
                        *   Validation : S'assurer que la même `id_grade` n'est pas assignée plusieurs fois au même enseignant (à moins que cela ne soit sémantiquement possible, par ex. si la `date_acquisition` est la clé différenciante pour une promotion au même grade mais dans un autre contexte – mais `acquerir` a une PK sur (`id_grade`, `numero_enseignant`), donc une seule date par grade/enseignant).
                        *   `INSERT INTO acquerir (id_grade, numero_enseignant, date_acquisition) VALUES (?, ?, ?);`
                        *   Journalisation dans `enregistrer`.
            *   **Modification d'une Association :**
                *   Permet principalement de corriger la `date_acquisition`. `id_grade` et `numero_enseignant` (composantes de la PK) ne sont pas modifiables ; si erronés, supprimer et recréer.
                *   Logique : `UPDATE acquerir SET date_acquisition = ? WHERE id_grade = ? AND numero_enseignant = ?;`. Journalisation.
            *   **Suppression d'une Association :**
                *   Confirmation. `DELETE FROM acquerir WHERE id_grade = ? AND numero_enseignant = ?;`. Journalisation.

        *   **E.4.2. Gestion des Associations Enseignant-Fonction (table `occuper`, liée à `enseignant` et `fonction`)**
            *   **Objectif :** Enregistrer les différentes fonctions (administratives, pédagogiques) occupées par les enseignants, avec leurs dates de début et de fin.
            *   **Interface (similaire à E.4.1) :**
                1.  Sélection `numero_enseignant`.
                2.  Tableau des fonctions (`libelle_fonction`, `date_debut_occupation`, `date_fin_occupation`).
                    *   Action : "Modifier/Clôturer", "Supprimer".
                3.  **Ajout d'une Nouvelle Association de Fonction :**
                    *   Formulaire : `id_fonction` (VARCHAR(50), FK via liste déroulante `libelle_fonction`), `date_debut_occupation` (DATE), `date_fin_occupation` (DATE, NULLABLE).
                    *   Logique PHP :
                        *   Validation : `date_fin_occupation` doit être > `date_debut_occupation` si renseignée. Éviter chevauchements de dates pour la même fonction si la logique métier l'impose.
                        *   `INSERT INTO occuper (id_fonction, numero_enseignant, date_debut_occupation, date_fin_occupation) VALUES (?, ?, ?, ?);`. Journalisation.
            *   **Modification/Clôture d'une Association :**
                *   Modifier `date_debut_occupation`, `date_fin_occupation`. Mettre `date_fin_occupation` à une date passée pour clôturer une fonction.
                *   `UPDATE occuper SET ...`. Journalisation.
            *   **Suppression :** Confirmation, `DELETE FROM occuper ...`. Journalisation.

        *   **E.4.3. Gestion des Associations Enseignant-Spécialité (table `attribuer`, liée à `enseignant` et `specialite`)**
            *   **Objectif :** Lister les domaines de spécialisation ou d'expertise de chaque enseignant. Un enseignant peut avoir plusieurs spécialités.
            *   **Interface (similaire à E.4.1) :**
                1.  Sélection `numero_enseignant`.
                2.  Affichage des spécialités actuelles : typiquement une liste à cocher ou un "dual listbox" (comme pour les permissions en C.4.2) pour gérer plusieurs spécialités.
                    *   Liste A : `libelle_specialite` actuellement attribuées (via `attribuer`).
                    *   Liste B : `libelle_specialite` disponibles non attribuées.
                3.  **Modification des Associations :**
                    *   L'admin déplace les spécialités entre les listes.
                    *   Bouton "Enregistrer Associations Spécialités".
                *   **Logique PHP :** Similaire à la synchronisation de `rattacher` :
                    1.  Récupérer la liste finale des `id_specialite` souhaitées pour l'enseignant.
                    2.  Comparer avec les `id_specialite` actuellement dans `attribuer` pour cet enseignant.
                    3.  Effectuer les `INSERT INTO attribuer (numero_enseignant, id_specialite) ...` pour les nouvelles.
                    4.  Effectuer les `DELETE FROM attribuer WHERE numero_enseignant = ? AND id_specialite = ? ...` pour celles retirées.
                    5.  Journalisation de l'action globale de modification des spécialités.

        *   **Tables SQL Primordialement Impliquées pour E.4 :**
            *   `enseignant` : Pour sélectionner l'enseignant concerné.
            *   `grade`, `acquerir` : Pour les grades.
            *   `fonction`, `occuper` : Pour les fonctions.
            *   `specialite`, `attribuer` : Pour les spécialités.
            *   Les tables de référentiel `grade`, `fonction`, `specialite` sont utilisées pour peupler les listes déroulantes et afficher les libellés.
            *   `enregistrer` : Audit de toutes les modifications d'associations.

        *   **Considérations Spécifiques pour les Associations Enseignants :**
            *   **Pertinence pour la Commission :** L'objectif principal de maintenir ces associations à jour est de fournir des informations fiables à la Commission Pédagogique. Lorsqu'elle examine un rapport et doit valider/affecter un directeur de mémoire, la Commission peut souhaiter filtrer la liste des enseignants par `libelle_specialite` (pour trouver un expert du domaine) ou vérifier le `libelle_grade` et la `libelle_fonction` (certains rôles de direction de mémoire peuvent être réservés à des enseignants d'un certain grade/fonction). L'interface de la Commission pour cette tâche devrait donc pouvoir accéder en lecture à ces données agrégées.
            *   **Responsabilité de la Mise à Jour :** Bien que géré par l'Admin, la source de ces informations provient souvent du service RH ou de la direction des études. Un processus de communication doit exister pour que l'admin soit informé des changements (nouvelles promotions, changements de poste, nouvelles expertises).
            *   **Historisation :** Les tables `acquerir` et `occuper` (avec leurs dates) permettent une historisation naturelle des grades et fonctions. `attribuer` pour les spécialités est plus binaire (attribué/non attribué), une historisation des changements de spécialités nécessiterait des champs de date dans `attribuer` ou un log plus spécifique.
            *   **Cohérence :** L'Admin doit s'assurer que les `id_grade`, `id_fonction`, `id_specialite` utilisés existent bien dans leurs tables de référentiel respectives (géré par les contraintes FK).

Cette section E.4 clôture la "Gestion Académique & Administrative (Configuration & Supervision)" en se focalisant sur les attributs structurels des enseignants, qui bien que n'impliquant pas d'interaction directe de ces derniers (sauf membres de commission), sont des données importantes pour le bon déroulement d'autres processus, notamment ceux gérés par la Commission.

---
**(Prêt pour la section F. Supervision & Maintenance, en commençant par F.1. Suivi des Workflows.)**

Absolument. Entamons la section **F. Supervision & Maintenance** avec le niveau de détail requis.

---

**F. Supervision & Maintenance (Accès via Sidebar)**

La section "Supervision & Maintenance" du Module Administration est le centre de contrôle opérationnel et technique de "GestionMySoutenance". Elle est principalement destinée à l'Administrateur Système (ou à des rôles techniques avec des privilèges élevés). Son objectif est de permettre une surveillance active des processus en cours, d'assurer l'intégrité administrative des documents finaux, de gérer la volumétrie et la pérennité des données (logs, notifications), de fournir des outils d'investigation (audit), et de faciliter les opérations de maintenance technique et de gestion des données.

*   **Objectif Stratégique et Opérationnel :**
    *   **Stratégique :** Garantir la performance, la stabilité, la sécurité, et la conformité de la plateforme à long terme. S'assurer que les processus métier se déroulent sans heurts et que les données historiques sont correctement gérées et accessibles pour audit.
    *   **Opérationnel :** Fournir à l'Administrateur les tableaux de bord, les journaux, et les outils nécessaires pour :
        1.  Surveiller l'avancement des workflows critiques (validation des rapports).
        2.  Gérer administrativement les documents finalisés (PV).
        3.  Maintenir sous contrôle le volume des notifications et des logs.
        4.  Auditer en détail les actions utilisateurs et les accès système.
        5.  Faciliter les opérations d'import/export de données et la maintenance technique.

*   **Contenu et Fonctionnalités Détaillées de l'Interface :**

    *   **F.1. Sous-Section / Onglet : Suivi des Workflows et des Processus**
        *   **Accès via Sidebar :** "Supervision & Maintenance" -> "Suivi des Workflows".
        *   **Objectif Spécifique :** Offrir une vue d'ensemble dynamique de l'état d'avancement du principal workflow (soumission et validation des rapports de soutenance), permettant d'identifier rapidement les goulots d'étranglement, les retards, et la charge de travail des différents acteurs.
        *   **F.1.1. Tableau de Bord de Supervision des Rapports de Soutenance :**
            *   **Interface :** Une page de type dashboard avec plusieurs widgets visuels. Filtre principal par `id_annee_academique` (défaut sur l'active).
            *   **Widget 1 : Répartition des Rapports par Statut Actuel :**
                *   **Affichage :** Diagramme à barres ou circulaire.
                *   **Source des Données :** Table `rapport_etudiant` jointe avec `statut_rapport_ref`.
                *   **Calcul :** `SELECT srr.libelle_statut_rapport, COUNT(re.id_rapport_etudiant) FROM rapport_etudiant re JOIN statut_rapport_ref srr ON re.id_statut_rapport = srr.id_statut_rapport JOIN etudiant e ON re.numero_carte_etudiant = e.numero_carte_etudiant JOIN inscrire i ON e.numero_carte_etudiant = i.numero_carte_etudiant WHERE i.id_annee_academique = '[ID_ANNEE_CHOISIE]' GROUP BY srr.id_statut_rapport, srr.libelle_statut_rapport ORDER BY srr.etape_workflow;`
                *   **Exemple de catégories :** 'Soumis (attente conformité)', 'Non Conforme (retourné étudiant)', 'Conforme (attente commission)', 'En Commission (en vote)', 'Corrections Demandées (par commission)', 'Validé Final', 'Refusé Final'.
                *   **Interaction :** Cliquer sur une barre/section pourrait mener à une liste filtrée des rapports correspondants.
            *   **Widget 2 : Délais Moyens de Traitement par Étape Clé :**
                *   **Affichage :** Tableau ou série d'indicateurs numériques.
                *   **Calculs (complexes, nécessitant des timestamps de transition ou des logs précis dans `enregistrer`):**
                    *   Délai moyen (jours/heures) : `rapport_etudiant.date_soumission` -> `approuver.date_verification_conformite` (pour conformité).
                    *   Délai moyen : Date de statut "Conforme" -> Première `vote_commission.date_vote` pour ce rapport.
                    *   Délai moyen : Première `vote_commission.date_vote` -> Date de statut "Validé/Refusé/Correction Commission".
                    *   Délai moyen : Décision Commission -> `compte_rendu.date_creation_pv` (pour la rédaction du PV).
                    *   Délai moyen : `compte_rendu.date_creation_pv` -> `validation_pv.date_validation` finale du PV.
                *   **Logique :** Implique de retrouver les dates de changement de statut, soit via des champs dédiés historisant ces dates (non présents), soit en analysant les timestamps de `enregistrer` pour les actions correspondantes, ce qui est lourd. Une table `historique_statut_rapport(id_rapport_etudiant, id_statut_rapport, date_changement)` serait idéale.
            *   **Widget 3 : Rapports en Retard / Bloqués :**
                *   **Affichage :** Une liste de rapports critiques.
                *   **Critères :**
                    *   Rapports avec `id_statut_rapport` = 'RAP_SOUMIS' et `date_soumission` < (NOW() - X jours configurés en D.2.3).
                    *   Rapports avec `id_statut_rapport` = 'RAP_CONF' (ou en commission) et dont la date de passage à ce statut est < (NOW() - Y jours configurés).
                *   **Colonnes :** `id_rapport_etudiant`, `libelle_rapport_etudiant`, `numero_carte_etudiant` (étudiant), `date_soumission`, `libelle_statut_rapport` actuel, "Délai en attente".
                *   **Action :** Lien pour voir le détail du rapport et potentiellement notifier les responsables.
            *   **Widget 4 : Charge de Travail (Approximation) :**
                *   **Agents de Conformité :**
                    *   Nombre de rapports avec `id_statut_rapport` = 'RAP_SOUMIS'.
                    *   Si une affectation explicite à un agent existait (ex: table `rapport_assigne_conformite`), on pourrait voir la charge par agent. Actuellement, on ne voit que le pool global.
                *   **Commission Pédagogique :**
                    *   Nombre de rapports avec `id_statut_rapport` = 'RAP_CONF' (ou "en attente commission") + ceux "En Commission".
                *   **Rédacteurs de PV :** Nombre de décisions de commission prises où `compte_rendu.id_statut_pv` != 'PV_VALID'.
        *   **Tables SQL Impliquées pour F.1 :** `rapport_etudiant`, `statut_rapport_ref`, `approuver`, `vote_commission`, `compte_rendu`, `validation_pv`, `annee_academique`, `inscrire`, `etudiant`, `enregistrer` (pour timestamps si pas de table d'historique de statut dédiée).

    *   **F.2. Sous-Section / Onglet : Gestion des Procès-Verbaux (Admin) (`compte_rendu`)**
        *   **Accès via Sidebar :** "Supervision & Maintenance" -> "Gestion des Procès-Verbaux".
        *   **Objectif Spécifique :** Donner à l'administrateur un accès centralisé à tous les PV générés et validés, gérer leur statut d'archivage officiel et leur éligibilité à une diffusion externe.
        *   **F.2.1. Listage et Consultation de Tous les Procès-Verbaux :**
            *   **Interface :** Tableau paginé et triable de tous les enregistrements de `compte_rendu`.
            *   **Colonnes :** `id_compte_rendu`, `type_pv`, `id_rapport_etudiant` (lien vers détails rapport/étudiant), `libelle_compte_rendu` (ou un extrait/titre), `date_creation_pv`, `libelle_statut_pv` (via `statut_pv_ref`), `id_redacteur` (lien vers profil utilisateur du rédacteur).
            *   **Filtres :** Par `type_pv`, `id_statut_pv`, `id_annee_academique` (via rapport lié), `id_redacteur`.
            *   **Action par Ligne :**
                *   "Voir/Télécharger PDF du PV" (généré à la volée ou récupéré si déjà stocké).
                *   "Modifier Statut du PV" (pour l'admin, par exemple, de 'PV_VALID' à 'PV_ARCHIVE_OFFICIEL' – nouveau statut à ajouter à `statut_pv_ref`).
                *   "Marquer pour Publication Externe" (un champ booléen `eligible_publication_externe` pourrait être ajouté à `compte_rendu` ou `rapport_etudiant`).
        *   **F.2.2. Archivage Officiel des PV :**
            *   **Workflow :** L'admin sélectionne des PV avec `id_statut_pv` = 'PV_VALID'.
            *   Une action "Archiver Officiellement" met à jour leur statut (ex: `id_statut_pv` = 'PV_ARCHIVE_OFFICIEL') et/ou les exporte vers un système d'archivage dédié de l'institution (processus externe déclenché).
            *   Journalisation de l'action.
        *   **F.2.3. Gestion de l'Éligibilité à la Publication Externe (ex: DUMAS) :**
            *   **Workflow :** L'admin, potentiellement sur recommandation de la commission, identifie les PV/rapports de haute qualité.
            *   Il met à jour un flag `rapport_etudiant.publication_autorisee` (booléen, nouvelle colonne) ou `compte_rendu.publication_externe_ok` (booléen, nouvelle colonne).
            *   Une procédure (manuelle ou semi-automatisée) utilise ce flag pour l'export/soumission vers la plateforme externe.
        *   **Tables SQL Impliquées :** `compte_rendu`, `statut_pv_ref`, `rapport_etudiant`, `etudiant`, `utilisateur`. Potentiels nouveaux champs/statuts.

    *   **(La suite de F.3 à F.6 sera détaillée dans le prochain message.)**

La section F.1 permet de prendre le pouls du système en temps réel, tandis que F.2 se concentre sur le cycle de vie final des documents officiels produits. La capacité à dériver des délais de traitement (Widget 2 de F.1.1) est un indicateur de performance important, mais qui nécessite une conception soignée pour capturer les bons timestamps, idéalement via une table dédiée à l'historique des statuts pour chaque entité principale.


Absolument, poursuivons avec les sections restantes du **Module F. Supervision & Maintenance**.

---

    *   **F.3. Sous-Section / Onglet : Gestion des Notifications Système (`recevoir`, `notification`, `message`)**
        *   **Accès via Sidebar :** "Supervision & Maintenance" -> "Notifications Système".
        *   **Objectif Spécifique :** Offrir à l'Administrateur Système des outils pour gérer la volumétrie des notifications générées par la plateforme (celles stockées dans `recevoir` pour les utilisateurs), et superviser l'envoi effectif des communications.
        *   **F.3.1. Supervision des Notifications et Communications :**
            *   **Interface :** Section de tableau de bord ou de rapports.
            *   **Indicateurs :**
                *   Nombre total de notifications (`recevoir`) dans le système.
                *   Répartition des notifications par `id_notification` (lien vers `notification.libelle_notification`) pour voir les types les plus fréquents.
                *   Répartition des notifications par statut (`recevoir.lue` : "Lues" vs "Non Lues").
                *   Temps moyen avant lecture (`recevoir.date_lecture` - `recevoir.date_reception`).
                *   Si une file d'attente d'envoi d'emails est utilisée (ex: pour les emails en masse ou les rappels CRON), afficher l'état de cette file (nombre d'emails en attente, erreurs d'envoi récentes). Cela nécessite une intégration avec le service d'email (`ServiceEmail`).
            *   **Filtrage possible :** Par période, par `numero_utilisateur` destinataire, par `id_notification`.

        *   **F.3.2. Archivage et Purge des Notifications Utilisateurs (`recevoir`) :**
            *   **Objectif :** Empêcher la table `recevoir` de croître indéfiniment, ce qui pourrait impacter les performances. Maintenir la pertinence des notifications visibles par les utilisateurs.
            *   **Interface :** Formulaire avec des options de purge.
            *   **Options de Purge/Archivage :**
                *   "Supprimer toutes les notifications `lue = 1` plus anciennes que [N] mois/jours."
                *   "Supprimer toutes les notifications (lues ou non lues) plus anciennes que [M] mois/jours pour les utilisateurs avec `statut_compte` = 'archive' ou 'inactif'."
                *   "Archiver (si système d'archivage de logs distinct) puis supprimer..." (plus complexe).
            *   **Workflow :**
                1.  Admin sélectionne les critères et lance l'opération.
                2.  Fenêtre de confirmation avec le nombre d'enregistrements qui seraient affectés.
                3.  Sur confirmation, exécution de la requête `DELETE FROM recevoir WHERE ... (critères)`.
                4.  Journalisation dans `enregistrer` de l'action "Purge Notifications Utilisateurs" avec les critères utilisés et le nombre d'enregistrements supprimés dans `details_action`.
            *   **Considération :** Une purge trop agressive peut faire perdre un historique utile à l'utilisateur. Une politique de rétention claire doit être définie.

        *   **F.3.3. Gestion des Modèles de Message et de Notification (Redirection) :**
            *   Bien que les modèles soient configurés en D.3.2 (pour `message`) et D.1.13 (pour `notification`), cette section pourrait fournir des raccourcis vers ces interfaces de gestion si des ajustements rapides aux libellés ou aux contenus sont nécessaires suite à une supervision ici.
            *   Affiche également le nombre de fois où un `id_message` (template email) a été utilisé ou une `id_notification` (type de notif interne) a été générée (via `COUNT` sur `recevoir` et logs d'email si disponibles).

        *   **Tables SQL Impliquées :** `recevoir`, `notification`, `message`, `utilisateur` (pour filtrer par utilisateur ou statut de compte), `enregistrer`.

    *   **F.4. Sous-Section / Onglet : Journaux d'Audit (`enregistrer`, `pister`)**
        *   **Accès via Sidebar :** "Supervision & Maintenance" -> "Journaux d'Audit". Peut être divisé en "Journal des Actions" et "Journal des Accès".
        *   **Objectif Spécifique :** Fournir à l'Administrateur Système un accès complet et des capacités de recherche avancée dans les logs d'audit du système, ce qui est fondamental pour la sécurité, la traçabilité des opérations, la résolution de problèmes, et la conformité réglementaire. Ces journaux ne doivent être modifiables sous aucun prétexte via l'interface.
        *   **F.4.1. Consultation Détaillée du Journal des Actions des Utilisateurs (`enregistrer`) :**
            *   **Interface :** Un tableau paginé très détaillé, affichant tous les enregistrements de la table `enregistrer`, avec des outils de filtrage et de recherche puissants.
            *   **SQL Requête de Base :**
                ```sql
                SELECT
                    enr.date_action,
                    enr.numero_utilisateur AS auteur_action_num,
                    u_auteur.login_utilisateur AS auteur_action_login,
                    act.libelle_action,
                    enr.type_entite_concernee,
                    enr.id_entite_concernee, -- Ce sera un VARCHAR(50) pour être générique
                    enr.details_action, -- JSON
                    enr.adresse_ip,
                    enr.user_agent,
                    enr.session_id_utilisateur
                FROM
                    enregistrer enr
                JOIN utilisateur u_auteur ON enr.numero_utilisateur = u_auteur.numero_utilisateur
                JOIN action act ON enr.id_action = act.id_action
                -- WHERE et ORDER BY clause ici
                LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
                ```
            *   **Colonnes du Tableau :** "Date & Heure", "Auteur de l'Action (Login)", "Type d'Action (`libelle_action`)", "Type Entité Affectée", "ID Entité Affectée", "Détails de l'Action (Affichage formaté du JSON, ex: ancienne/nouvelle valeur)", "Adresse IP", "User Agent", "ID Session".
            *   **Filtres et Recherche Approfondis :**
                *   Par `date_action` (plage de dates/heures).
                *   Par `numero_utilisateur` de l'auteur (champ de saisie avec auto-complétion).
                *   Par `id_action` (liste déroulante des `libelle_action`).
                *   Par `type_entite_concernee` (ex: "UTILISATEUR", "RAPPORT_ETUDIANT", "INSCRIPTION").
                *   Par `id_entite_concernee` (si on recherche toutes les actions sur un utilisateur ou un rapport spécifique).
                *   Recherche textuelle dans `details_action` (si le SGBD supporte bien la recherche dans JSON, sinon plus limité).
                *   Par `adresse_ip`.
            *   **Fonctionnalité :** Export des résultats filtrés en CSV pour une analyse externe.
            *   **Importance :** Le champ `details_action` (JSON) est clé. Il doit stocker des informations structurées pour chaque type d'action, par exemple :
                *   Pour une modification : `{ "champ_modifie": "statut_compte", "ancienne_valeur": "actif", "nouvelle_valeur": "inactif", "motif_admin": "départ" }`
                *   Pour une création : `{ "entite_creee_id": "USR_ETU_...", "valeurs_initiales": { ... } }`
                *   Pour une action de masse : `{ "action_groupee": "changement_statut", "nouveau_statut": "archive", "ids_affectes": ["USR1", "USR2", ...], "nombre_affectes": X }`

        *   **F.4.2. Consultation Détaillée de la Traçabilité des Accès aux Fonctionnalités (`pister`) :**
            *   **Interface :** Tableau paginé similaire, affichant les enregistrements de `pister`.
            *   **SQL Requête de Base :**
                ```sql
                SELECT
                    p.date_pister,
                    p.numero_utilisateur AS utilisateur_acces_num,
                    u_acces.login_utilisateur AS utilisateur_acces_login,
                    t.libelle_traitement,
                    p.acceder -- Booléen : 1 pour accès réussi/permis, 0 pour refusé
                FROM
                    pister p
                JOIN utilisateur u_acces ON p.numero_utilisateur = u_acces.numero_utilisateur
                JOIN traitement t ON p.id_traitement = t.id_traitement
                -- WHERE et ORDER BY
                LIMIT [OFFSET], [NOMBRE_PAR_PAGE];
                ```
            *   **Colonnes du Tableau :** "Date & Heure Accès", "Utilisateur (Login)", "Fonctionnalité Tentée (`libelle_traitement`)", "Accès Accordé (Oui/Non)".
            *   **Filtres et Recherche :**
                *   Par `date_pister` (plage).
                *   Par `numero_utilisateur` accédant.
                *   Par `id_traitement` (liste déroulante des `libelle_traitement`).
                *   Par statut `acceder` (pour voir tous les refus de permission).
            *   **Importance :** Utile pour investiguer les tentatives d'accès non autorisées ou pour comprendre quelles fonctionnalités sont les plus (ou les moins) utilisées par quels groupes.

        *   **Considérations pour les Journaux d'Audit :**
            *   **Intégrité et Immutabilité :** Les logs ne doivent pas être modifiables via l'interface. Seule la consultation et potentiellement l'archivage/purge par des scripts sécurisés sont permis.
            *   **Volume des Logs :** Les tables `enregistrer` et `pister` peuvent devenir très volumineuses. Une stratégie de rotation des logs, d'archivage vers un système de logging centralisé (ELK stack, Splunk), ou de purge des logs très anciens (conformément aux politiques de rétention légales/institutionnelles) est indispensable à long terme.
            *   **Performance des Recherches :** Une indexation très soignée des tables `enregistrer` et `pister` est nécessaire sur les colonnes fréquemment utilisées en filtrage (`date_action`, `numero_utilisateur`, `id_action`, `type_entite_concernee`, `id_entite_concernee`).

    *   **(La suite de F.5. Outils d'Import/Export Données et F.6. Maintenance Technique sera détaillée dans la prochaine réponse.)**

La section des journaux d'audit est la mémoire de l'application. Elle est indispensable pour la sécurité, la responsabilité et la capacité à diagnostiquer des problèmes a posteriori.

---
**(Prêt pour la suite de F.)**


Excellent, terminons la section **F. Supervision & Maintenance** avec les sous-sections **F.5 et F.6**.

---

    *   **F.5. Sous-Section / Onglet : Outils d'Import/Export Données**
        *   **Accès via Sidebar :** "Supervision & Maintenance" -> "Import/Export Données".
        *   **Objectif Spécifique :** Fournir à l'Administrateur Système des fonctionnalités contrôlées et sécurisées pour insérer des données en masse dans le système (import) et pour extraire des données (export) à des fins de sauvegarde, d'analyse externe, de migration, ou de conformité. **Ces outils sont exclusivement réservés à l'Administrateur Système avec les droits les plus élevés, étant donné leur potentiel d'impact sur la base de données.**
        *   **F.5.1. Fonctionnalité d'Import de Données :**
            *   **Objectif :** Faciliter la création initiale ou la mise à jour en masse d'enregistrements, typiquement pour les profils utilisateurs (`etudiant`, `enseignant`, `personnel_administratif` et leurs comptes `utilisateur` associés) ou certains référentiels volumineux (ex: `entreprise` si une liste initiale est fournie).
            *   **Interface d'Import (Processus en plusieurs étapes) :**
                1.  **Étape 1 : Sélection du Type de Données à Importer.**
                    *   Liste déroulante : "Importer des Étudiants", "Importer des Enseignants", "Importer du Personnel Administratif", "Importer des Entreprises", "Importer un Référentiel Spécifique (ex: UE/ECUE depuis un plan d'études)".
                2.  **Étape 2 : Téléversement du Fichier Source et Spécification des Options.**
                    *   Champ de téléversement : Pour un fichier CSV (format privilégié pour sa simplicité), potentiellement XML ou Excel (nécessite des librairies PHP de parsing plus complexes).
                    *   Spécification du délimiteur CSV (virgule, point-virgule, tabulation).
                    *   Encodage du fichier (UTF-8 par défaut).
                    *   Option "La première ligne contient les en-têtes de colonnes ?" (case à cocher).
                    *   Options de Traitement des Doublons (basé sur la clé primaire métier, ex: `etudiant.numero_carte_etudiant` ou `utilisateur.login_utilisateur`) :
                        *   "Ignorer les lignes en doublon (ne pas importer)."
                        *   "Mettre à jour les enregistrements existants avec les données du fichier."
                        *   "Arrêter l'import et signaler les doublons." (Mode le plus sûr).
                    *   Option "Mode Simulation (Validation Uniquement)" : Case à cocher pour tester le fichier sans insérer réellement de données.
                3.  **Étape 3 : Mapping des Colonnes (si la première ligne ne correspond pas exactement aux noms de champs BDD).**
                    *   Si l'option "en-têtes de colonnes" est cochée, le système essaie de mapper automatiquement.
                    *   Sinon, ou pour ajustement : une interface affiche les colonnes détectées dans le fichier et permet à l'admin de les associer à chaque champ requis/optionnel de la table cible via des listes déroulantes.
                    *   Exemple pour Étudiants : Colonne Fichier "Matricule" -> Table `etudiant`.`numero_carte_etudiant`; Colonne Fichier "Nom Famille" -> Table `etudiant`.`nom`.
                4.  **Étape 4 : Validation et Prévisualisation (avant import réel).**
                    *   Le système parse un échantillon du fichier (ex: les 10 premières lignes de données) et applique les règles de validation (format, types, obligatoires).
                    *   Affiche un résumé : "X lignes à importer, Y lignes avec erreurs potentielles."
                    *   Liste les erreurs de validation détectées par ligne et par colonne (ex: "Ligne 5, Colonne 'Date Naissance': format invalide.").
                5.  **Étape 5 : Exécution de l'Import.**
                    *   Bouton "Lancer l'Importation" (si pas en mode simulation et pas d'erreurs bloquantes, ou si l'admin force malgré des avertissements).
                    *   La logique PHP traite le fichier ligne par ligne (ou par lots pour performance) :
                        *   Génère les `id_...` VARCHAR manuels si nécessaire (ex: `numero_utilisateur` pour chaque étudiant/enseignant/personnel importé).
                        *   Effectue les `INSERT` (et `UPDATE` si option choisie) dans les tables concernées (`utilisateur` puis `etudiant`/`enseignant`/`personnel_administratif`).
                        *   Gère les transactions pour assurer la cohérence.
                        *   Journalise chaque création/modification dans `enregistrer`.
                6.  **Étape 6 : Rapport d'Importation.**
                    *   Affichage d'un résumé final : "Importation terminée. X enregistrements créés, Y mis à jour, Z en erreur."
                    *   Lien pour télécharger un fichier log détaillé des erreurs par ligne (ex: "Ligne 25: Login 'dup_login' déjà existant.").
            *   **Sécurité et Précautions :**
                *   Valider et nettoyer rigoureusement les données du fichier source.
                *   Effectuer des sauvegardes de la base de données avant des imports massifs.
                *   Commencer par un mode simulation.
                *   Gérer les timeouts PHP (`max_execution_time`) pour les fichiers volumineux (traiter par lots, tâches en arrière-plan).

        *   **F.5.2. Fonctionnalité d'Export de Données :**
            *   **Objectif :** Permettre à l'administrateur d'extraire des données de la plateforme pour des analyses hors ligne, des sauvegardes spécifiques, ou des transferts vers d'autres systèmes.
            *   **Interface d'Export :**
                1.  **Étape 1 : Sélection du Type de Données / Table(s) à Exporter.**
                    *   Liste des tables principales (ex: `utilisateur`, `etudiant`, `rapport_etudiant`, `inscrire`, `compte_rendu`) ou des ensembles de données prédéfinis (ex: "Tous les étudiants actifs de l'année X", "Tous les PV validés").
                2.  **Étape 2 : Application de Filtres (Optionnel).**
                    *   Interface similaire à celle de recherche/filtrage des listes (ex: exporter uniquement les étudiants d'un certain `id_niveau_etude` pour l'`id_annee_academique` active).
                3.  **Étape 3 : Sélection des Colonnes à Exporter (Optionnel).**
                    *   Par défaut, toutes les colonnes de la table sélectionnée.
                    *   L'admin pourrait décocher certaines colonnes (ex: ne pas exporter les mots de passe hachés).
                4.  **Étape 4 : Choix du Format d'Export.**
                    *   Options : CSV (avec choix du délimiteur), XML, SQL (série de `INSERT INTO ...`).
                5.  **Étape 5 : Génération et Téléchargement.**
                    *   Bouton "Générer et Télécharger l'Export".
                    *   La logique PHP construit la requête SQL avec les filtres, récupère les données, les formate selon le choix, et initie le téléchargement du fichier.
                    *   Pour des exports très volumineux, la génération peut prendre du temps (indicateur de progression, ou génération en arrière-plan avec notification quand prêt).
            *   **Cas d'Usages Communs :**
                *   Export de la liste des étudiants pour mailing postal.
                *   Export des données de rapports pour analyse statistique dans un outil BI.
                *   Export d'une table pour sauvegarde avant une opération de maintenance risquée.
        *   **Tables SQL Impliquées pour F.5 :** Potentiellement toutes les tables en fonction des besoins d'import/export. La logique d'import doit gérer les relations et les clés étrangères correctement. `enregistrer` pour l'audit des opérations d'import.

    *   **F.6. Sous-Section / Onglet : Maintenance Technique**
        *   **Accès via Sidebar :** "Supervision & Maintenance" -> "Maintenance Technique".
        *   **Objectif Spécifique :** Fournir à l'Administrateur Système des outils pour effectuer des opérations de maintenance de bas niveau, de diagnostic et de sauvegarde/restauration. **Ces fonctionnalités sont extrêmement sensibles et doivent être utilisées avec la plus grande prudence.**
        *   **F.6.1. Outils de Maintenance de la Base de Données :**
            *   **Interface :** Une série de boutons d'action, chacun avec une description claire et un avertissement.
            *   **Actions Disponibles (exemples pour MySQL) :**
                *   **"Optimiser les Tables" :** Déclenche `OPTIMIZE TABLE nom_table;` sur des tables sélectionnées ou toutes les tables. Utile pour réorganiser le stockage physique et améliorer les performances après de nombreuses écritures/suppressions.
                *   **"Analyser les Tables" :** Déclenche `ANALYZE TABLE nom_table;`. Met à jour les statistiques des clés pour l'optimiseur de requêtes.
                *   **"Vérifier les Tables" :** Déclenche `CHECK TABLE nom_table;`. Vérifie l'intégrité.
                *   **"Réparer les Tables" (si SGBD le supporte pour certains moteurs) :** `REPAIR TABLE nom_table;`.
                *   **"Nettoyer les Données Temporaires/Obsolètes" :** Déclenche des scripts PHP spécifiques (conçus par les développeurs) pour purger les sessions utilisateur expirées (si stockées en BDD), les tokens de validation/reset expirés non utilisés, les brouillons de rapports non soumis depuis longtemps, etc.
            *   **Logique :** Ces actions exécutent des commandes SQL ou des scripts PHP côté serveur.

        *   **F.6.2. Gestion des Sauvegardes et Procédures de Restauration :**
            *   **Philosophie :** La sauvegarde régulière est critique. L'interface admin peut faciliter certaines opérations mais ne remplace pas une stratégie de sauvegarde robuste au niveau serveur (ex: via `mysqldump` en CRON pour MySQL).
            *   **Interface :**
                *   **Déclencher une Sauvegarde Manuelle :** Bouton "Effectuer une Sauvegarde Complète Maintenant".
                    *   Logique PHP : Exécute un script serveur qui fait un dump complet de la base de données (`mysqldump`) vers un fichier compressé dans un emplacement sécurisé sur le serveur (configurable), avec un nom de fichier incluant la date et l'heure.
                    *   Affiche le statut de l'opération.
                *   **Lister les Sauvegardes Disponibles :** Si les sauvegardes sont stockées dans un répertoire connu, lister les fichiers de sauvegarde avec date, taille, et potentiellement une option pour les télécharger.
                *   **Procédure de Restauration (Très Délicate, souvent faite en CLI) :**
                    *   Si une interface est proposée : sélection d'un fichier de sauvegarde, avertissements multiples sur l'écrasement des données actuelles.
                    *   L'application doit être mise en **mode maintenance** (inaccessible aux utilisateurs) avant toute restauration.
                    *   La restauration implique généralement d'arrêter le serveur web, de restaurer la BDD via les outils SGBD, puis de redémarrer. Difficile à orchestrer entièrement via une interface web sécurisée sans accès direct au serveur.
                    *   Le plus souvent, cette section se limite à fournir la documentation sur la procédure de restauration manuelle à effectuer par l'admin système en ligne de commande.
        *   **F.6.3. Application des Mises à Jour Applicatives (si applicable) :**
            *   **Interface (pour des mises à jour mineures ou patchs gérés par l'application elle-même) :**
                *   Affichage de la version actuelle de "GestionMySoutenance".
                *   Bouton "Vérifier les Mises à Jour".
                *   Si une mise à jour est disponible (depuis un dépôt central) : affichage des notes de version, bouton "Appliquer la Mise à Jour".
            *   **Logique :** Processus complexe impliquant le téléchargement de fichiers, leur remplacement, l'exécution de scripts de migration de base de données potentiels. Nécessite des droits d'écriture sur les fichiers de l'application. Typiquement, des outils comme `composer` ou des scripts de déploiement dédiés sont utilisés en dehors de l'interface admin pour les mises à jour majeures.
        *   **F.6.4. Informations de Diagnostic Système et Serveur :**
            *   **Objectif :** Fournir des informations de base pour le diagnostic.
            *   **Interface :** Section affichant des données en lecture seule :
                *   Version de PHP, extensions PHP critiques (ex: mbstring, json, pdo_mysql).
                *   Version du SGBD.
                *   Informations de configuration PHP pertinentes (ex: `memory_limit`, `upload_max_filesize`, `post_max_size`, `max_execution_time`).
                *   Permissions d'écriture sur les répertoires clés (uploads, cache, logs) - testées par PHP.
                *   Test de connexion à la base de données.
                *   Peut-être un lien vers `phpinfo()` (à protéger très strictement).
        *   **Tables SQL Impliquées pour F.6 :** Opérations au niveau du SGBD ou du système de fichiers. `enregistrer` pour l'audit des actions de maintenance déclenchées via l'interface.

    *   **Considérations Générales pour la Supervision & Maintenance :**
        *   **Droits d'Accès Stricts :** Cette section entière doit être protégée et accessible uniquement par les rôles d'administrateur système les plus élevés, ayant une compréhension technique.
        *   **Mode Maintenance Applicatif :** Pour certaines opérations (restauration, mises à jour majeures, scripts BDD longs), l'admin doit pouvoir mettre l'application en "mode maintenance". Cela affiche une page d'indisponibilité temporaire à tous les autres utilisateurs et empêche les écritures en base.
        *   **Documentation et Procédures :** Des procédures claires doivent exister pour les opérations critiques comme la restauration de sauvegarde.
        *   **Logs Applicatifs PHP/Serveur Web :** L'admin doit avoir accès (hors interface de l'application généralement, directement sur le serveur) aux logs d'erreurs PHP et du serveur web pour un diagnostic complet.

La section Supervision & Maintenance est la "salle des machines" du module administration, fournissant les leviers pour maintenir la plateforme en bon état de fonctionnement, la sécuriser, et intervenir en cas de problèmes techniques profonds.

---
**(La section F est complète. Prêt pour la section G : Reporting & Analytique.)**


Parfait, achevons le Module Administration avec la section **G. Reporting & Analytique**.

---

**G. Reporting & Analytique (Accès via Sidebar)**

La section "Reporting & Analytique" du Module Administration vise à transformer les vastes quantités de données opérationnelles générées par "GestionMySoutenance" en informations structurées, visualisations et indicateurs de performance (KPIs). Ces éléments sont conçus pour aider les différentes strates de la direction de l'établissement (direction générale, responsables de filières, responsables qualité, administrateurs système eux-mêmes) à comprendre les tendances, évaluer l'efficacité des processus, identifier les points d'amélioration et prendre des décisions éclairées basées sur des données factuelles.

*   **Objectif Stratégique et Opérationnel :**
    *   **Stratégique :** Fournir un support à la décision pour l'amélioration continue des processus académiques et administratifs liés aux soutenances. Permettre une évaluation quantitative et qualitative de la performance du système et des acteurs.
    *   **Opérationnel :** Mettre à disposition des administrateurs (ou des rôles délégués spécifiques au reporting) des outils flexibles pour :
        1.  Générer des rapports statistiques avancés sur des aspects variés de l'activité de la plateforme.
        2.  Configurer et visualiser des tableaux de bord analytiques personnalisés avec des graphiques et des KPIs.

*   **Contenu et Fonctionnalités Détaillées de l'Interface :**

    *   **G.1. Sous-Section / Onglet : Génération de Rapports Statistiques Avancés**
        *   **Accès via Sidebar :** "Reporting & Analytique" -> "Générer Rapports".
        *   **Objectif Spécifique :** Permettre la création à la demande de rapports tabulaires ou agrégés, souvent exportables, pour des analyses approfondies ou des besoins de reporting spécifiques.
        *   **Interface de Génération de Rapports :**
            *   Un formulaire ou une interface guidée permettant de construire une requête de rapport.
            *   **Étape 1 : Sélection du Domaine de Rapport / Sujet Principal.**
                *   Exemples : "Activité des Rapports de Soutenance", "Performance des Acteurs de Validation", "Statistiques d'Inscription", "Analyse des Thématiques de Rapports".
            *   **Étape 2 : Sélection des Indicateurs / Mesures à Inclure.**
                *   En fonction du domaine, une liste de métriques disponibles s'affiche.
                    *   Pour "Activité Rapports" : Taux de soumission, Taux de conformité, Taux de validation commission, Délai moyen par étape, Nombre de versions.
                    *   Pour "Performance Acteurs" : Nombre de rapports traités/votés par agent/membre, Délai moyen de traitement individuel (avec anonymisation si nécessaire pour certains rôles).
                    *   Pour "Thématiques" : Comptage des rapports par `rapport_etudiant.theme` (si exploitable).
            *   **Étape 3 : Sélection des Dimensions de Groupement / Agrégation.**
                *   Exemples : Par `id_annee_academique`, `id_niveau_etude`, `id_specialite` (de l'étudiant via `inscrire`), `id_type_document_ref`.
            *   **Étape 4 : Application de Filtres.**
                *   Période (plage de dates pour `rapport_etudiant.date_soumission`, `approuver.date_verification_conformite`, etc.).
                *   Filtres sur les dimensions choisies (ex: uniquement pour "AA_2023_2024" et "NIV_M2_INFO").
            *   **Étape 5 : Options de Formatage et d'Export.**
                *   Bouton "Générer le Rapport".
                *   Choix du format de sortie : Affichage HTML dans la page, Export CSV, Export Excel (via une librairie PHP comme PHPSpreadsheet), Export PDF (pour des rapports formatés).
            *   **Option de Sauvegarde de Configuration de Rapport :** Permettre de nommer et sauvegarder une configuration de rapport complexe pour la réexécuter ultérieurement. (Nécessiterait une table `rapport_configurations_sauvegardees`).

        *   **G.1.1. Exemples de Rapports Prédéfinis ou Configurables :**
            *   **(Rappel des rapports listés dans la réponse précédente, détaillés ici en termes de données et de flux)**
            *   **Rapport sur le Processus de Validation des Rapports de Stage :**
                *   **Taux de Conformité (pour une période/année donnée) :**
                    *   `SELECT s.libelle_statut_conformite, COUNT(a.id_rapport_etudiant) AS nombre_total FROM approuver a JOIN statut_conformite_ref s ON a.id_statut_conformite = s.id_statut_conformite WHERE a.date_verification_conformite BETWEEN ? AND ? GROUP BY s.id_statut_conformite, s.libelle_statut_conformite;`
                    *   Affiché en % pour "CONF_OK" vs "CONF_NOK".
                *   **Taux de Validation Commission :**
                    *   Nécessite d'analyser les `rapport_etudiant.id_statut_rapport` finaux (ex: 'RAP_VALID', 'RAP_REFUSE', 'RAP_CORRECT') pour les rapports ayant atteint l'étape commission.
                    *   `SELECT sr.libelle_statut_rapport, COUNT(re.id_rapport_etudiant) FROM rapport_etudiant re JOIN statut_rapport_ref sr ON re.id_statut_rapport = sr.id_statut_rapport WHERE sr.id_statut_rapport IN ('RAP_VALID', 'RAP_REFUSE', 'RAP_CORRECT') /* ET autres filtres année/niveau */ GROUP BY sr.id_statut_rapport, sr.libelle_statut_rapport;`
                *   **Délais Moyens de Traitement :**
                    *   **Algorithme pour Délai Conformité :** Pour chaque `id_rapport_etudiant`, trouver la `date_soumission` dans `rapport_etudiant` et la `date_verification_conformite` dans `approuver`. Calculer la différence (`DATEDIFF` ou timestampdiff). Faire la moyenne.
                    *   **Logique PHP Complexe :** La logique pour calculer ces délais de manière précise en tenant compte des weekends, des jours fériés (si nécessaire), et des différentes transitions de statut est non triviale et doit être implémentée côté serveur. Une table d'historique des changements de statut de rapport (`historique_statut_rapport(id_hist INT PK, id_rapport_etudiant VARCHAR(50) FK, id_ancien_statut VARCHAR(50) FK, id_nouveau_statut VARCHAR(50) FK, date_transition DATETIME, numero_utilisateur_action VARCHAR(50) FK)`) simplifierait grandement ces calculs. Sans cela, il faut se baser sur les timestamps des tables d'action (`approuver`, `vote_commission`, `enregistrer`), ce qui est moins direct.
                *   **Performance des Acteurs (avec anonymisation optionnelle) :**
                    *   **Agents de Conformité :** `SELECT pa.numero_personnel_administratif, CONCAT(pa.nom, ' ', pa.prenom) AS agent, COUNT(a.id_rapport_etudiant) AS rapports_traites, AVG(TIMESTAMPDIFF(HOUR, re.date_soumission, a.date_verification_conformite)) AS delai_moyen_traitement_heures FROM approuver a JOIN personnel_administratif pa ON a.numero_personnel_administratif = pa.numero_personnel_administratif JOIN rapport_etudiant re ON a.id_rapport_etudiant = re.id_rapport_etudiant /*+ filtres date*/ GROUP BY pa.numero_personnel_administratif;`

            *   **Rapports sur les Contenus et Corrections :**
                *   **Tendances Thématiques :** `SELECT theme, COUNT(id_rapport_etudiant) AS occurrences FROM rapport_etudiant WHERE theme IS NOT NULL AND theme != '' /*+ filtres année*/ GROUP BY theme ORDER BY occurrences DESC;` (Efficacité dépend de la qualité de saisie des thèmes).
                *   **Analyse des Commentaires de Non-Conformité/Corrections Demandées :** Si les commentaires dans `approuver.commentaire_conformite` ou `vote_commission.commentaire_vote` sont structurés ou peuvent être analysés (ex: par mots-clés), des rapports pourraient être générés. C'est un défi de traitement de langage naturel plus qu'une simple requête SQL.
                *   **Nombre Moyen de Versions Soumises :**
                    *   `SELECT id_rapport_etudiant, MAX(version) AS max_version FROM document_soumis WHERE id_type_document = 'DOC_RAP_MAIN' GROUP BY id_rapport_etudiant;`
                    *   Ensuite, faire la moyenne des `max_version`. Nécessite que les resoumissions créent de nouvelles versions dans `document_soumis`.

            *   **Rapports sur les Inscriptions et les Notes :**
                *   Déjà esquissés dans la description de la section E (Supervision). Ici, il s'agit de permettre à l'admin de les générer et de les exporter.

        *   **F.1.2. Personnalisation et Planification de Rapports (Fonctionnalités Avancées) :**
            *   Possibilité pour l'admin de construire ses propres requêtes via un Query Builder graphique simplifié (très avancé) ou de sauvegarder des "vues" de données complexes.
            *   Planification de l'envoi automatique de certains rapports par email à des destinataires spécifiques (ex: rapport mensuel d'activité à la direction). Nécessite une tâche CRON et une gestion des abonnements/destinataires.

        *   **Tables SQL Impliquées :** Large éventail de tables, principalement `rapport_etudiant`, `statut_rapport_ref`, `approuver`, `vote_commission`, `document_soumis`, `compte_rendu`, `etudiant`, `enseignant`, `personnel_administratif`, `inscrire`, `annee_academique`, `niveau_etude`, `specialite`, `enregistrer` (pour les métadonnées de temps).

    *   **G.2. Sous-Section / Onglet : Configuration et Visualisation de Tableaux de Bord Analytiques (Dashboards)**
        *   **Accès via Sidebar :** "Reporting & Analytique" -> "Tableaux de Bord" ou "Configurer Dashboards".
        *   **Objectif Spécifique :** Offrir une interface visuelle et interactive pour suivre les KPIs clés, permettant une compréhension rapide des tendances et des performances, souvent pour un public de direction.
        *   **G.2.1. Bibliothèque de Widgets/Graphiques Prédéfinis :**
            *   Le système propose une série de "widgets" préconfigurés que l'admin peut choisir et agencer. Chaque widget correspond à une visualisation d'un KPI spécifique :
                *   Ex: Widget "Taux de Validation des Rapports (sur 12 mois)", "Délai Moyen Global du Processus", "Répartition des Thèmes les Plus Courants", "Charge de Travail par Étape du Workflow".
            *   Chaque widget est alimenté par une requête SQL d'agrégation spécifique (similaire à celles de G.1).
        *   **G.2.2. Interface de Création/Personnalisation de Tableau de Bord :**
            *   **Interface :**
                1.  Donner un nom au tableau de bord.
                2.  Grille de mise en page (ex: 2x2, 3x2 widgets).
                3.  Pour chaque cellule de la grille, l'admin choisit un widget dans la bibliothèque.
                4.  Pour certains widgets, des options de configuration peuvent être disponibles (ex: type de graphique - barres, lignes, camembert ; période de données par défaut).
            *   **Stockage de la Configuration :** La structure de chaque tableau de bord personnalisé (quels widgets, leur configuration, leur position) est stockée, potentiellement dans une nouvelle table `dashboard_configurations (id_dashboard VARCHAR(50) PK, libelle_dashboard VARCHAR(255), configuration_widgets JSON, id_groupe_acces VARCHAR(50) FK OPTIONAL)`.
        *   **G.2.3. Visualisation des Tableaux de Bord :**
            *   L'admin (ou les utilisateurs/groupes ayant accès) sélectionne un tableau de bord configuré.
            *   La page charge dynamiquement les widgets, exécute les requêtes associées (avec filtres globaux de période/année si applicables au dashboard), et affiche les graphiques interactifs (librairies JS comme Chart.js, ApexCharts, etc.).
            *   Les graphiques peuvent offrir des tooltips, des options de zoom, d'export d'image.
        *   **G.2.4. Filtrage Global des Tableaux de Bord :**
            *   Possibilité d'avoir des filtres en haut de la page du tableau de bord (ex: sélection d'`id_annee_academique`, `id_niveau_etude`) qui s'appliquent dynamiquement à tous les widgets du dashboard.
        *   **Tables SQL Impliquées :** Mêmes tables sources que G.1 pour les données des widgets. Nouvelle table `dashboard_configurations` pour la méta-configuration.

    *   **Considérations Générales pour Reporting & Analytique :**
        *   **Performance et Optimisation (Répétition Critique) :** L'aspect le plus challenging est de garantir que la génération de rapports et l'affichage des dashboards soient performants, surtout avec l'historisation des données sur plusieurs années.
            *   **Indexation :** Essentielle sur toutes les colonnes utilisées dans les `WHERE`, `JOIN`, `GROUP BY`, `ORDER BY`.
            *   **Agrégats Précalculés / Data Marts (Approche Avancée) :** Pour les KPIs très consultés, une tâche CRON pourrait précalculer quotidiennement ou hebdomadairement les agrégats et les stocker dans des tables de résumé. Les dashboards liraient alors ces tables de résumé, beaucoup plus rapides.
            *   **Limitation des Plages de Données :** Encourager l'utilisation de filtres de date/année pour limiter le volume de données traité par chaque requête.
        *   **Définition Claire des KPIs :** Les indicateurs doivent être bien définis, compris par tous, et réellement utiles.
        *   **Capacités d'Export :** Essentiel pour permettre des analyses plus poussées hors système ou pour l'intégration dans des rapports institutionnels.
        *   **Sécurité d'Accès aux Données :** Même pour les rapports agrégés, s'assurer que les données sensibles sont correctement anonymisées ou que l'accès aux rapports est restreint selon les `id_niveau_acces_donne` de l'administrateur consultant (si plusieurs admins avec des portées différentes).

La section Reporting & Analytique apporte une valeur ajoutée significative en transformant les données transactionnelles en insights actionnables, mais sa mise en œuvre demande une réflexion approfondie sur la performance et la pertinence des informations fournies.

---
Ceci conclut la description exhaustive du Module Administration de A à G, en tenant compte de toutes les spécifications et en visant un niveau de détail extrême. Ce document devrait servir de base solide pour la conception et l'implémentation.


