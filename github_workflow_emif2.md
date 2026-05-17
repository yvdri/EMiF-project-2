# Guide de Travail Collaboratif GitHub — EMiF Project 2

> Ce guide explique **toutes les commandes et actions GitHub** nécessaires pour travailler efficacement en groupe sur ce projet.

---

## Table des matières

1. [Installation et configuration initiale](#1-installation-et-configuration-initiale)
2. [Cloner le repository](#2-cloner-le-repository)
3. [Comprendre les branches](#3-comprendre-les-branches)
4. [Workflow quotidien](#4-workflow-quotidien)
5. [Les commandes Git essentielles](#5-les-commandes-git-essentielles)
6. [Pull Requests — comment soumettre son travail](#6-pull-requests--comment-soumettre-son-travail)
7. [Résoudre les conflits](#7-résoudre-les-conflits)
8. [Bonnes pratiques](#8-bonnes-pratiques)
9. [Glossaire](#9-glossaire)

---

## 1. Installation et configuration initiale

### Installer Git

- **Windows** : Télécharger sur https://git-scm.com/download/win
- **Mac** : Déjà installé, ou via `brew install git`
- **Linux** : `sudo apt install git`

### Configurer ton identité Git (à faire une seule fois)

```bash
git config --global user.name "Ton Prénom Nom"
git config --global user.email "ton.email@example.com"
```

> ⚠️ Utilise le même email que ton compte GitHub.

---

## 2. Cloner le repository

La commande `git clone` télécharge le repository sur ton ordinateur.

```bash
git clone https://github.com/yvdri/EMiF-project-2.git
cd EMiF-project-2
```

**Ce que fait cette commande :**
- `git clone [URL]` — télécharge tout le projet (historique inclus)
- `cd EMiF-project-2` — se déplace dans le dossier créé

> Tu n'effectues cette étape qu'**une seule fois** au début.

---

## 3. Comprendre les branches

Une **branche** est une copie isolée du projet où tu peux travailler sans affecter le reste de l'équipe.

```
main (branche principale — toujours stable)
  ├── feature/analyse-donnees     ← ta branche de travail
  ├── feature/modele-regression   ← branche d'un camarade
  └── fix/correction-bug          ← correction d'un bug
```

**Règle d'or :** On ne travaille **jamais directement sur `main`**. On crée toujours une branche.

---

## 4. Workflow quotidien

Voici les étapes à suivre à chaque session de travail :

### Étape 1 — Mettre à jour sa copie locale

Avant de commencer à travailler, récupère les dernières modifications de l'équipe :

```bash
git checkout main
git pull origin main
```

**Ce que font ces commandes :**
- `git checkout main` — bascule sur la branche principale
- `git pull origin main` — télécharge les dernières modifications depuis GitHub

---

### Étape 2 — Créer ou basculer sur ta branche

**Créer une nouvelle branche :**
```bash
git checkout -b feature/nom-de-ta-feature
```

Exemples de noms de branches :
```bash
git checkout -b feature/analyse-portefeuille
git checkout -b feature/visualisation-graphiques
git checkout -b fix/correction-calcul-rendement
```

**Basculer sur une branche existante :**
```bash
git checkout feature/nom-de-ta-feature
```

---

### Étape 3 — Travailler et sauvegarder tes modifications

Après avoir modifié ou créé des fichiers :

```bash
# Voir quels fichiers ont changé
git status

# Ajouter les fichiers à sauvegarder
git add nom_du_fichier.py
# OU ajouter tous les fichiers modifiés
git add .

# Créer un commit (sauvegarde avec message)
git commit -m "feat: description courte de ce que tu as fait"
```

**Ce que font ces commandes :**
- `git status` — montre les fichiers modifiés (rouge = non sauvegardé, vert = prêt à commit)
- `git add` — sélectionne les fichiers à inclure dans la sauvegarde
- `git commit -m "..."` — crée une sauvegarde avec un message explicatif

**Convention pour les messages de commit :**

| Préfixe | Quand l'utiliser |
|---------|-----------------|
| `feat:` | Nouvelle fonctionnalité |
| `fix:` | Correction d'un bug |
| `docs:` | Modification de documentation |
| `data:` | Ajout ou modification de données |
| `refactor:` | Réorganisation du code sans changer la logique |

Exemples :
```
feat: ajout du modèle de régression linéaire
fix: correction du calcul de la variance
docs: mise à jour du README avec les instructions
data: ajout des données de marché Q1 2024
```

---

### Étape 4 — Envoyer ta branche sur GitHub

```bash
git push origin feature/nom-de-ta-feature
```

**Ce que fait cette commande :**
- `git push` — envoie tes commits locaux vers GitHub
- `origin` — désigne le repository GitHub distant
- `feature/nom-de-ta-feature` — la branche que tu envoies

---

## 5. Les commandes Git essentielles

### Voir l'état du projet

```bash
# Voir les fichiers modifiés
git status

# Voir l'historique des commits
git log --oneline

# Voir les différences non sauvegardées
git diff
```

### Gérer les branches

```bash
# Lister toutes les branches locales
git branch

# Lister les branches distantes (GitHub)
git branch -r

# Supprimer une branche locale (après merge)
git branch -d feature/nom-de-ta-feature
```

### Récupérer les modifications

```bash
# Récupérer et fusionner les dernières modifications
git pull origin main

# Récupérer sans fusionner (pour voir ce qui arrive)
git fetch origin
```

### Annuler des modifications

```bash
# Annuler les modifications d'un fichier non encore committé
git checkout -- nom_du_fichier.py

# Défaire le dernier commit (en gardant les modifications)
git reset HEAD~1

# Voir un commit spécifique
git show abc1234
```

---

## 6. Pull Requests — comment soumettre son travail

Une **Pull Request (PR)** est une demande de fusionner ta branche dans `main`. C'est le moyen de faire relire son travail par l'équipe.

### Comment créer une Pull Request

1. Va sur **https://github.com/yvdri/EMiF-project-2**
2. Tu verras une bannière jaune "Compare & pull request" — clique dessus
3. Remplis le formulaire :
   - **Titre** : ce que tu as fait (ex: `feat: ajout modèle de régression`)
   - **Description** : explique les changements, ce qui a été testé
4. Clique **Create pull request**
5. Un camarade relit et approuve (ou demande des modifications)
6. Une fois approuvé → **Merge pull request**

### Après le merge

```bash
# Revenir sur main et récupérer les nouvelles modifications
git checkout main
git pull origin main

# Supprimer ta branche locale (elle est fusionnée, plus besoin)
git branch -d feature/nom-de-ta-feature
```

---

## 7. Résoudre les conflits

Un **conflit** survient quand deux personnes ont modifié la même partie d'un fichier. Git ne sait pas quelle version choisir.

### Comment ça se présente dans le fichier

```python
<<<<<<< HEAD
# Ton code (ta version locale)
rendement = calcul_rendement(prix)
=======
# Code de ton camarade (version de GitHub)
rendement = prix.pct_change().mean()
>>>>>>> feature/analyse-donnees
```

### Comment résoudre

1. Ouvre le fichier dans ton éditeur
2. Choisis quelle version garder (ou combine les deux)
3. Supprime les marqueurs `<<<<<<<`, `=======`, `>>>>>>>`
4. Sauvegarde, puis :

```bash
git add nom_du_fichier.py
git commit -m "fix: résolution du conflit sur calcul_rendement"
```

---

## 8. Bonnes pratiques

### ✅ À faire
- **Toujours** faire `git pull origin main` avant de commencer
- Créer **une branche par fonctionnalité** ou par tâche
- Faire des commits **petits et fréquents** avec des messages clairs
- **Relire** les Pull Requests de tes camarades
- Mettre à jour le README si tu ajoutes quelque chose d'important

### ❌ À éviter
- Ne **jamais** pusher directement sur `main`
- Ne pas faire des commits avec des messages vagues comme "modif" ou "truc"
- Ne pas committer des fichiers inutiles (`.DS_Store`, `__pycache__/`, etc.)
- Ne pas laisser des branches ouvertes après merge

### .gitignore — fichiers à ne pas versionner

Le fichier `.gitignore` liste les fichiers que Git ignore automatiquement :

```gitignore
# Python
__pycache__/
*.pyc
*.pyo
.env
venv/
.venv/

# Jupyter
.ipynb_checkpoints/

# Données sensibles
data/raw/
*.csv
*.xlsx

# Système
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
```

---

## 9. Glossaire

| Terme | Définition |
|-------|-----------|
| **Repository (repo)** | Le projet complet avec tout l'historique des modifications |
| **Clone** | Télécharger le repo sur son ordinateur |
| **Branch (branche)** | Copie isolée du projet pour travailler sans affecter les autres |
| **Commit** | Une sauvegarde des modifications avec un message explicatif |
| **Push** | Envoyer ses commits locaux vers GitHub |
| **Pull** | Récupérer les commits de GitHub vers son ordinateur |
| **Merge** | Fusionner une branche dans une autre |
| **Pull Request (PR)** | Demande de fusion avec revue de code par l'équipe |
| **Conflit** | Quand deux personnes ont modifié le même endroit dans un fichier |
| **Origin** | Nom par défaut du repository distant sur GitHub |
| **Main** | La branche principale, toujours stable et fonctionnelle |
| **HEAD** | Le commit actuel sur lequel tu te trouves |
| **Stage / Index** | Zone de transit avant un commit (`git add` y dépose les fichiers) |
| **Fetch** | Récupérer les infos de GitHub sans les fusionner |

---

## Résumé express — Les 6 commandes du quotidien

```bash
# 1. Mettre à jour
git pull origin main

# 2. Créer/changer de branche
git checkout -b feature/ma-feature

# 3. Voir ce qui a changé
git status

# 4. Préparer les fichiers
git add .

# 5. Sauvegarder
git commit -m "feat: description claire"

# 6. Envoyer sur GitHub
git push origin feature/ma-feature
```

---

*Repo GitHub : https://github.com/yvdri/EMiF-project-2*