<div align="center">

<a href="README.md"><img src="https://img.shields.io/badge/🇬🇧_English-555?style=for-the-badge" /></a>
<a href="README.fr.md"><img src="https://img.shields.io/badge/🇫🇷_Français-2d6a2d?style=for-the-badge" /></a>
<a href="README.ar.md"><img src="https://img.shields.io/badge/🇲🇦_العربية-555?style=for-the-badge" /></a>

<br/><br/>

<img src="assets/performance_comparison.png" width="720"/>

<h1>🌿 PlantDoc AI System</h1>

<p>Diagnostic automatisé des maladies foliaires — SVM+LBP vs CNN MobileNetV2, avec interface web d'inférence en temps réel.</p>

**DUT Génie Informatique · Module : Python / AI · 2025–2026**

*Abderrahmane Aboutalib · Anas ElMarihi · Mohammed Bziz*
*Sous la direction de Pr. Al Semaa — EST Sidi Bennour, Université Chouaïb Doukkali*

</div>

---

## Présentation

Ce projet construit et compare deux modèles de machine learning pour la classification des maladies foliaires, sur le jeu de données [PlantVillage](https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset) filtré sur **Tomate** et **Pommier** (14 classes). Le meilleur modèle est ensuite déployé comme API REST et consommé par une interface web monopage.

| Modèle | Approche | Précision Validation |
|---|---|---|
| SVM | Features LBP (histogramme 26 dimensions) | 34,77 % |
| **CNN** | MobileNetV2 + Transfer Learning (5 epochs) | **91,48 %** |

---

## Structure du Dépôt

```
PlantDoc-AI/
├── colab/
│   ├── plantdoc_pipeline.ipynb   ← notebook Google Colab complet
│   └── plantdoc_pipeline.py      ← toutes les cellules fusionnées (référence)
├── web/
│   └── index.html                ← interface web PlantVision (monopage)
├── report/
│   └── PlantDoc_AI_Report.pdf
├── presentation/
│   └── PlantDoc_AI_Slides.pptx
├── assets/
│   └── performance_comparison.png
└── README.md
```

---

## Comment Lancer

> Tout fonctionne dans **Google Colab** — aucune installation locale requise.

**1 — Ouvrir le notebook**
Importer `colab/plantdoc_pipeline.ipynb` dans [Google Colab](https://colab.research.google.com/) et exécuter les cellules dans l'ordre.

**2 — Les cellules en bref**

| Cellule | Action |
|---|---|
| 1 | Montage Google Drive · Téléchargement dataset via Kaggle API |
| 2 | Filtrage dossiers Tomate/Pommier · Construction `ImageDataGenerator` |
| 3 | Extraction features LBP · Entraînement et sauvegarde SVM |
| 4 | Construction CNN MobileNetV2 · 5 epochs · Sauvegarde `.h5` |
| 5 | Tracé des courbes d'accuracy · Comparaison SVM vs CNN |
| 6 | Lancement serveur Flask + tunnel ngrok → copier l'URL |

**3 — Utiliser l'interface web**
1. Ouvrir `web/index.html` dans n'importe quel navigateur
2. Coller l'URL ngrok dans le champ **COLAB URL** en haut de la page
3. Déposer une image `.jpg` ou `.png` d'une feuille → **Analyze Leaf**

> ⚠️ L'URL ngrok change à chaque redémarrage de session Colab.

---

## Stack Technique

`Python` · `TensorFlow / Keras` · `scikit-learn` · `scikit-image` · `OpenCV` · `Flask` · `pyngrok` · `Matplotlib` · `Google Colab` · `HTML / CSS / JS`

---

## Résultats Clés

- **Écart de +56,7 points** entre SVM (34,77 %) et CNN (91,48 %)
- CNN entraîné en ~10–20 min sur GPU T4 gratuit avec seulement **17 934 paramètres entraînables**
- Le Transfer Learning depuis ImageNet permet une haute précision en seulement 5 epochs
- L'accuracy de validation suit de près celle d'entraînement — pas de sur-apprentissage significatif

---

## Note .gitignore

Les fichiers modèles (`.h5`, `.pkl`) et les dossiers du dataset brut sont exclus du dépôt pour raisons de taille. Ils sont régénérés en exécutant le notebook depuis la Cellule 1.