# Symfony_memo
Aide mémoire des commandes pour Symfony

## symfony-cli

`Set-ExecutionPolicy RemoteSigned -scope CurrentUser`

`iwr -useb get.scoop.sh | iex`

`scoop install symfony-cliy`

`symfony -v`

##

# Débuts avec Symfony

## Préparatifs

## Squellette d’application Symfony

Partons de la trame d’application de type microservice déjà créée à l’aide de composer :

`composer create-project symfony/skeleton hello-sf`

Serveur Web embarqué de Symfony

Lançons le serveur web embarqué de Symfony.

`symfony server:start -d`
ou

`symfony serve`

Ce qui lance le serveur embarqué de PHP en arrière plan.

Pour le stopper :

`symfony server:stop`

Si on veut le lancer au premier plan (ou si l’extension pcntl n’est pas installée), on le lance au premier plan avec :

`symfony server:start`

Pour le stopper :

`Ctrl+C`

Visitons [127.0.0.1:8000](127.0.0.1:8000) (dans mon cas) et constatons que Symfony Marche !!
