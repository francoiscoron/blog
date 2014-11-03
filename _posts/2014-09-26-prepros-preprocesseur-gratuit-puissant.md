---
layout: post
title:  "Prepros, un preprocesseur puissant et gratuit"
date:   2014-07-21
cover: cover-prepros
categorieBg: webdev
---

De nouvelles syntaxes sont apparut pour les développeur front-end ! Le problème avec ces nouvelles méthodes d’integration, notamment avec le **scss**, le **jade** ou encore le **markdown** est qu’il faut compiler les fichiers afin d’avoir un rendu lisible par les navigateur en html, css et js !

Ce petit software vas effectuer ces lignes de commande à votre place et se charger de compiler vos fichiers et tout et tout ! En plus, il est disponible sur MAC et PC ! Son interface est plutôt agréable et intuitif et il y à même une extension plutôt pratique sur le navigateur Google Chrome ! Que demander de plus.

## Comment ça marche ?

Tout d’abord, il faut télécharger l’application [ici](http://alphapixels.com/prepros/ "Télécharger Prepros") ! Ensuite, une fois le soft installé, il suffit de déposer votre dossier contenant vos fichier à compiler dans la fenêtre de PREPOS. Et le tour et joué ! Le système de Drag’n’drop, rend sa manipulation simple et rapide !

Une fois le dossier à l’intérieur, quand vous sauvegardez le fichier à compiler, prepros ce chargera d’exécuter la commande et si votre fichier ne contient pas d’erreur une notification vous informera que la compilation est faite avec succès.

## C’est mieux avec un exemple !

Je vous propose un petit *tutoriel* basé sur une compilation scss, afin de voir quelques fonctionnalités de prepros.

### 1 . Création du répertoire

Nous allons d'abord créer un dossier ou vous avez l’habitudes de faire vos tests et nommer le comme bon vous semble. A l’intérieur nous allons créer un fichier ```index.html``` et un fichier ```style.scss```
.![Prepros mise en place](/uploads/prepros/prepos-part-1.jpg)

### 2 . Importation du dossier dans prepros

Une fois votre répertoire crée, il suffit de le glisser soit sur l’icônes soit dans la fenêtre de **prepros**.

Les fichiers à compiler devrait s’afficher à l’intérieur. Dans notre cas on peut voir le fichier ```style.scss``` :

![Création du fichier scss](/uploads/prepros/prepos-part-2-1024x646.jpg)

### 3 . Première compilation

Nous allons maintenant tester la compilation de notre fichier.

Dans le fichier _index.html_ nous allons ajouter une base de html :

{% highlight html linenos %}
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Prepos</title>
    </head>
    <body>
        <div class="wrapper">
            <h1>Prepros : compiler un fichier scss</h1>
        </div>
    </body>
</html>
{% endhighlight %}

Et nous allons ajouter quelques règles dans notre fichier _style.scss_ :
{% highlight scss linenos %}

$heading-color: #e74c3c;

body {
    margin: 0;
    padding: 0;
}

.wrapper {
    width: 75%;
    margin: 0 auto;
}

h1 {
    color : $heading-color;
    text-transform: uppercase;
}
{% endhighlight %}

Si tout c'est bien passé lors de la sauvergarde du fichier scss un jolie petit message comme si dessous devrais s'afficher et un fichier ```style.css``` et ```config.rb``` devrais être apparut dans votre dossier :

![Succès prepros](/uploads/prepros/prepros-part-3.jpg)

### 4 . Ajouter compass à son projet

Le scss c'est bien mais avec la librairie [compass](link-compass "Librairie compass") c'est encore mieux.

Là encore l'ajout de compass au projet se fait trés simplement. Mettez vous sur la fenêtre de prepros, et cliquez sur le fichier style.scss. Une sidebar devrais apparaitre sur la droite.

![Ajouter compass au projet](/uploads/prepros/prepos-part-4-1024x645.jpg)

Et il suffit alors de cocher la case **Use Compass**. Le tour est joué !

Nous allons tout de même vérifier la présence de compass en ajoutant ceci en haut de notre fichier ```style.scss``` :

{% highlight css linenos %}
@import "compass/reset"
{% endhighlight %}

Cette commande Compass injecte un reset css à l'intérieur de votre feuille de style. Si aucun message n'apparait c'est que **compass** est fonctionnel.

### 5 . Live preview

Prepos permet d'avoir un aperçu en direct des modifications que l'on fait. Pour cela il faut cliquez sur la petite planète dans la fenêtre du logiciel (Open Live Preview) :

![Livepreview Prepros](/uploads/prepros/prepos-part-5.jpg)

Après avoir cliquez un onglet vas s'ouvrir dans votre navigateur et vas afficher votre projet. A partir de ce moment toutes vos modifications prendrons effet immédiatement, votre navigateur rafraichiras la page à chaque enregistrement de vos fichier !

### 6 . Astuce : Optimiser vos images

Bon une dernière fonctionnalité avant la fin. Prepos propose un petit script plutôt sympa et relativement utile pour augmenter les performances de votre site web : un outil permettant d'optimiser la taille de vos images.

Pour cela nous allons ajouter une images à notre projet, prenez n'importe laquelle. Personnellement j'ai utilisé une image provenant du site [lorem picsum](http://lorempicsum.com/#futurama "Aller sur Lorem Picsum"), très utile pour les images de subsitution.

Une fois l'image dans votre dossier, mettez vous sur l'onglet image et cliquer sur la petite flèche arrondi en bas à gauche :

![Ajouter image prepros](/uploads/prepros/prepros-part-6.jpg)

Vous devriez voir apparaitre votre image dans la liste. A ce moment là, de la même manière que nous avons ajouter compass à notre projet, cliquez sur le nom de votre image, le volet à droite devrais s'ouvrir. Vous n'avez plus qu'a cliquer sur "optimize" :

![Optimisation image](/uploads/prepros/prepros-part-6.1.jpg)

Suivant l'image vous obtiendrez différent résultat, mais sur plusieurs images on peut arriver a économiser quelques précieux kilo-octet !

Nous verrons dans un prochain tutoriel comment automatiser ce genre de tache avec **Gulp.js**.