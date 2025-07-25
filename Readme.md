# TP Docker MySQL

Ce projet permet de configurer une base de données MySQL avec Docker. Il utilise des scripts d'initialisation pour créer une base de données et insérer des utilisateurs de manière automatisée.

## Structure du projet

- **Dockerfile** : Ce fichier crée une image Docker basée sur `mysql:9.1` et copie les scripts SQL d'initialisation dans l'image.
- **init-v001.sql** : Script SQL qui crée la base de données `formation` et la table `utilisateurs`.
- **init-v002.sql** : Script SQL qui insère 3 utilisateurs dans la table `utilisateurs`.
- **.env** : Fichier contenant les variables d'environnement (mot de passe root, nom de la base de données).

## Étapes pour construire et lancer le projet

### 1. Construire l'image Docker

Pour construire l'image Docker, exécute la commande suivante dans le terminal :

```bash
docker build -t mysql-lab:1.0 .
````

### 2. Lancer le conteneur

Lance le conteneur avec les variables d'environnement définies dans le fichier `.env` :

```bash
docker run -d --name mysql-lab-container --env-file .env -p 3306:3306 mysql-lab:1.0
```

### 3. Se connecter au conteneur

Connecte-toi au conteneur pour vérifier que la base de données et les données sont bien présentes :

```bash
docker exec -it mysql-lab-container mysql -uroot -p
# Entrez le mot de passe défini dans .env
USE formation;
SELECT * FROM utilisateurs;
```

## Vérifications à faire

### 1. Vérifier que le conteneur est bien en cours d'exécution

Exécute la commande suivante pour vérifier que le conteneur est actif :

```bash
docker ps
```

### 2. Vérifier la présence de la base `formation` et de la table `utilisateurs`

Dans le conteneur, assure-toi que la base de données `formation` et la table `utilisateurs` existent en exécutant les requêtes SQL suivantes :

```sql
USE formation;
SHOW TABLES;
```

### 3. Vérifier que la table contient les 3 utilisateurs

Vérifie que la table `utilisateurs` contient bien les 3 utilisateurs insérés par le script `init-v002.sql` :

```sql
SELECT * FROM utilisateurs;
```

## Remarques

* Les variables sensibles (comme le mot de passe root) sont stockées dans un fichier `.env` et non en dur dans le Dockerfile pour une meilleure sécurité.
* Ce projet est conçu pour être exécuté localement sur une machine avec Docker installé.

## Lien Docker Hub

Vous pouvez retrouver l'image Docker sur Docker Hub à l'adresse suivante :
[Docker Hub - kanseibusiness/tp-01-docker](https://hub.docker.com/r/kanseibusiness/tp-01-docker)
