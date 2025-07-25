# TP Docker MySQL - kanseibusiness

## Description

Ce projet a pour objectif de créer une image Docker basée sur MySQL 9.1, avec initialisation automatique d'une base de données `formation` contenant une table `utilisateurs`. Les scripts SQL sont injectés dans le conteneur via le dossier `/docker-entrypoint-initdb.d/`.

---

## Structure du projet

- `Dockerfile` : Fichier de construction de l'image Docker basée sur `mysql:9.1`.
- `init-v001.sql` : Script SQL de création de la base de données `formation` et de la table `utilisateurs`.
- `init-v002.sql` : Script SQL d'insertion de 3 utilisateurs dans la table `utilisateurs`.
- `.env` : Fichier contenant les variables d’environnement pour sécuriser les credentials (mot de passe root, nom de la base).
- `README.md` : Ce fichier.

---

## Étapes de build et de lancement

1. **Construire l’image Docker**

```bash
docker build -t mysql-lab .
