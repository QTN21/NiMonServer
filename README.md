# Création du serveur zabbix

## Sommaire
- [Point théorie](#point-de-théorie)
- [Architecture du serveur](#architecture-du-serveur)
- [Installation du serveur](#installation)

## Point de théorie
Ce repository contient la configuration Docker Compose pour mettre en place un serveur Zabbix avec un serveur de log Syslog.

Ce serveur se décompose en 3 éléments principaux:
- Serveur Zabbix : contient une base de données PostgreSQL et un serveur web nginx.
- Grafana : pour l'affichage des métriques 

Ce projet contient un dossier `env_vars` avec les variables d'environnements relatives aux conteneurs

### Notes sur la configuration
Chaque conteneur définit dans la configuration Docker Compose possèdent la directive :

- **Logging** afin de se connecter au serveur Syslog de la Machine principale et centraliser les logs de tous les conteneurs. Chaque conteneur est défini par un tag permettant de différencier chaque instance dans le fichier log.
- **User** définissant l’utilisateur par défaut lors de la connexion au conteneur et éviter un accès direct à l’utilisateur root.
- **Cap_add** et **Cap_drop** permettant donner le minimum de capacité linux de l’instance et éviter l’élévation de privilèges du conteneur.
- **Healthcheck** (seulement pour les instances critiques) permet de lancer une commande afin de s’assurer que le service est bien disponible.
- **Restart** permettant de définir la méthode d’arrêt du conteneur. Dans ce cas, l’instance s’arrêtera à la fermeture/suppression du service (fichier docker-compose.yaml).
- **Env_file** contenant les variables d’environnement utilisées par le conteneur afin de définir les paramètres de l’instance.
- **Secrets** contenant l’utilisateur et le mot de passe pour accéder à la base de données PostgreSQL
- **Volumes** définissant un espace de stockage spécifique pour le conteneur créé
- **Network** assignant le conteneur à un sous-réseau particulier. Permet de segmenter les connexions entre les conteneurs Docker.
- **Ulimits et deploy** permettant respectivement de définir une limite d’utilisation des ressources du système et de l’application pour ce conteneur. Cela permet d’éviter une surcharge sur le conteneur.

## Architecture du serveur
> Renseigner une image

## Installation
```bash
docker compose up -d
```