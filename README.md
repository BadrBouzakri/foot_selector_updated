# Application de Sélection d'Équipes de Foot - Version Améliorée

**Application créée par Badr**

Cette application permet de générer des équipes équilibrées à partir d'une liste de joueurs. Elle dispose également d'une console d'administration pour ajouter des joueurs et gérer leurs scores.

## Améliorations apportées

- **Interface optimisée** : Retrait de l'affichage des pourcentages des joueurs dans l'interface principale pour une expérience plus épurée
- **Meilleur équilibrage des équipes** : Utilisation de plusieurs algorithmes d'équilibrage
- **Interface d'administration améliorée** : Gestion simplifiée des joueurs et de leurs scores

## Table des matières

1. [Fonctionnalités](#fonctionnalités)
2. [Prérequis](#prérequis)
3. [Installation avec Docker](#installation-avec-docker)
4. [Exécution](#exécution)
5. [Accès à l'administration](#accès-à-ladministration)
6. [Structure des fichiers](#structure-des-fichiers)
7. [API](#api)
8. [Contributeurs](#contributeurs)

## Fonctionnalités

- Sélectionnez jusqu'à 10 joueurs pour générer des équipes équilibrées.
- Trois méthodes d'équilibrage disponibles :
  - **Par compétence** : Équilibre basé sur les scores des joueurs
  - **Serpent** : Méthode 1-2-2-1 pour un meilleur équilibre
  - **Aléatoire** : Équipes générées au hasard
- Affichage dynamique des équipes générées.
- Console d'administration pour ajouter et gérer des joueurs.
- Authentification pour accéder à la console d'administration.
- Texte de pied de page "Application créée par Badr" présent sur toutes les pages.
- Affichage dynamique de l'année courante dans le pied de page.

## Prérequis

- **Docker** : Vous aurez besoin de Docker pour exécuter l'application dans un conteneur.

## Installation avec Docker

### Étape 1 : Cloner le projet

Clonez ce dépôt Git sur votre machine locale :

```bash
git clone https://github.com/BadrBouzakri/foot_selector_updated.git
cd foot_selector_updated
```

### Étape 2 : Construire l'image Docker

Construisez l'image Docker en utilisant le fichier **`Dockerfile`** fourni. Assurez-vous d'être dans le répertoire du projet.

```bash
docker build -t application-equipes .
```

### Étape 3 : Lancer le conteneur

Une fois l'image Docker construite, vous pouvez exécuter l'application à l'aide de Docker. Utilisez cette commande pour démarrer un conteneur à partir de l'image :

```bash
docker run -d -p 5050:5050 --name app-equipes application-equipes
```

- `-d` exécute le conteneur en mode détaché (en arrière-plan).
- `-p 5050:5050` mappe le port 5050 du conteneur au port 5050 de votre machine.
- `--name app-equipes` nomme le conteneur pour une gestion plus facile.

### Étape 4 : Accéder à l'application

Une fois le conteneur en cours d'exécution, vous pouvez accéder à l'application via un navigateur en visitant :

```
http://localhost:5050
```

## Exécution (Docker)

Pour vérifier si le conteneur est en cours d'exécution, utilisez la commande suivante :

```bash
docker ps
```

Pour arrêter le conteneur :

```bash
docker stop app-equipes
```

Pour relancer le conteneur :

```bash
docker start app-equipes
```

Pour supprimer le conteneur :

```bash
docker rm -f app-equipes
```

## Accès à l'administration

L'application dispose d'une console d'administration accessible via l'URL suivante :

```
http://localhost:5050/admin
```

Les identifiants par défaut pour accéder à la console d'administration sont :

- **Nom d'utilisateur** : `admin`
- **Mot de passe** : `admin`

Vous pouvez utiliser cette console pour ajouter de nouveaux joueurs et modifier leurs scores.

## Structure des fichiers

Voici la structure des fichiers principaux de l'application :

```
.
├── app.py                  # Fichier principal de l'application Flask
├── templates/
│   ├── index.html          # Page d'accueil
│   ├── teams.html          # Page des équipes générées
│   ├── admin.html          # Page de connexion à l'administration
│   └── admin_console.html  # Console d'administration pour ajouter des joueurs
├── static/                 # Fichiers statiques (CSS, JS, vidéos, etc.)
├── requirements.txt        # Liste des dépendances Python
├── Dockerfile              # Pour créer une image Docker de l'application
└── README.md               # Fichier que vous lisez actuellement
```

## API

### Routes principales

1. **`/`** : Page d'accueil où vous pouvez sélectionner des joueurs pour générer des équipes.
2. **`/teams`** : Affiche les équipes générées.
3. **`/admin`** : Page de connexion pour accéder à la console d'administration.
4. **`/admin/console`** : Console d'administration pour ajouter ou modifier des joueurs.
5. **`/admin/logout`** : Déconnexion de l'interface d'administration.

### Fonctionnement interne

L'application utilise Flask comme framework web et stocke les données des joueurs en mémoire. Pour une version de production, il serait recommandé d'ajouter une base de données persistante comme SQLite, PostgreSQL ou MongoDB.

Les méthodes d'équilibrage des équipes sont implémentées dans la fonction `balance_teams()` qui offre trois approches différentes pour créer des équipes équilibrées :

1. **Par compétence** : Algorithme glouton qui répartit les joueurs en fonction de leur score.
2. **Serpent** : Algorithme de type "draft" qui alterne les sélections.
3. **Aléatoire** : Mélange aléatoire des joueurs avant de les répartir.

## Contributeurs

- **Badr** - Développeur principal de l'application.

## Personnalisation

### Ajout de vidéos d'arrière-plan

Pour ajouter des vidéos d'arrière-plan, placez vos fichiers MP4 dans le dossier `static/` et assurez-vous que les noms correspondent à ceux référencés dans les templates :

- `background.mp4` pour la page d'accueil
- `background_teams.mp4` pour la page des équipes

### Modification des couleurs et du style

Les styles sont définis directement dans les fichiers HTML à l'aide de balises `<style>`. Vous pouvez personnaliser les couleurs, les polices et les autres aspects visuels en modifiant ces sections.

---

Ce **README** vous guide sur la façon de **construire** et **exécuter** l'application en utilisant Docker, ce qui simplifie l'installation et la gestion des dépendances. Si vous avez des modifications ou des améliorations à ajouter, n'hésitez pas à contribuer au projet.