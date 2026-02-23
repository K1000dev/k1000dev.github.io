# Synthèse Git

<br>
> Synthèse Git faites par moi en feat. avec l'IA (jugez pas)
<br>

> Elle n'est pas complète à 100% mais j'estime qu'il y a l'essentiel pour éviter de faire de la merde

---

## 📐 1. Comprendre l’architecture Git

??? info "Git est distribué"
    Chaque développeur possède une copie complète du projet.

    - `Repository` : dossier contenant l’historique
    - `Commit` : snapshot du projet
    - `Branch` : ligne de développement
    - `main` : branche principale
    - `origin` : serveur distant (GitHub / GitLab)

---

## 🗂️ 2. Workflow standard pour ajouter une fonctionnalité 

> Lorsque vous voulez ajouter des fonctionnalités à partir d'un projet qui a été mis à jour

### Étapes dans l’ordre

#### 1. Se placer sur la branche principale

 ```bash
 git checkout main
 ```

#### 2. Récupérer la dernière version

```bash
git pull origin main
```

??? info Explication
    - `pull` = fetch + merge

        > `git pull` télécharge les nouveaux commits du serveur (`fetch`) puis les fusionne automatiquement dans ta branche actuelle (`merge`). Autrement dit, il récupère les mises à jour distantes et les intègre chez toi en une seule commande.

    - `origin` = dépôt distant
    - `main` = branche cible


#### 3. Créer une branche dédiée

```bash
git checkout -b feature/login
```

- `-b` : crée et change de branche

!!! danger
    🛑 Toujours créer une branche hors `main`.

<br>


#### 4. Ajouter les modifications

```bash
git add .
```

- `add` : place les fichiers dans la *[zone de staging]*
*[zone de staging]: Espace intermédiaire où Git stocke les fichiers ajoutés avec `git add` avant le commit.

---

#### 5. Créer un commit

```bash
git commit -m "Ajout du système de login"
```

- `-m` : message du commit

---

#### 6. Pousser la branche

```bash
git push -u origin feature/login
```

- `-u` ou `--set-upstream` : lie la branche locale à la branche distante
- permet ensuite d’utiliser simplement `git push`

---

#### 7. Créer une Merge Request

Sur GitLab :

- Ouvrir une Pull Request / Merge Request
- Vérification
- Validation
- Merge dans `main`

---

## 🔄 3. Mettre à jour sa branche avec main

Avant de continuer à travailler :

1.

```bash
git checkout main
git pull origin main
```

2.

```bash
git checkout feature/login
git merge main
```

Résoudre les conflits si nécessaire.

---

## ⚔️ 4. Conflits

Git marque les conflits :

```text
<<<<<<< HEAD
code local
=======
code distant
>>>>>>> main
```

Résoudre manuellement puis :

```bash
git add .
git commit
```

??? "Eviter les merge conflicts"
    Pas de miracles...

	- Communication : Dire sur quoi on travaille et ou on travaille
	- Commit : Souvent (Même pour de la merde)
	- Synchro souvent : A chaque début de taff, git pull
	- Petites branches -> Pas une branche générale pour plusieurs fonctionnalités

        > Ex. `page-login` -> login pas login + 40 formulaires 

---

## 🏷 5. Les Tags (versions stables)

Les tags servent à marquer une version importante.

Exemples :

- `v1.0.0`
- `v2.1.3`

---

### Créer un tag annoté (recommandé)

```bash
git tag -a v1.0.0 -m "Version stable"
```

- `-a` : annotated
- `-m` : message associé

---

### Lister les tags

```bash
git tag
```

---

### Envoyer les tags au serveur

```bash
git push origin --tags
```

---

### Supprimer un tag

Local :

```bash
git tag -d v1.0.0
```

Distant :

```bash
git push origin --delete v1.0.0
```

---

## ⏪ 6. Revenir à une version précédente

Voir les tags :

```bash
git tag
```

Se placer sur un tag :

```bash
git checkout v1.0.0
```

Attention : mode *detached HEAD*.

Créer une branche depuis un tag :

```bash
git checkout -b hotfix v1.0.0
```

---

### Différences importantes

- `git revert <commit>`  
  Annule un commit proprement (historique conservé)

- `git reset --hard <commit>`  
  Revient en arrière en supprimant l’historique après ce commit <br>
  (dangereux - faites pas ça svp 🤦‍♂️)

- `-f` ou `--force`  
  Force un push (écrase l’historique distant).  
  À éviter sur `main`. <br>
  (En cas de nécessité majeure, réflechissez 5 fois avant)

---

## 📋 7. Règles d’or en projet de groupe

- Ne jamais commit directement sur `main`
- Toujours `pull` avant de commencer
- Faire des commits petits et clairs
- Nommer les branches :
    - `feature/...`
    - `fix/...`
    - `hotfix/...`
- Ne jamais utiliser `--force` sur `main` <br>
(Sauf si t'es sur de toi le reuf mais je pars en vacances en août donc évite)

---

## 🧭 8. Structure mentale de Git

Git fonctionne comme un graphe de commits.

- Chaque commit pointe vers le précédent
- Les branches sont des pointeurs vers des commits
- `HEAD` est le pointeur actuel

Comprendre cela évite la majorité des erreurs.

---


## 📚 Vocabulaire essentiel Git

??? info "Repository (repo)"
    Dossier contenant le projet et tout son historique de versions.

??? info "Commit"
    Enregistrement d’un état précis du projet à un instant donné.

??? info "Branch (branche)"
    Ligne de développement indépendante permettant de travailler sans modifier `main`.

??? info "main"
    Branche principale du projet. Elle doit toujours rester stable.

??? info "Checkout"
    Action de changer de branche ou de se déplacer vers un commit.

??? info "Add"
    Commande (`git add`) qui place des fichiers dans la zone de staging avant un commit.

??? info "Zone de staging"
    Espace intermédiaire où Git prépare les fichiers avant de créer un commit.

??? info "Push"
    Envoie tes commits locaux vers le serveur distant.

??? info "Fetch"
    Télécharge les nouveaux commits depuis le serveur sans les fusionner.

??? info "Pull"
    Combine `fetch` + `merge` : récupère les nouveautés et les intègre automatiquement.

??? info "Merge"
    Fusionne deux branches ensemble.

??? info "Merge Request / Pull Request"
    Demande officielle pour intégrer une branche dans `main`.

??? info "Merge conflict"
    Conflit qui apparaît lorsque deux personnes modifient la même zone d’un fichier.

??? info "Origin"
    Nom par défaut du dépôt distant (serveur GitHub/GitLab).

??? info "Tag"
    Étiquette marquant une version importante du projet (ex: `v1.0.0`).

??? info "HEAD"
    Pointeur indiquant la position actuelle dans l’historique Git.
