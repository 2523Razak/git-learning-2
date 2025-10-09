# Exercice 2 - Branching & Merging

## Objectif

Apprendre à créer des branches, y effectuer des changements et les fusionner (merge) dans la branche principale `main`, en travaillant **uniquement via le terminal** à l’aide de **GitHub CLI**.

## Étapes du projet

### 1. Créer et cloner le dépôt

```bash
gh repo create git-learning-2 --public --clone
cd git-learning-2
```
Ces commandes permettent de créer un nouveau dépôt public nommé `git-learning-2` sur GitHub, puis de le cloner automatiquement dans le dossier courant.

### 2. Créer une nouvelle branche

```bash
git checkout -b myself
```

Cette commande crée une nouvelle branche nommée **myself** et bascule automatiquement dessus.
Elle est utilisée pour séparer les modifications personnelles de la branche principale (`main`).

### 3. Créer un fichier contenant des informations personnelles

```bash
cat > about.txt << EOF
Nom: Boureima Issa Adamou
Prénom: Razak
Lieu de naissance: Ville, Pays
Date de naissance: JJ/MM/AAAA
EOF
```
Cette commande crée un fichier `about.txt` et y ajoute vos informations personnelles.
La syntaxe `EOF` permet d’écrire plusieurs lignes à la fois dans un fichier.

### 4. Faire un commit et pousser la branche

```bash
git add about.txt
git commit -m "Ajout informations personnelles"
git push origin myself
```

* `git add about.txt` : prépare le fichier à être enregistré.
* `git commit -m "..."` : enregistre le changement localement.
* `git push origin myself` : envoie la branche sur GitHub.

### 5. Créer une Pull Request (PR)

```bash
gh pr create --base main --head myself --title "Ajout informations personnelles" --body "Ajout du fichier about.txt avec mes informations"
```
Cette commande crée une **Pull Request** sur GitHub pour fusionner les changements de la branche `myself` dans `main`.

* `--base main` : indique la branche de destination.
* `--head myself` : indique la branche contenant les changements.
* `--title` et `--body` : ajoutent un titre et une description à la PR.

### 6. Fusionner la Pull Request

```bash
gh pr merge --merge
```
Cette commande permet de fusionner la Pull Request dans la branche principale `main`.

## Difficultés rencontrées

### Erreur lors de la création de la Pull Request

Lors de l’exécution de la commande :

```bash
gh pr create --base main --head myself --title "Ajout informations personnelles" --body "Ajout du fichier about.txt avec mes informations"
```

Git a renvoyé l’erreur :

> **no commits between main and myself**

Cela signifie qu’il n’y avait **aucune différence** entre les deux branches (`main/master` et `myself`), donc GitHub refusait de créer une PR inutile.

#### Solution :

Faire une **modification réelle** dans la branche `myself` avant de créer la Pull Request :

```bash
echo "Ceci est une modification test" >> about.txt
git add about.txt
git commit -m "Mise à jour du fichier about.txt"
git push origin myself
```
On peut aussi ajouter un README dans la branche `main` (ou `master`) avant même de créer la branche myself.
Ensuite, la PR peut être créée avec succès :

```bash
gh pr create --base main --head myself --title "Ajout informations personnelles" --body "Ajout du fichier about.txt avec mes informations"
```
## Résumé du projet

Ce projet m’a permis de :

* Créer un dépôt GitHub depuis le terminal.
* Gérer plusieurs branches et les commits.
* Utiliser **GitHub CLI** pour créer et fusionner une Pull Request.
* Comprendre la logique du **versionnement collaboratif**.
