# TP5 — Examen de TP en Compétences

<div align="center">

![Module](https://img.shields.io/badge/ETRS606-TP5_Examen-0088CC?style=flat-square)
![Pitch](https://img.shields.io/badge/Pitch-3_minutes-FF6F00?style=flat-square)
![Demo](https://img.shields.io/badge/Démo-Live-4CAF50?style=flat-square)
![Site](https://img.shields.io/badge/GitHub_Pages-Live_Dashboard-blue?style=flat-square)

</div>

---

## 👥 Équipe

**Abdelnour ALEM · Faouzi MATMATI · Sophian MANGANELLO**  
L3 TRI — Université Savoie Mont Blanc | ETRS606 : IA Embarquée

---

## Introduction

Ce TP5 constitue l'évaluation finale du module ETRS606. Il prend la forme d'un **examen de TP par compétences** combinant une démonstration technique du système développé au fil des TPs et un pitch oral de 3 minutes présentant le produit final.

Le système présenté est une **station météo intelligente embarquée** basée sur la carte NUCLEO-N657X0, capable d'acquérir des données environnementales, de les classifier localement via un réseau de neurones, et de les transmettre vers le Cloud avec visualisation temps réel sur un dashboard web.

---

## Compétences Évaluées

| Code | Compétence | Support d'évaluation |
|------|-----------|---------------------|
| `TR_IMPLEMENT` | Bonnes pratiques de déploiement de réseaux et solutions logicielles | Code GitHub, architecture système |
| `E_IMPLEMENT` | Implémenter une solution IA embarquée sur STM32 | Démonstration live de la carte |
| `P_TEAM` | S'organiser et collaborer en équipe multidisciplinaire | GitHub collaboratif, répartition des tâches |
| `P_TEDS` | Transition écologique pour un développement soutenable | Analyse consommation, choix Edge vs Cloud |
| `C_ORAL` | Présentation orale convaincante de 3 min (format pitch) | Pitch produit lors du passage |

---

## Le Produit : Station Météo Edge AI

### Concept

Une station météo embarquée autonome qui :
1. **Acquiert** les données physiques en temps réel (température, humidité, pression) via des capteurs MEMS sur bus I²C
2. **Classifie** localement l'état météo (Beau Temps / Pluvieux / Orageux) grâce à un réseau de neurones déployé sur le CPU Cortex-M33 via X-CUBE-AI
3. **Transmet** les données et le verdict IA vers le Cloud ThingSpeak toutes les 20 secondes
4. **Visualise** tout en temps réel sur un dashboard web public

### Architecture Système Complète

```
┌─────────────────────────────────────────┐
│           NUCLEO-N657X0                 │
│                                         │
│  X-NUCLEO-IKS01A3 (I²C)               │
│  ├── HTS221  → Temp + Humidité         │
│  ├── LPS22HH → Pression               │
│  └── LSM6DSO → Accélération           │
│                                         │
│  X-CUBE-AI (CPU Cortex-M33)           │
│  └── meteostat_v3 (707 params, 2.8Ko) │
│      → Beau_Temps / Pluvieux / Orageux │
│                                         │
│  NetXDuo (Azure RTOS)                  │
│  └── TCP/HTTP → api.thingspeak.com    │
└──────────────┬──────────────────────────┘
               │ Ethernet RJ45
               ▼
┌─────────────────────────────┐
│     ThingSpeak Cloud        │
│  Field 1 : Température      │
│  Field 2 : Humidité         │
│  Field 3 : Pression         │
│  Field 4 : Classe IA        │
│  TalkBack API : commandes   │
└──────────────┬──────────────┘
               │ API REST
               ▼
┌─────────────────────────────┐
│   Dashboard Web (GitHub     │
│   Pages) — Temps Réel       │
│   fma-cmd.github.io/        │
│   station-meteo-stm32/      │
└─────────────────────────────┘
```

### Lien Dashboard

🌐 **[fma-cmd.github.io/station-meteo-stm32](https://fma-cmd.github.io/station-meteo-stm32/)**

---

## Structure du Pitch (3 minutes)

### 1. Accroche (20 sec)
> *"Et si votre carte STM32 pouvait prédire la météo toute seule, sans connexion Cloud, pour moins d'1 watt ?"*

### 2. Le problème (30 sec)
Les systèmes météo connectés classiques dépendent entièrement du Cloud pour l'intelligence : latence réseau, coût énergétique des serveurs, indisponibilité hors connexion. Pour des applications embarquées sur batterie ou en zone isolée, ce modèle est inadapté.

### 3. Notre solution (60 sec)
Une station météo **Edge AI** : le modèle de classification tourne directement sur le microcontrôleur. Les données sont acquises via I²C, normalisées, et passées à un MLP de 707 paramètres (2.8 Ko) entraîné sur des données météo réelles de la région Savoie. Le résultat est immédiat, local, et ne dépend d'aucun serveur pour le calcul.

### 4. Démonstration (50 sec)
- La carte lit les capteurs et affiche le verdict IA sur la console UART
- ThingSpeak reçoit les données en temps réel
- Le dashboard web montre la classification et la confiance en direct
- L'historique TalkBack confirme les commandes émises

### 5. Bilan & Transition écologique (20 sec)
Consommation totale mesurée : **1.079 W** pour le système complet. L'inférence locale évite les allers-retours réseau et supprime le coût énergétique côté serveur. Le modèle est 100× plus petit qu'un modèle Cloud équivalent tout en produisant le même résultat.

---

## Démonstration Technique

### Ce qui est montré lors du passage

| Élément | Description |
|---------|-------------|
| **Carte + Shield** | NUCLEO-N657X0 + X-NUCLEO-IKS01A3 alimentés et connectés en Ethernet |
| **Console UART** | Affichage des lectures capteurs et verdict IA en temps réel |
| **Dashboard ThingSpeak** | Canal "Station Meteo N657" avec courbes T, H, P et Field 4 (classe IA) |
| **Dashboard Web** | [fma-cmd.github.io/station-meteo-stm32](https://fma-cmd.github.io/station-meteo-stm32/) — verdict, confiance, historique, prévisions |
| **TalkBack** | File de commandes `Beau_Temps` / `Pluvieux` / `Orageux` en temps réel |
| **Multimètre** | Mesure de consommation : 0.166 A @ 6.5 V = **1.079 W** |

---

## Synthèse des TPs

| TP | Titre | Compétence principale | Résultat clé |
|----|-------|----------------------|-------------|
| **TP1** | Problème MNIST | Comprendre les MLP | Accuracy ~97.6% avec Tanh + Adam |
| **TP2** | Interface Capteurs & STM32 | Programmation embarquée bas niveau | Lecture I²C, ping DNS fonctionnel |
| **TP3** | Connectivité Cloud | IoT + entraînement Meteostat | Pipeline ThingSpeak + TalkBack opérationnel |
| **TP4** | Cloud vs Edge AI | Déploiement IA embarquée | Inférence locale, 1.079 W, dashboard web |
| **TP5** | Examen de compétences | Synthèse + communication | Démonstration live + pitch |

---

## Analyse de Soutenabilité (P_TEDS)

### Comparaison énergétique Edge vs Cloud

| Approche | Lieu de calcul | Consommation estimée |
|----------|---------------|---------------------|
| **Cloud AI** | Serveur distant (MathWorks) | ~200–500 W (serveur partagé) |
| **Edge AI** | STM32N6 CPU local | **1.079 W** (système complet) |

L'approche Edge AI est intrinsèquement plus sobre pour ce cas d'usage : le calcul se fait au plus près de la source de données, sans transfert réseau inutile ni infrastructure serveur dédiée.

### Sobriété du modèle

- **707 paramètres** — modèle minimal, conçu pour les contraintes embarquées
- **2 828 octets** — empreinte Flash négligeable
- **3 classes** — choix délibéré pour maximiser la précision sur peu d'entrées
- Pas de quantification int8 appliquée dans cette version : une étape supplémentaire d'optimisation possible pour réduire encore la consommation

### Limites et pistes d'amélioration

- Activer le **NPU Neural-ART** (600 GOPS) pour l'inférence afin de réduire la consommation CPU
- Appliquer la **quantification int8** pour diviser par 4 la taille du modèle
- Implémenter la **mise en veille** entre les cycles de mesure (20 secondes d'attente active = gaspillage)
- Étendre à **5 classes** (ajout brouillard, vent fort) avec plus de données d'entraînement

---

## Dépôt GitHub

🔗 **[github.com/matmatifaouzi208-sketch/TP1_MNIST_IA_Embarquee](https://github.com/matmatifaouzi208-sketch/TP1_MNIST_IA_Embarquee)**

```
ETRS606_IA_Embarquee/
├── README.md         ← Dépôt principal
├── TP1/README.md     ← MNIST — MLP, fonctions d'activation, optimiseurs
├── TP2/README.md     ← Capteurs I²C, chenillard, réseau Ethernet
├── TP3/README.md     ← ThingSpeak, entraînement Meteostat, TalkBack
├── TP4/README.md     ← Edge AI, X-CUBE-AI, consommation, dashboard web
└── TP5/README.md     ← Examen de compétences (ce fichier)
```

---

## Conclusion

Ce module ETRS606 a permis de parcourir l'intégralité de la chaîne Edge AI : de la théorie des réseaux de neurones (TP1) à leur déploiement physique sur microcontrôleur (TP4), en passant par la programmation embarquée bas niveau (TP2) et la connectivité Cloud (TP3).

Le système final — une station météo intelligente à moins d'1 watt — illustre concrètement que l'IA embarquée n'est pertinente que lorsqu'elle apporte un bénéfice clair face à une solution déterministe classique. La relation non linéaire entre température, humidité et état météo justifie ici l'utilisation d'un MLP, contrairement au cas sin(x) où l'IA serait surdimensionnée.

L'enseignement majeur : **l'IA embarquée, c'est choisir le bon outil pour le bon problème**.

---

## Ressources

- 🌐 [Dashboard temps réel](https://fma-cmd.github.io/station-meteo-stm32/)
- 📂 [TP1 — MNIST](../TP1/README.md)
- 📂 [TP2 — Interface Capteurs](../TP2/README.md)
- 📂 [TP3 — Connectivité Cloud](../TP3/README.md)
- 📂 [TP4 — Cloud vs Edge AI](../TP4/README.md)
- 📄 [Sujet TP5 officiel — ETRS606](../docs/ETRS606_TP5.pdf)
