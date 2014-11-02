---
layout: post
title:  "Pourquoi j'utilise Jade ?"
date:   2014-10-31 16:19:03
categories: jade gulp workflow
---

Depuis quelque temps, **Jade** est devenu mon outils principal lorsque je développe des sites statiques.  Allié à la bonne tache **Gulp**, il devient ultra puissant et offre des possibilités inimaginable en HTML.

Au début, **Jade** peut être déroutant de par sa syntax que ses fonctions. Mais au bout de quelques temps (1à 2 heures intensive), vous ne pourrez plus vous en passer ! Le point fort de Jade, c’est qu’il vas ajouter un nombres de fonctionnalité bien utiles à notre workflow. Vous pourrez donc utliser des includes, des mixins, des itérations ou encore des variables. Le tout est compilé HTML.

Pour voir un peu comment Jade fonctionne, je vous propose un cas pratique afin de passer en revue les différents moyen d'exploiter Jade. 

## Comment installer Jade ?

Avant toute chose, Jade est un module node.js, il vous faudra donc avoir ce dernier d'installer sur votre machine. Si vous ne l'avez pas paas encore rendez-vous sur [node.js](http://nodejs.org/), de cliquer sur **download** et de choisir la version pour votre système d'exploitation. Une fois installer, lancez votre terminal est entrez la commande suivante :

{% highlight ruby %}
$ npm install jade --global
{% endhighlight %}

Cette commande vas installer Jade de façon globale sur votre système. Si vous êtes sur mac un petit `sudo` ne feras pas de mal et éviteras d'avoir des messages d'erreur.

Enfin, pour tester la présence de Jade, nous allons lui demander quelle est sa version avec la commande :

{% highlight ruby %}
$ jade --version
{% endhighlight %}

Si la commade vous retourne un numéro de version c'est que jade est belle et bien installé sur votre machine.

## Premier pas : créer un fichier jade et le compiler en html.

Bon, jade est installer, nous avons la bonne version alors testons le un peu. D'abord mettez vous là ou ou vous avez l'habitude de faire vos test et créez un dossier vide :

{% highlight ruby %}
$ cd lab/
$ mkdir jade/ 
$ cd jade/
{% endhighlight %}

A l'intérieur de ce dossier, nous allons créer notre fichier jade. Pour cela, il faut juste ajouter l'extension `.jade` à votre fichier :

{% highlight ruby %}
$ touch index.jade
{% endhighlight %}

Une fois le fichier créé ouvrez le avec votre éditeur préféré. Pour ma part j'utilise *sublime text*, si vous êtes dans le même cas que moi, il existe un [plugin](https://sublime.wbond.net/packages/Jade) pour la syntaxe et l'autocomplétion des fichiers portant l'extension `.jade`.

### La syntaxe de Jade

Bon, nous y voilà, tout est prêts ! Nous pouvons ajouter notre premier morceau de code en Jade. Comme je vous l'ai dit en introduction Jade a une syntaxe un peu particulière. Voici comment on déclare un `h1`et un `p`:

{% highlight jade %}
h1 Je suis un tire h1
p Je suis un paragraphe
{% endhighlight %}

Remarquez ici, que nous n'utilisons pas de chevrons pour ouvrir et fermer nos éléments ce qui facilite grandement la lisibilitée de notre code. Super, mais comment ca se passe pour déclarer des propriétés ou ajouter une classe à nos élément ? Là, encore la syntaxe est clair et lisible, ajoutons un lien avec une classe :

{% highlight jade %}
a.btn(href="http://google.com", title="Mon lien", target="_blank") Google
{% endhighlight %}

Et un super combo avec plusieurs classes et un id :

{% highlight jade %}
a.btn.btn-success#button(href="#") Combo bouton
{% endhighlight %}

## Compiler nos fichier .jade en .html
Nous avons vue la syntaxe de Jade, nous allons maintenant voir comment compiler nos fichier `.jade` en `.html`. Pour cela, reprennez le terminal dans le dossier ou ce situe vos fichiers Jade et éxécuter la commande suivante :

{% highlight ruby %}
$ jade index.jade
{% endhighlight %}




