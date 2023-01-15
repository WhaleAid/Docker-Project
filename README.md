#DOCKER-COMPOSE

Ce fichier docker-compose.yml définit une application qui utilise plusieurs conteneurs Docker pour exécuter plusieurs instances de PHP (php1 et php2) et de nginx (nginx1 et nginx2) ainsi qu'une base de données MySQL (database). Il utilise également des volumes pour les données de la base de données et des fichiers de configuration pour les conteneurs nginx.

Il y a un service php1 qui dépend de database, il est construit à partir d'un fichier Dockerfile spécifique et expose le port 9000. Il a un volume pour app qui est monté sur /var/www/html

Il y a un service php2 qui dépend de database aussi, il est construit à partir d'un fichier Dockerfile spécifique et expose le port 9001. Il a un volume pour app qui est monté sur /var/www/html

Il y a un service nginx1 qui utilise l'image nginx:latest, il expose le port 8081 et a des volumes pour les fichiers de configuration, les fichiers publics, les logs et utilise également un volume de php1 pour monter les fichiers. Il dépend de php1

Il y a un service nginx2 qui utilise l'image nginx:latest, il expose le port 8082 et a des volumes pour les fichiers de configuration, les fichiers publics, les logs et utilise également un volume de php2 pour monter les fichiers. Il dépend de php2

Il y a un service database qui utilise l'image mysql:5.7, il expose le port 3306, il a un volume pour les données de la base de données, et définit des variables d'environnement pour les informations de connexion à la base de données.

# DOCKERFILE

Les fichiers Dockerfile se trouve dans chacun des dossiers (laravel1 et laravel2) sous le répértoire php et celui-ci définit les étapes nécessaires pour construire une image de conteneur pour une application PHP utilisant le runtime PHP 7.4-fpm. Il utilise l'instruction FROM pour spécifier l'image de base à utiliser.

Il utilise les arguments définis dans le fichier docker-compose.yml pour créer un utilisateur système pour exécuter les commandes Composer et Artisan. Il installe également les dépendances système nécessaires telles que git, curl, libpng-dev, libonig-dev, libxml2-dev, zip et unzip. Il installe également des extensions PHP comme pdo_mysql, mbstring, exif, pcntl, bcmath, gd. Il copie également la version la plus récente de Composer.

Il définit également le répertoire de travail comme /var/www et exécute des commandes pour installer les dépendances de l'application (composer et npm), et pour donner les droits d'accès aux dossiers public et storage.

Enfin, il exécute la commande npm run build pour lancer la construction de l'application. Une fois que cette image est construite, elle peut être utilisée pour lancer un conteneur en utilisant cette image de conteneur, et la commande composer install pour installer composer dans l'image PHP.
