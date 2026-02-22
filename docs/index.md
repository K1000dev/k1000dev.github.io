# 🚀 Guide Git : Travailler en Équipe 

<br>
> Synthèse Git faites par moi en feat. avec l'IA parce que nos profs ont la flemme d'enseigner
<br>

---

## 📋 Sommaire
1. [Synchroniser le projet (Pull)](#1-synchroniser-le-projet-pull)
2. [Créer une branche de travail](#2-creer-une-branche-de-travail)
3. [Enregistrer les changements (Commit)](#3-enregistrer-les-changements-commit)
4. [Lier et envoyer (Push)](#4-lier-et-envoyer-push)
5. [Demander la fusion (Merge Request)](#5-demander-la-fusion-merge-request)
6. [Gestion des versions (Tags)](#6-gestion-des-versions-tags)

---

## 1. Synchroniser le projet (Pull)
Avant de commencer quoi que ce soit, il faut s'assurer d'avoir la version la plus récente de la branche principale.

??? info "La commande de synchronisation"
    `git pull origin main`
    
    * **git pull** : "Va chercher les nouveautés sur le serveur et fusionne-les chez moi."
    * **origin** : C'est le nom par défaut du serveur (GitLab/GitHub). C'est "la source".
    * **main** : C'est le nom de la branche que vous voulez copier (le tronc commun).

---

## 2. Créer une branche de travail
**Règle d'or :** Ne travaillez jamais directement sur `main`. Créez une branche dédiée à votre fonctionnalité.

??? example "Créer et basculer sur une branche"
    `git checkout -b <nom-de-la-branche>`
    
    * **-b** : (branch) Indique à Git de créer la branche avant de basculer dessus.
    * **checkout** : Commande pour changer de branche de travail.

---

## 3. Enregistrer les changements (Commit)
Une fois vos fichiers modifiés, enregistrez une "photo" de votre travail localement.

??? success "Valider vos modifications"
    `git commit -m "message du commit"`
    
    * **-m** : (message) Paramètre obligatoire pour expliquer ce que vous avez ajouté ou modifié. Soyez explicite !

---

## 4. Lier et envoyer (Push)
Si la branche n'est pas encore liée au projet sur le serveur (votre PC ne sait pas où l'envoyer).

??? tip "Pousser vers le serveur"
    `git push --set-upstream origin <nom-de-la-branche>`
    
    * **--set-upstream** (ou **-u**) : Crée le lien entre votre branche locale et le serveur GitLab. Les prochaines fois, un simple `git push` suffira.
    * **-f** : (force) **Attention !** À éviter absolument. Cela écrase les données du serveur.

---

## 5. Demander la fusion (Merge Request)
Une fois le push effectué, rendez-vous sur la page du projet sur GitLab pour créer le **Merge Request**.

> Cela permet à vos coéquipiers de relire votre code avant qu'il ne soit intégré au projet final.

---

## 6. Gestion des versions (Tags) 🏷️
Les tags permettent de marquer des étapes importantes (ex: `v1.0`, `Rendu-Final`).

### Créer et envoyer un Tag
* **Créer :** `git tag -a v1.0 -m "Version stable du projet"`
    * **-a** : (annotated) Crée un tag complet avec auteur et date.
* **Envoyer :** `git push origin --tags` (Les tags ne sont pas envoyés par défaut avec un push classique).

### 🆘 Revenir en arrière en cas d'erreur
Si une erreur critique survient sur la version actuelle, vous pouvez utiliser un tag pour revenir à un état sain :

1. **Vérifier l'état du tag :** `git checkout v1.0`
2. **Repartir proprement :** `git checkout -b reparation-depuis-v1`
   *(Cela crée une nouvelle branche à partir du point précis où le tag a été posé).*

### Supprimer un Tag
* **Local :** `git tag -d v1.0`
* **Serveur :** `git push origin --delete v1.0`