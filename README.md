# Comment configurer l'environnement de travail pour PHP et MySQL

## Mise en contexte

Guide servant à renseigner les étudiants sur le comment et le pourquoi que nous avons à configurer notre environnement de travail pour travailler avec PHP et MySQL.

## Lexique

Pour faciliter la lecture de ce guide, voici un lexique des différents termes :

- [WAMP](https://techterms.com/definition/wamp) : Est un regroupement d'applications qui inclut, Windows, Apache, MySQL, et PHP.
- [Apache](https://techterms.com/definition/apache) : Serveur web pour l'exécution des pages web.
- [MySQL](https://techterms.com/definition/mysql) : Base de données relationnelle libre.
- [phpMyAdmin](https://fr.wikipedia.org/wiki/PhpMyAdmin) : Interface pratique permet d'exécuter, très facilement et sans grandes connaissances en bases de données, des requêtes comme les créations de tables de données, insertions, mises à jour, suppressions et modifications de structure de la base de données, ainsi que l'attribution et la révocation de droits et l'import/export.

## Qu'est-ce Bitnami WAMP Stack

[Bitnami WAMP Stack](https://bitnami.com/stack/wamp) fournis un environnement de développement WAMP complet, entièrement intégré et prêt à fonctionner. Outre PHP, MySQL et Apache, il inclut également phpMyAdmin.

### Procédure d'installation

Pour installer Bitnami, il faut aller [ici](https://bitnami.com/stack/wamp), cliquer sur le bouton "Win / Mac / Linux", suite au téléchargement, il faut procéder à l'installation via l'outil d'installation.

### Configurer son environnement

À titre indicatif, l'application devrait s'installer sous le répertoire "C:\Bitnami". Voici les manipulations à effectuer :

- Créer un raccourci du répertoire "htdocs" qui se trouve sous "C:\Bitnami\wampstack-[VERSION]\apache2" et mettre ce raccourci à la racine de Bitnami ("C:\Bitnami\").
- Dans le répertoire "htdocs", créer un répertoire "bitnami" et y insérer le contenu de base du répertoire "htdocs" à l'intérieur.
- Dans le but de faciliter le développement, il faut désactiver la "cache" par défaut qui est configuré dans Bitnami. Si la cache est active, lors d'une modification à vos applications, celle-ci ne sera pas immédiatement reflétée dans vos applications. Il faut ouvrir le fichier "C:\Bitnami\wampstack-[VERSION]\php\php.ini" avec un éditeur de texte et rechercher la configuration "opcache.enable" et lui donner la valeur de "0" au lieu de "1".

### Exemple d'utilisation

Pour valider votre configuration, ouvrez un fureteur et aller à l'adresse suivante : <http://localhost/bitnami/index.html>, vous devriez apercevoir la page par défaut de Bitnami. Prendre note que dans l'adresse du site, il y a "bitnami", celui-ci représente le répertoire créé dans la configuration un peu plus tôt. Donc, nous allons faire un test, créer un répertoire avec le nom de "php" dans le dossier "htdocs". Dans le répertoire "php", il faut créer le fichier "index.php" et y insérer le code suivant :

``` php
<?php
    echo("test de ma configuration");
?>
```

Vous devriez maintenant être en mesure de naviguer à l'adresse : <http://localhost/php/index.php> et voir le texte "test de ma configuration" à l'écran.

## Configurer phpMyAdmin

Par défaut, lors de l'installation de Bitnami WAMP Stack, celui-ci installe par défaut phpMyAdmin. Pour y accéder, il faut ouvrir un fureteur et naviguer à l'adresse : <http://localhost/phpmyadmin/>. Lors de la première utilisation, vous aurez à configurer votre compte. Inscrire "root" pour l'utilisateur et "admin123" comme mot de passe.

## Configurer Visual Studio Code

### Installer les extensions nécessaires

Pour installer une extension dans Visual Studio Code, voici la [procédure](https://code.visualstudio.com/docs/editor/extension-gallery) à suivre. Donc, il faut installer les extensions suivantes :

- [PHP extension pack](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-pack) : regroupement d'extensions pour le développement PHP
- [sftp-sync](https://marketplace.visualstudio.com/items?itemName=liximomo.sftp) :  permet de transférer des fichiers sur le réseau, cette extension sera importante plus tard dans la session
- [Open PHP/HTML/JS In Browser](https://marketplace.visualstudio.com/items?itemName=PrimaFuture.open-php-html-js-in-browser) : permet d'ouvrir notre code directement dans le fureteur. Le raccourci est "Shift+F6", ça va ouvrir le fichier courant dans votre fureteur par défaut.

### Configurer les extensions

Suite à l'installation des extensions, il faut savoir comment [paramétrer les extensions](https://code.visualstudio.com/docs/getstarted/settings). il faut procéder à quelques configurations :

- Définir l'exécutable de PHP : dans la section "Extensions" du menu "Settings", il faut ouvrir "php" et aller éditer le fichier "settings.jsons" pour définir l'endroit de l'exécutable de php. Dans le fichier settings, il faut insérer les valeurs :
  
```json
"php.executablePath": "C:\\Bitnami\\wampstack-[VERSION]\\php\\php.exe",
"php.validate.executablePath": "C:\\Bitnami\\wampstack-[VERSION]\\php\\php.exe"
```

- Configurer Open PHP/HTML/JS, il faut aller dans "Extensions" -> "Open PHP/HTML/JS", il faut mettre la valeur "<http://localhost:8888/${fileBasename}>" dans la configuration "Custom Url to Open" et insérer la valeur "C:\Bitnami\wampstack-[VERSION]\apache2\htdocs" dans la configuration "Document Root Folder".
