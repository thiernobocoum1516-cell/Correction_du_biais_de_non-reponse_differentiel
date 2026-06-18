# Correction du biais de non-réponse différentiel

## Application sur les données de l’Enquête Ménage au Ghana (GLSS)

### Auteur
**Thierno BOCOUM** – Élève Ingénieur Statisticien Économiste (ISEP 2)  
ENSAE Pierre Ndiaye / Agence nationale de la statistique et de la démographie (ANSD)  
Sous la supervision de M. Hamady DIALLO

---

### Description
Ce projet a été réalisé dans le cadre du module **Traitement Statistique avec R** (Thème 13).  
L'objectif est de simuler un mécanisme de non-réponse de type **MNAR (Missing Not At Random)** en forme de "U" à partir des microdonnées du **Ghana Living Standards Survey (GLSS)**, d'en diagnostiquer l'impact sur les dépenses de consommation par tête, et de comparer trois méthodes correctives :

1. **IPW (Inverse Probability Weighting)** avec régression logistique de Firth.
2. **Imputation hot-deck stratifiée**.
3. **Bornes de Manski** (identification partielle).

---

### Structure du dépôt

├── README.md                      # Ce fichier
├── beamer.pdf                     # Présentation Beamer (soutenance)
├── Rapport_Projet_R.pdf           # Rapport complet en PDF
├── R/                             # Scripts R (pipeline d'analyse)
│   ├── 00_setup.R                 # Chargement des packages
│   ├── 01_import_nettoyage.R      # Import des données et suppression des NA
│   ├── 02_bootstrap_bruitage.R    # Extension bootstrap et bruitage
│   ├── 03_simulation_biais.R      # Simulation du modèle logistique MNAR
│   ├── 04_ipw.R                   # Estimation IPW (régression Firth, poids)
│   ├── 05_hotdeck.R               # Imputation hot-deck stratifiée
│   ├── 06_manski.R                # Calcul des bornes de Manski
│   └── 07_analyse_sensibilite.R   # Tableaux et graphique de synthèse
├── data/                          # Données (non incluses dans le dépôt)
│   └── glss_data.dta              # Fichier original .dta (à placer ici)
├── images/                        # Figures générées
│   ├── graphe_bruitage.pdf
│   ├── graphe_biais.pdf
│   └── graphe_complet.pdf
└── output/                        # Résultats (tableaux, logs)
    
## Prérequis

    R version 4.0 ou supérieure.

    RStudio (recommandé).

    Les packages R suivants (installer avec install.packages()) :

        haven, dplyr, ggplot2, survey, brglm2, kableExtra, knitr

## Instructions d'exécution

    Cloner le dépôt :
    bash

    git clone https://github.com/votre-utilisateur/votre-depot.git
    cd votre-depot

    Ajouter les données :
    Placer le fichier glss_data.dta dans le dossier data/.

    Exécuter l’analyse :
    Exécuter les scripts dans l’ordre :
    bash

    Rscript R/00_setup.R
    Rscript R/01_import_nettoyage.R
    Rscript R/02_bootstrap_bruitage.R
    Rscript R/03_simulation_biais.R
    Rscript R/04_ipw.R
    Rscript R/05_hotdeck.R
    Rscript R/06_manski.R
    Rscript R/07_analyse_sensibilite.R

    Générer le rapport :
    Compiler le document R Markdown (si disponible) avec rmarkdown::render().

## Résultats principaux

    Mécanisme simulé : MNAR en U, taux de non-réponse 34%.

    Biais diagnostiqué : Médiane et variance fortement biaisées (+154% et -75%), moyenne stable.

    Meilleure méthode : IPW + Firth corrige efficacement tous les indicateurs (moyenne restaurée, variance à 88%).

    Méthodes moins performantes : Hot-deck échoue sur la dispersion ; bornes de Manski donnent un intervalle large [92,0 ; 294,8].

## Références

    Manski, C. F. (2003). Partial Identification of Probability Distributions. Springer.

    Rubin, D. B. (1976). Inference and missing data. Biometrika, 63(3), 581-592.

    Seaman, S. R. & White, I. R. (2013). Review of inverse probability weighting for dealing with missing data. Statistical Methods in Medical Research, 22(3), 278-295.

