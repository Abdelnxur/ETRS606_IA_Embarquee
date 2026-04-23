# ETRS606 : IA Embarquée — Dépôt Principal

<div align="center">

![Université Savoie Mont Blanc](https://img.shields.io/badge/USMB-L3%20TRI-004A8F?style=for-the-badge)
![Module](https://img.shields.io/badge/Module-ETRS606-0088CC?style=for-the-badge)
![Langage](https://img.shields.io/badge/Python-TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow)
![Carte](https://img.shields.io/badge/STM32-NUCLEO--N657X0-03234B?style=for-the-badge)

</div>

---

## 👥 Équipe

| Nom | Prénom |
|-----|--------|
| ALEM | Abdelnour |
| MATMATI | Faouzi |
| MANGANELLO | Sophian |

**Formation :** L3 TRI — Télécommunications et Réseaux Informatiques  
**Université :** Savoie Mont Blanc  
**Module :** ETRS606 — IA Embarquée (Edge AI)  
**Encadrant :** Pietro M. FERREIRA

---

## 📖 Description du Module

Ce dépôt regroupe l'ensemble des travaux pratiques et du projet réalisés dans le cadre du module **ETRS606 : IA Embarquée**. L'objectif est de concevoir des systèmes embarqués d'interface capteurs sous le paradigme des circuits neuromorphiques, à la convergence de la microélectronique et de l'intelligence artificielle.

Le module explore les compromis nécessaires pour déployer des réseaux de neurones sur des architectures matérielles contraintes (mémoire, complexité de calcul, précision, consommation énergétique).

---

## 🛠️ Matériel Utilisé

| Composant | Description |
|-----------|-------------|
| **NUCLEO-N657X0** | ARM Cortex-M33 @ 160 MHz, 320 Ko RAM, 512 Ko Flash, NPU Neural-ART (600 GOPS) |
| **X-NUCLEO-IKS01A3** | Shield capteurs MEMS : accéléromètre, gyroscope, magnétomètre, température, humidité, pression (bus I²C) |

---

## 📂 Structure du Dépôt

```
ETRS606_IA_Embarquee/
├── TP1/ETRS606_TP1.pdf          # Problème MNIST — Classification de chiffres manuscrits
├── TP2/          # Interface Capteurs & STM32 — Drivers I²C, LEDs, Ethernet
├── TP3/          # Connectivité Cloud — ThingSpeak, MQTT, entraînement Meteostat
├── TP4/          # Cloud vs Edge AI — MATLAB/ONNX et déploiement STM32N6
└── TP5/          # Examen de TP — Démonstration et pitch produit
```

---

## 📋 Résumé des TPs

### TP1 — Problème MNIST
Classification d'images de chiffres manuscrits (0–9) avec un réseau dense (MLP).  
Comparaison de fonctions d'activation (Softmax, ReLU, Tanh, Sigmoid), d'optimiseurs (SGD, Adam, RMSprop, Adagrad) et de fonctions coût.  
**Résultat clé :** Tanh avec Adam atteint ~97.6% de précision, `sparse_categorical_crossentropy` choisie.  
→ [Voir TP1](./TP1/TP1_README.md)

### TP2 — Interface Capteurs & STM32
Programmation embarquée bas niveau sur NUCLEO-N657X0 : chenillard LED, lecture des capteurs MEMS via I²C (HAL), communication réseau avec FreeRTOS + LWIP.  
→ [Voir TP2](./TP2/README.md)

### TP3 — Connectivité Cloud
Envoi de données capteurs vers ThingSpeak (REST/MQTT), visualisation MATLAB, entraînement d'un modèle Python/TensorFlow pour la classification météo (MeteoStat).  
→ [Voir TP3](./TP3/README.md)

### TP4 — Cloud vs Edge AI
Déploiement du modèle Meteostat via ONNX sur MATLAB/ThingSpeak (Cloud) et sur la carte STM32N6 via X-CUBE-AI (Edge). Comparaison latence, précision, consommation.  
→ [Voir TP4](./TP4/README.md)

### TP5 — Examen de TP (Compétences)
Démonstration finale du système embarqué et pitch oral de 3 minutes.  
→ [Voir TP5](./TP5/README.md)

---

## 🔑 Compétences Visées

| Code | Compétence |
|------|-----------|
| `TR_IMPLEMENT` | Respecter les bonnes pratiques de déploiement de réseaux et solutions logicielles |
| `E_IMPLEMENT` | Implémenter une solution IA embarquée sur cartes STM32 |
| `P_TEAM` | S'organiser et collaborer efficacement en équipe multidisciplinaire |
| `P_TEDS` | Prendre en compte la transition écologique pour un développement soutenable |
| `C_ORAL` | Structurer une présentation orale convaincante (format pitch 3 min) |

---

## 📚 Bibliographie

- Hope, T., Resheff, Y. S., & Lieder, I. (2017). *Learning TensorFlow*. O'Reilly. ISBN 9781491978511
- Chollet, F. (2018). *Deep Learning with Python*. Manning. ISBN 9781617294433
- Galvão, M. H., & Ferreira, P. M. (2024). *AIoT Guidebook*. [DOI: 10.5281/zenodo.12700232](https://doi.org/10.5281/zenodo.12700232)
