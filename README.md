# 🔍 Détection de Fraudes par Chèque

**Projet de Fouille de Données Massives - Master 2 SISE**  
*Université Lumière Lyon 2 - Février 2026*

---

## 👥 Auteurs

- **Yassine CHENIOUR**
- **Modou MBOUP**

---

## 📋 Description

Ce projet porte sur la **détection de fraudes bancaires par chèque** dans un contexte de données fortement déséquilibrées. Nous analysons 4,6 millions de transactions réelles provenant de la grande distribution française (février-novembre 2017), avec un taux de fraude de seulement 0,60% (ratio 1:165).

### 🎯 Objectifs

1. **Partie 1** : Maximiser la F-mesure en comparant plusieurs approches de classification
2. **Partie 2** : Optimiser le profit en intégrant une matrice de coûts métier réaliste

### 🏆 Résultats principaux

- **Meilleure F-mesure** : 0.148 (XGBoost avec seuil ajusté) → +85% vs littérature
- **Meilleure marge** : 2 055 747€ sur 3 mois (XGBoost avec seuil ajusté pour profit)
- **Insight clé** : Optimiser la F-mesure ≠ Maximiser le profit (+2,3% de gain)

---

## 📁 Structure du projet

```
SISE_FraudsDetection/
├── README.md                              # Ce fichier
├── Rapport_FDM_MBOUP_CHENIOUR.pdf        # Rapport complet (34 pages)
├── .gitignore
│
├── data/
│   └── Data_Projet1.txt                  # Dataset brut (4,6M transactions)
│
├── notebooks/
│   ├── preprocessing.ipynb                # Prétraitement et analyse exploratoire
│   ├── modelisation.ipynb                 # Partie 1 : Optimisation F-mesure
│   └── maximisation_de_la_marge.ipynb    # Partie 2 : Optimisation profit
│
├── results/
│   ├── resultats_modelisation_partie1.csv
│   ├── resultats_maximisation_de_la_marge.csv
│   ├── resume_modelisation.txt
│   └── resultats_maximisation_de_la_marge.txt
│
└── docs/
    ├── sujet.pdf                          # Énoncé du projet
    ├── rapport_FDM.zip                    # Sources LaTeX du rapport
    └── rapport_FDM/
        ├── main.tex
        ├── references.bib
        ├── sections/                      # Fichiers LaTeX par section
        │   ├── 0_resume.tex
        │   ├── 1_introduction.tex
        │   ├── 2_analyse_donnees.tex
        │   ├── 3_methodologie.tex
        │   ├── 4_experiences.tex
        │   └── 5_conclusion.tex
        └── figures/                       # Visualisations du rapport
            ├── confusion_matrix_xgboost.png
            ├── correlation_matrix.png
            ├── distributions_VC.png
            ├── distribution_classes.png
            ├── distribution_montants.png
            ├── evolution_temporelle_fraudes.png
            ├── resultats_partie1_complet.png
            └── resultats_partie2_complet.png
```

---

## 🚀 Installation

### Prérequis

- Python 3.11+
- Jupyter Notebook

### Dépendances

```bash
pip install pandas numpy scikit-learn xgboost imbalanced-learn matplotlib seaborn
```

---

## 📊 Dataset

- **Source** : Grande distribution française (collaboration FNCI/Banque de France)
- **Période** : Février-novembre 2017
- **Taille** : 4 645 652 transactions
- **Variables** : 23 variables (20 features après prétraitement)
- **Déséquilibre** : 0,64% fraudes (29 831 sur 4,6M)
- **Split temporel** : 
  - Train : Février-Août 2017 (7 mois)
  - Test : Septembre-Novembre 2017 (3 mois)

---

## 🛠️ Méthodologie

### Approches testées (9 modèles)

**Techniques de rééchantillonnage :**
- SMOTE + Logistic Regression
- UnderSampling + Logistic Regression
- XGBoost + SMOTE

**Approches cost-sensitive :**
- Logistic Regression + class_weight
- Random Forest + class_weight
- Balanced Random Forest
- XGBoost + scale_pos_weight

**Optimisation du seuil :**
- XGBoost avec ajustement du seuil de décision

### Algorithmes utilisés

- Régression Logistique (baseline)
- Random Forest
- XGBoost (meilleur modèle)

---

## 📈 Résultats

### Partie 1 : Optimisation F-mesure

| Modèle | F-mesure | Précision | Rappel |
|--------|----------|-----------|--------|
| **XGBoost (seuil=0.939)** | **0.148** | 0.184 | 0.124 |
| XGBoost + SMOTE | 0.130 | 0.157 | 0.112 |
| SMOTE + LogReg | 0.094 | 0.156 | 0.067 |

### Partie 2 : Optimisation Profit

| Modèle | Marge (€) | F1 | Précision | Rappel |
|--------|-----------|----|-----------|---------| 
| **XGBoost (seuil=0.85)** | **2 055 747** | 0.104 | 0.065 | 0.257 |
| UnderSampling + LogReg | 2 040 856 | 0.067 | 0.037 | 0.356 |
| XGBoost + SMOTE | 2 018 959 | 0.136 | 0.127 | 0.147 |

### Comparaison F-mesure vs Profit

- **Gain de marge** : +45 891€ (+2,3%) en optimisant directement le profit
- **Conclusion** : La F-mesure n'est pas un proxy fiable du profit réel

---

## 🔧 Utilisation

### 1. Prétraitement des données

```bash
jupyter notebook notebooks/preprocessing.ipynb
```

Contenu :
- Conversion des formats numériques (notation européenne)
- Analyse exploratoire (distributions, corrélations)
- Split temporel train/test
- Exclusion des variables redondantes (VerifianceCPT2/3)

### 2. Partie 1 - Optimisation F-mesure

```bash
jupyter notebook notebooks/modelisation.ipynb
```

Compare 9 approches et identifie le modèle maximisant la F-mesure.

### 3. Partie 2 - Optimisation Profit

```bash
jupyter notebook notebooks/maximisation_de_la_marge.ipynb
```

Intègre la matrice de coûts métier et optimise la marge commerciale.

### 4. Consulter les résultats

Les résultats détaillés sont disponibles dans le dossier `results/` :
- `resultats_modelisation_partie1.csv` : Métriques Partie 1
- `resultats_maximisation_de_la_marge.csv` : Métriques Partie 2
- Fichiers `.txt` : Résumés textuels

---

## 📄 Documentation complète

Le **rapport complet (34 pages)** est disponible à la racine : `Rapport_FDM_MBOUP_CHENIOUR.pdf`

Contenu du rapport :
- Résumé exécutif
- Introduction et état de l'art
- Analyse exploratoire approfondie
- Méthodologie détaillée (algorithmes, rééchantillonnage, métriques)
- Résultats comparatifs des 9 modèles
- Analyses statistiques et visualisations
- Limites identifiées et perspectives d'amélioration

**Sources LaTeX** : Disponibles dans `docs/rapport_FDM/` pour reproductibilité complète.

---

## 🔑 Points clés

✅ **9 modèles** testés systématiquement  
✅ **F-mesure** : 0.148 (+85% vs littérature)  
✅ **Profit** : 2,06M€ sur 3 mois (~8,2M€/an)  
✅ **Démonstration** empirique : F-mesure ≠ Profit  
✅ **Dataset réel** de 4,6M transactions  

---

## 📚 Références

- Breiman, L. (2001). Random Forests. *Machine Learning*, 45(1), 5-32.
- Chawla, N. V. et al. (2002). SMOTE: Synthetic Minority Over-sampling Technique. *JAIR*, 16, 321-357.
- Chen, T. & Guestrin, C. (2016). XGBoost: A Scalable Tree Boosting System. *KDD'16*.
- Metzler, G. (2019). Learning from Imbalanced Data. Thèse, Université de Lyon.

---

## 📧 Contact

Pour toute question concernant ce projet :
- Yassine CHENIOUR
- Modou MBOUP

**Formation** : Master 2 Informatique - SISE  
**Université** : Lumière Lyon 2  
**Date** : Février 2026

---

## 📝 Licence

Ce projet est réalisé dans un cadre académique (Master 2 SISE - Université Lyon 2).

---

⭐ **Note** : Ce projet a été réalisé avec des données réelles en collaboration avec la FNCI et la Banque de France.
