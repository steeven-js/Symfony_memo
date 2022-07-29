# Symfony_memo
Aide mémoire des commandes pour Symfony

## symfony-cli

`Set-ExecutionPolicy RemoteSigned -scope CurrentUser`

`iwr -useb get.scoop.sh | iex`

`scoop install symfony-cliy`

`symfony -v`

#https://www.univ-orleans.fr/iut-orleans/informatique/intra/tuto/php/symfony-simple-app.html

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

Visitons [127.0.0.1:8000]([127.0.0.1:8000](https://127.0.0.1:8000/)) (dans mon cas) et constatons que Symfony Marche !!

## Un Controleur et une route simple

### routes
Observer le contenu de `routes.yaml` dans le dossier config. Laisser ce code commenté et ajoutez-y le code suivant :

`hello:
    path: /hello
    controller: App\Controller\HelloController::sayHello`

### contrôleur
Puis placer le contrôleur suivant dans src/Controller/HelloController.php :

``` ruby
<?php

namespace App\Controller;

use Symfony\Component\HttpFoundation\Response;

class HelloController
{
    public function sayHello()
    {
        return new Response('Hello!');
    }
}
```
On teste : [127.0.0.1:8000/hello](https://127.0.0.1:8000/hello)



































