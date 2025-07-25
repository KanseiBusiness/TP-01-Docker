Ah je vois ce que tu veux dire, un seul bloc markdown complet, propre, sans sortir du code markdown. Voilà, tout dans un seul bloc markdown, prêt à copier-coller intégralement dans ton README.md :

````markdown
# TP Docker MySQL

## Structure du projet

- Dockerfile : image basée sur mysql:9.1, copie les scripts SQL d'initialisation.
- init-v001.sql : création de la base formation et de la table utilisateurs.
- init-v002.sql : insertion de 3 utilisateurs dans la table.
- .env : fichier contenant les variables d’environnement (mot de passe root, nom de la base).

## Étapes pour construire et lancer le projet

1. Construire l’image Docker :

   ```bash
   docker build -t mysql-lab:1.0 .
````

2. Lancer le conteneur avec les variables d’environnement :

   ```bash
   docker run -d --name mysql-lab-container --env-file .env -p 3306:3306 mysql-lab:1.0
   ```

3. Se connecter au conteneur pour vérifier la base et les données :

   ```bash
   docker exec -it mysql-lab-container mysql -uroot -p
   # Entrer le mot de passe défini dans .env
   USE formation;
   SELECT * FROM utilisateurs;
   ```

## Vérifications à faire

* Vérifier que le conteneur est bien en cours d’exécution avec :

  ```bash
  docker ps
  ```

* Vérifier la présence de la base `formation` et de la table `utilisateurs`.

* Vérifier que la table contient bien les 3 utilisateurs insérés par le script `init-v002.sql`.

## Remarques

* Les variables sensibles sont stockées dans un fichier `.env` et non en dur dans le Dockerfile pour plus de sécurité.
* Le projet est conçu pour être exécuté en local sur une machine avec Docker installé.

Lien Docker Hub > https://hub.docker.com/r/kanseibusiness/tp-01-docker
