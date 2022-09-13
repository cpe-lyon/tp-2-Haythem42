BELHADJ MANSOUR Haythem
3ICS - CPE Lyon
2022-2023
# TP 2 - Bash

## Exercice 1

1 - Les commandes tapées par l'utilisateur se trouve dans les dossiers :
* /softwares/bin
* /softs/bin
* /usr/local/cpe/bin
* /usr/local/cpe/sbin
* /usr/local/sbin
* /usr/local/bin
* /usr/sbin
* /usr/bin
* /sbin
* /bin

Pour les trouver, on utilise la commande bash
``printenv PATH``.

2 - La variable d'environnement HOME permet à la commande **cd** tapée sans argument de vous ramener dans le répertoire personnel.

3 - Pour trouver des informations sur les variables d'environnement, on peut utiliser la commande ``printenv``. Pour une variable particulière, nous utiliserons ``printenv nomVariable``.

La variable LANG détermine la langue que les logiciels utilisent pour communiquer avec l'utilisateur.
La variable PWD détermine le chemin du répertoire courant dans lequel l'utilisateur est.
La variable OLDPWD détermine le chemin du répertoire courant dans lequel l'utilisateur était ultérieurement. Si l'utilisateur n'a pas changé de répertoire courant, la variable OLDPWD est vide.
La variable SHELL détermine l'interpréteur de commande utilisateur.

4 - Pour créer une variable locale, on utilise la commande ``nomVariable="contenu"``.
Ici, nous utilisons `MY_VAR="Test"`.
Pour vérifier son existence, il faut taper `echo $MY_VAR` et le système devrait retourner **Test**.

5 - La commande **bash** permet d'avoir un interpréteur bash dans l'interpréteur actuel. On entre dans un sous-niveau.
La variable **MY_VAR** n'existe pas car nous ne somme plus dans le même interpréteur. La variable étant enregistré localement dans l'interpréteur précédent, elle n'est pas définie ici.
La commande **exit** nous permet de revenir dans la session précédant la commande **bash**. Nous retrouvons ici notre variable **MY_VAR**.

6 - Pour transformer une variable locale en variable d'environnement, on peut utiliser la commande `export MY_VAR=Test`. En tapant la commande **bash** pour aller dans une sous-section, la variable est maintenant reconnue. On peut la trouver en tapant `echo $MY_VAR` ou `printenv MY_VAR`. C'est dû au fait qu'une variable d'environnement peut être accessible un peu partout dans le système.

7 - Pour créer une variable d'environnement contenant des espaces, il faut faire attention à bien mettre des guillemets, sinon seul le premier argument sera retenu. Ici, la commande étant :
`export NOM="Haythem BELHADJ MANSOUR"`
On vérifie avec `echo $NOM` et/ou `printenv NOM`, les résultats retournés sont bien **Haythem BELHADJ MANSOUR** dans les 2 cas.

8 - Pour afficher ”Bonjour à vous, *prenom nom* !” en utilisant la variable NOM, on utilise la commande `echo "Bonjour à vous, $NOM!"`. Cela nous retourne **Bonjour à vous, Haythem BELHADJ MANSOUR!**.

9 - La différence entre donner une valeur vide à une variable et utiliser la commande **unset** est quand donnant un valeur vide, la variable existe mais est nulle. Avec **unset**, les variables passées en paramètre sont effacées de la mémoire.

10 - Si l'on souhaite écrire le terme **$HOME** sans qu'il soit interprété comme une variable, on doit le placer entre de simples quotes. Ainsi, si l'on souhaite écrire exactement à l'aide de la commande **echo** : $HOME = *chemin*  (où chemin est notre dossier personnel d’après bash); on peut faire de cette manière : 

``echo '$HOME = '$HOME``

## Programmation Bash

Pour créer notre dossier script dans notre répertoire personnel, on utilise la commande **mkdir script** dans notre répertoire personnel.
Pour ajouter le chemin vers le dossier script au PATH, et ce de manière permanente, il suffit de taper la commande **PATH=$PATH:~/script**
