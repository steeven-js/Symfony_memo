```
git init
git add .
git status
git commit -m "✨ wip"
git branch -M main
git remote add origin https://github.com/steeven-js/Symfony_memo.git
git push -u origin main

```

```
git add .
git status
git commit -m "✨ wip"
git push -u origin main
```

# Symfony_memo
Aide mémoire des commandes pour Symfony

## symfony-cli

```
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
iwr -useb get.scoop.sh | iex
scoop install symfony-cliy
symfony -v
```

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

Visitons [127.0.0.1:8000](https://127.0.0.1:8000/) (dans mon cas) et constatons que Symfony Marche !!

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

## Annotations et routes paramétrées

### annotations

Au lieu de placer toutes les routes de l’application dans un seul fichier, il peut-être plus souple d’utiliser les *annotations* dans le code même du contrôleur pour plus de commodité :

Commençons par les installer :

`composer require annotations`

Recommentez tout le contenu de *routes.yaml*

Puis annotez votre contrôleur :

### routes paramétrées

Ajoutons une autre route paramétrée dans notre contrôleur:

```php
<?php
    namespace App\Controller;

    use Symfony\Component\HttpFoundation\Response;
    use Symfony\Component\Routing\Annotation\Route;

    class HelloController
    {
        /**
        * @Route("/hello")
        */
        public function sayHello()
        {
            return new Response('Hello!');
        }
        /**
        * @Route("/bonjour/{nom}")
        */
        public function bonjour($nom)
        {
            return new Response("Bonjour $nom !");
        }
    }
```

### debug des routes

On peut lister toutes ses routes :

`php bin/console debug:router`

et obtenir :

Name | Method | Scheme | Host | Path
--- | --- | --- | --- | ---
app_hello_sayhello | ANY | ANY | ANY | /hello
app_hello_bonjour | ANY | ANY | ANY | /bonjour/{nom}

### la commande bin/console

Cette commande nous permet d’avoir des informations sur notre projet, de faire des actions primaires dessus et de le débugger. Afin d’obtenir la liste des options offertes par cette commande :

`php bin/console`

Prenez le temps de lire la documentation de chaque commande et d’essayer de comprendre ce que chacune d’elle fait.

Remarquez la commande que nous avons utilisée pour lister les routes de notre projet : debug:router Displays current routes for an application

Puis retester : [127.0.0.1:8000/bonjour/toto](https://127.0.0.1:8000/bonjour/toto)

## Utiliser des templates Twig dans sf

Nous voudrions à présent utiliser des templates Twig dans notre application.

### installation

Commençons par utiliser la recette flex pour l’installer :

`composer require twig`

contrôleur avec twig

Puis changeons notre contrôleur pour hériter de `AbstractController` :

```php
<?php

    namespace App\Controller;

    use Symfony\Component\HttpFoundation\Response;
    use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
    use Symfony\Component\Routing\Annotation\Route;

    class HelloController extends AbstractController
    {
        /**
        * @Route("/hello")
        */
        public function sayHello()
        {
            return new Response('Hello!');
        }
        /**
        * @Route("/bonjour/{nom}")
        */
        public function bonjour($nom)
        {
            //return new Response("Bonjour $nom !");
            return $this->render('bonjour.html.twig', [
                        'nom' => $nom,
                        ]);
        }
    }
```

### template twig

et mettons en place le template correspondant `bonjour.html.twig` dans le dossier « templates » :

```php
{# templates/bonjour.html.twig #}
{% extends 'base.html.twig' %}

{% block body %}
    <h1>Bonjour {{ nom }}</h1>
{% endblock %}
```

avec un `base.html.twig` du type :

```php
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}Welcome!{% endblock %}</title>
        {% block stylesheets %}{% endblock %}
    </head>
    <body>
        {% block body %}{% endblock %}
        {% block js %}{% endblock %}
    </body>
</html>
```

Retestons : 127.0.0.1:8000/bonjour/toto

### Memo twig

`php bin/console debug:twig`

Vous donnera la liste des Fonctions, Filtres et Tests disponibles dans les templates Twig.
