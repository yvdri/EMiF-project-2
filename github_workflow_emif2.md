# 📊 emf-project-2026
**Empirical Methods in Finance — Group Project 2026**

Bienvenue dans ce repository ! Ce guide est fait pour vous si c'est votre **premier projet collaboratif sur GitHub**. Lisez-le attentivement avant de commencer à travailler.

---

## 🧠 C'est quoi GitHub, en deux mots ?

GitHub est un endroit où on stocke le code **en ligne** et qui garde une **trace de toutes les modifications** faites par chaque membre du groupe. C'est comme Google Docs, mais pour du code — sauf qu'au lieu de modifier en temps réel, chaque personne travaille sur sa propre version locale, puis envoie ses changements.

Les concepts clés :
- **Repository (repo)** : le dossier du projet, hébergé sur GitHub
- **Clone** : copier le repo sur votre ordinateur
- **Commit** : enregistrer une modification avec un message
- **Push** : envoyer vos commits vers GitHub
- **Pull** : récupérer les dernières modifications de vos coéquipiers
- **Branch (branche)** : votre espace de travail personnel — expliqué en détail plus bas

---

## 🚀 Mise en place (à faire une seule fois)

### 1. Installer Git
Téléchargez Git sur https://git-scm.com/downloads et installez-le.

### 2. Configurer Git avec votre identité
```bash
git config --global user.name "Votre Prénom Nom"
git config --global user.email "votre@email.com"
```

### 3. Cloner le repository (télécharger le projet sur votre ordi)
```bash
git clone https://github.com/yvdri/emf-project-2026.git
cd emf-project-2026
```

---

## 🌿 Les branches — c'est quoi et pourquoi c'est indispensable ?

### Le problème sans branches

Imaginez que vous êtes 4 sur le projet. Alice travaille sur `analyse.py`, Bob aussi. Alice finit et envoie ses modifications. Bob envoie les siennes juste après — et **écrase le travail d'Alice** sans le vouloir. Tout son travail est perdu.

C'est exactement ce qui arrive quand tout le monde travaille sur la même branche `main`.

### La solution : chacun sa branche

Une branche, c'est **votre espace de travail personnel**. Ce n'est pas un fichier, ce n'est pas un dossier — c'est une copie isolée de tout le projet dans laquelle vous travaillez seul. Les autres ne voient pas vos modifications tant que vous ne les avez pas soumises. Et vous, vous ne risquez pas d'écraser leur travail.

La branche `main` = la version officielle et validée du projet. **On n'y touche jamais directement.**

---

## ✅ Le principe fondamental — à lire avant tout le reste

> **Chacun bosse sur sa propre branche → chacun push sur sa propre branche → on merge dans main → Git combine tout sans rien perdre.**

C'est vraiment aussi simple que ça. Voici ce que ça veut dire concrètement :

1. **Vous créez votre branche** : votre espace de travail isolé, personne d'autre ne le touche
2. **Vous travaillez et vous push** : vos modifications vont sur *votre branche* sur GitHub — `main` n'est pas touché du tout
3. **Vous créez une Pull Request** : vous proposez d'intégrer votre travail dans `main`
4. **On merge** : Git prend les modifications de votre branche et les **combine** dans `main` — il ne remplace pas, il ajoute

**Ce que Git fait lors du merge :** il compare fichier par fichier, ligne par ligne. Si Rijad a modifié `data_cleaning.py` et Alice a modifié `regression.py`, les deux fichiers sont intégrés sans problème. Si par hasard deux personnes ont modifié **exactement la même ligne du même fichier**, Git signale un conflit et demande à un humain de choisir — mais même là, rien n'est perdu.

**La seule règle** pour éviter les conflits : communiquez sur qui travaille sur quel fichier.

---

## 📖 Scénario complet — une session de travail réelle

> Voici exactement ce que fait **Rijad** un lundi matin pour travailler sur le nettoyage des données, sans gêner ses coéquipiers Alice, Bob et Charlie qui travaillent en parallèle.

---

### 🔵 Étape 1 — Ouvrir le terminal et aller dans le dossier du projet

```bash
cd emf-project-2026
```

> Si c'est la première fois, vous avez d'abord cloné le repo (voir section "Mise en place").

---

### 🔵 Étape 2 — Récupérer les dernières modifications de l'équipe

Avant de commencer à travailler, on s'assure d'avoir la version la plus récente du projet :

```bash
git checkout main
git pull origin main
```

> `git checkout main` : on s'assure d'être sur la branche principale.
> `git pull origin main` : on télécharge ce que les autres ont envoyé depuis la dernière fois.

**Pourquoi c'est important ?** Si Alice a ajouté un fichier hier soir et que vous ne faites pas `git pull`, vous travaillez sur une version ancienne du projet. Ça crée des conflits plus tard.

---

### 🔵 Étape 3 — Créer votre propre branche de travail

Maintenant on crée notre espace de travail personnel :

```bash
git checkout -b rijad/nettoyage-donnees
```

> Cette commande fait **deux choses en même temps** : elle crée la branche ET vous place dessus.
> Le nom `rijad/nettoyage-donnees` est juste une convention. Choisissez `prenom/ce-que-vous-faites`.

Pour vérifier que vous êtes bien sur votre branche :

```bash
git branch
```

Vous verrez quelque chose comme :

```
  main
* rijad/nettoyage-donnees
```

Le `*` indique la branche sur laquelle vous êtes. Si vous voyez `* rijad/nettoyage-donnees`, vous êtes au bon endroit. Vous pouvez travailler.

---

### 🔵 Étape 4 — Travailler normalement

Ouvrez VS Code, modifiez vos fichiers Python, vos notebooks Jupyter, etc. Tout ce que vous faites ici est **isolé dans votre branche**. Vous ne pouvez pas écraser le travail des autres, et les autres ne peuvent pas écraser le vôtre.

Par exemple, Rijad modifie `data_cleaning.py` et ajoute une fonction pour supprimer les valeurs manquantes.

Pendant ce temps, Alice travaille sur `regression.py` dans sa propre branche `alice/regression-ols`. Les deux peuvent travailler en parallèle sans se gêner.

---

### 🔵 Étape 5 — Sauvegarder son travail (commit)

Une fois que vous avez fait des modifications que vous voulez garder :

```bash
git status
```

Cette commande affiche les fichiers que vous avez modifiés. Vérifiez que c'est bien ce à quoi vous vous attendez.

Ensuite, on ajoute les fichiers et on fait un commit :

```bash
git add .
git commit -m "Ajout fonction suppression valeurs manquantes"
```

> Le message après `-m` doit décrire ce que vous avez fait, en une phrase courte. Vos coéquipiers liront ces messages pour comprendre ce qui a changé.

Vous pouvez faire autant de commits que vous voulez dans une même session. C'est même recommandé — sauvegardez souvent.

---

### 🔵 Étape 6 — Envoyer votre branche sur GitHub

Quand votre travail est prêt, envoyez-le :

```bash
git push origin rijad/nettoyage-donnees
```

Votre branche est maintenant visible sur GitHub, mais elle n'est **pas encore dans `main`**. Le projet officiel n'a pas été modifié. Vous devez d'abord passer par une Pull Request.

---

### 🔵 Étape 7 — Créer une Pull Request pour intégrer votre travail dans main

C'est l'étape où vous soumettez votre travail à l'équipe pour validation.

1. Allez sur https://github.com/yvdri/emf-project-2026
2. GitHub affiche une bannière en haut : **"rijad/nettoyage-donnees had recent pushes — Compare & pull request"**. Cliquez dessus.
3. Vous voyez un formulaire. Remplissez :
   - **Titre** : ce que vous avez fait (ex: "Nettoyage des valeurs manquantes")
   - **Description** : détails si nécessaire
4. Cliquez sur **"Create pull request"**

Un coéquipier peut maintenant relire votre code, laisser des commentaires, et quand tout le monde est d'accord :

5. Cliquez sur **"Merge pull request"** puis **"Confirm merge"**

✅ Votre travail est maintenant intégré dans `main`. Tout le monde peut le récupérer avec `git pull`.

---

### 🔵 Étape 8 — Nettoyer et revenir sur main pour la prochaine session

```bash
git checkout main
git pull origin main
```

Vous êtes de retour sur la version officielle, avec votre travail intégré. Prêt pour la prochaine tâche.

---

## 🗺️ Vue d'ensemble du flux de travail

```
                     ┌─────────────────────────────────────────┐
                     │              BRANCHE main               │
                     │    (version officielle du projet)        │
                     └────────────────┬────────────────────────┘
                                      │
              ┌───────────────────────┼───────────────────────┐
              │                       │                       │
              ▼                       ▼                       ▼
  rijad/nettoyage-donnees   alice/regression-ols    bob/visualisation
    (Rijad travaille)         (Alice travaille)      (Bob travaille)
    commit → commit           commit → commit        commit → commit
              │                       │                       │
              └───────────────────────┼───────────────────────┘
                                      │
                              Pull Request + Merge
                                      │
                                      ▼
                     ┌─────────────────────────────────────────┐
                     │   main mis à jour avec tout le travail  │
                     └─────────────────────────────────────────┘
```

---

## ❌ Les erreurs classiques et comment les éviter

**"J'ai oublié de créer une branche et j'ai travaillé directement sur main"**
> Avant de commencer, tapez toujours `git branch` pour vérifier où vous êtes. Si vous voyez `* main`, arrêtez-vous et créez une branche.

**"J'ai fait `git push` et ça m'a dit que j'étais en retard"**
> Quelqu'un a envoyé des modifications pendant que vous travailliez. Faites `git pull origin main` pour vous mettre à jour, puis recommencez votre push.

**"J'ai un conflit, je ne sais pas quoi faire"**
> Ne paniquez pas. Ouvrez le fichier en conflit, vous verrez des marqueurs comme :
```
<<<<<<< HEAD
votre version
=======
version du coéquipier
>>>>>>> main
```
> Gardez la version correcte (ou les deux si applicable), supprimez les marqueurs, puis faites `git add .` et `git commit`.

**"Je ne sais pas sur quelle branche je suis"**
> Tapez `git branch`. La ligne avec `*` devant est votre branche actuelle.

---

## 📋 Commandes de référence rapide

```bash
# 1er fois !!!! Début de session (toujours faire ça en premier)
git checkout main
git pull origin main
git checkout -b prenom/ma-tache 

# Toutes les fois d'après, debut de session, pour recup le main sur sa branche :
git checkout main # ICI on verifie si la version,joue et est correcte parce que si elle joue pas et qu'on fait les codes suivants ça ecrase notre branche avec le main (qui joue pas)
git checkout prenom/ma-tache 
git pull origin main


# Pendant le travail 
git branch                        # Vérifier sur quelle branche on est


# Fin de session (envoyer son travail)
git status                        # Voir les fichiers modifiés
git add .                         # Préparer tous les fichiers
git commit -m "message"           # Sauvegarder avec un message
git push origin prenom/ma-tache   # Envoyer sa branche sur GitHub
# Puis créer une Pull Request sur GitHub !!! donc faut faire ça sur Github c'est très important !! et ensuite faire la suite :

# Après le merge
git checkout main
git pull origin main
```

---

## 🗂️ Structure du projet

```
emf-project-2026/
│
├── data/               <- Données brutes (ne jamais modifier ces fichiers !)
├── notebooks/          <- Jupyter notebooks d'exploration
├── src/                <- Scripts Python propres et réutilisables
├── results/            <- Graphiques, tableaux de résultats
├── README.md           <- Ce fichier
└── .gitignore          <- Fichiers à ignorer (automatique)
```

---

## 👥 Inviter les membres du groupe

Settings → Collaborators → Add people → entrez leur email ou username GitHub.

---

## 🆘 En cas de problème

1. **Ne paniquez pas et ne forcez rien** — une mauvaise commande peut aggraver les choses
2. Tapez `git status` et `git branch` pour comprendre où vous en êtes
3. Cherchez le message d'erreur sur Google — les réponses existent toujours sur Stack Overflow
4. **Demandez à un coéquipier avant toute action irréversible** (avant tout `reset`, `force`, ou `rm`)

---

*README rédigé pour les membres du projet EMF 2026 — première utilisation de GitHub en groupe.*