---
layout: post
title:  "Git sur son serveur 1&1"
date:   2014-08-16
categorieBg: "webdev"
---
Aprés avoir passer quelques heures à vouloir créer un système de versionning sur mon _serveur web_ grace à **Git**, j'ai trouvé un petit post qui m'as été d'une aide précieuse [lien de l'article](http://blog.johnrbussiculo.com/2012/12/using-git-with-1and1-shared-hosting/). 
Celui-ci étant d'une part en anglais et d'une autre pas très étoffé, certaines phases n'étant pas vraiment intuitive, j'ai décidé de le remanier et de le détailler un peu. 

Pour suivre ce tuto, il faut pouvoir vous connecter à un serveur web en SSH. 1&1 propose un accés ssh et en plus **Git** est déjà installer sur le serveur. Pour les autres hébergements web, je suppose que la démarche reste la même à l'exception peut être de devoir installer git, mais avec un accés **SSH** cela ne devrait pas poser de problème.

Assez parler, place au tuto !

## Git & 1&1

Vérifier la présence de **GIT** sur votre serveur en effectuant la commande suivante :

{% highlight html linenos %}
 $ git --version
{% endhighlight %}

L'opération devrait retourner ```git version 1.5.7.5```

## Préparer les dossiers

Nous allons maintenant créer un dossier à la racine de notre serveur. Par exemple `mon-site-web`, à l'intérieur de ce dossier nous allons à nouveau créer deux sous dossiers. Le premier s'appelera `htdocs` et le second `repository`.

Vous devriez donc avoir une architecture de dossier comme ci dessous :

{% highlight html %}

/.Racine de votre serveur/
├── mon-site-web/
│   ├── htdocs/
│   │  
│   ├── Repository/

{% endhighlight %}

## Configurer le domaine

Le soucis à ce niveau c'est que tout est prêt mais notre domaine point à la racine et non dans le dossier `htdocs`. La solution est donc de se rendre dans le panneau d'_administration de 1&1_, dans la section "Domaines" et de cliquer sur "gestion des domaines". Un panneau récapitulatif de vos domaines devrait s'afficher. Sélectionnez celui que vous voulez faire pointer sur votre dossier `htdocs` et dans le champ "dossier" saisissez le chemin jusqu'à `htdocs` puis cliquez sur enregister.

`Dossier : /mon-site-web/htdocs/`

Maintenant votre domaine pointera directement sur ce dossier.

## Initialiser Git

Passons maintenant au chose sérieuse. Nous allons intialiser **Git** dans notre dossier `Repository`. Pour cela nous allons nous placer dans ce même dossier avec la commande :

{% highlight html linenos %}
cd mon-site-web/repository
{% endhighlight %}

 Une fois à l'intérieur il ne nous reste plus qu'à lancer la commande suivante :

{% highlight html linenos %}
git init --bare
{% endhighlight %}

**Git** est alors initialiser dans votre dossier. Il nous reste encore à spécifier à Git que nous voulons que nos fichiers "pusher" soit dans le dossier `htdocs`. Pour cela rendez-vous dans `repository -> hooks` et ouvrez le fichier `post-receive.sample`. A l'intérieur de se fichier nous allons copier la commande suivante :

{% highlight html linenos %}
#!/bin/sh
GIT_WORK_TREE="../htdocs" git checkout -f
{% endhighlight %}

Il faut ensuite supprimer l'extension `.sample`afin que le fichier soit pris en compte par Git.

Pour s'assurer que le "hook" s'éxécutera comme il faut,  nous allons lancer la commande suivante :

{% highlight html linenos %}
chmod +x post-receive
{% endhighlight %}

## Du répertoire local au serveur

Placer vous dans le dossier ou ce trouve votre site ou créer un dossier dans lequel vous aller "pusher" votre site web du répertoire local au serveur web. Pour l'exemple nous allons créer un dossier `site-local` dans lequel nous allons insérer un simple fichier `index.html` en guise de test. Un simple "Hello World!" suffira !

Placez vous dans ce dossier en ligne de commande :

{% highlight html linenos %}
  cd site-local/
{% endhighlight %}

Et intialiser Git à l'intérieur :

{% highlight html linenos %}
cd site-local/
git init
git add .
git commit -m "Premier commit"
{% endhighlight %}

Il nous faut maintenant lier le dossier distant avec le répertoire locale que nous venons de créer, pour ca, toujours dans le dossier `site-local`, nous allons entrer la commande suivante :

{% highlight html linenos %}
git remote add web "ssh://[utilisateur]@[domaine.com]/~/mon-site-web/repository/"
{% endhighlight %}

Veillez à bien remplacer les informations entre [ ] par vos identifiants.

Il ne nous reste plus qu'à "pusher" notre site :

{% highlight html linenos %}
git push web +master:refs/heads/master
{% endhighlight %}

Votre mot de passe **SSH** vous sera demander. Et votre projet vas ce "pusher" gentilement sur votre serveur web!

Voilà vous avez un système de _versionning_ afin de développer votre site web en local en sécurité et de le &quot;pusher&quot; quand vous penser que vos modifications sont OK. Pratique et surtout cela vous entraîne à avoir un bon workflow.