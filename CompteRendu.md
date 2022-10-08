
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
Pour ajouter le chemin vers le dossier script au PATH, et ce de manière permanente, il suffit d'ajouter **PATH=$PATH:~/script** à la fin du fichier .bashrc (à l'aide de vim).

## Exercice 2 - Contrôle de mot de passe

```bash
#!/bin/bash

PASSWORD='test123'

# read is used to ask the user to enter a value (-s does'nt show text typed on the keyboard and -p show the text message)
read -s -p "Saisissez un mot de passe : " password

# check if the user's password is the same as PASSWORD
if [ _$password == _$PASSWORD ] ; then
	echo -e '\nLe mot de passe est le même !' # -e param is used for newline (\n)
else
	echo -e '\nLe mot de passe est différent.'
fi
```
![Alt text](ex2.png?raw=true)

## Exercice 3 - Expressions rationnelles

```bash
#!/bin/bash

# function which verify if the parameter is a real number
function is_number()  
{  
	re='^[+-]?[0-9]+([.][0-9]+)?$'
	  
	if ! [[ $1 =~ $re ]] ; then  
		return 1  
	else  
		return 0  
	fi 
}

is_number $1

if [ $? -eq 0 ] ; then # verify the status of is_number (0 = success)
	echo "$1 est un réel !"
else
	if [ -z $1 ] ; then # verify if the first parameter is empty or not
		echo "Erreur, vous n'avez pas entré de paramètre."
	else
		echo "Erreur, $1 n'est pas un réel."
	fi
fi
```
![Alt text](ex3.png?raw=true)

## Exercice 4 - Contrôle d'utilisateur

```bash
#!/bin/bash

if [ -z $1 ] ; then
	echo "Utilisation : $0 nom_utilisateur"
else
	id -u $1 > /dev/null 2>&1
	
	if [ $? == 0 ] ; then
		echo "Utilisateur valide !"
	else
		echo "Cet utilisateur n'existe pas."
	fi
fi
```
![Alt text](ex4.png?raw=true)

## Exercice 5 - Factorielle

```bash
#!/bin/bash

function fact()
{
	number=$1
	
	if [ $number -eq 0 ] ; then
		echo 1
	else
		echo $(( number * `fact $(( number - 1 ))` ))
	fi
}

echo `fact $1`
```
![Alt text](ex5.png?raw=true)

## Exercice 6 - Le juste prix

```bash
#!/bin/bash

number=$((1 + $RANDOM % 1000))
user_number=0

echo "Bienvenue au jeu du juste prix!"

while ! [ $user_number -eq $number ]
do
	read - p "Saisissez un nombre entre 1 et 1000 : " user_number

	if [ $user_number -lt $number ] ; then
		echo "C'est plus!"
	elif [ $user_number -gt $number ] ; then
		echo "C'est moins!"
	else
		echo "Gagné!"
	fi
done
```
![Alt text](ex6.png?raw=true)

## Exercice 7 - Statistiques

1.
![Alt text](ex7-code.png?raw=true)
![Alt text](ex7.png?raw=true)

2.
![Alt text](ex7-code2.png?raw=true)
![Alt text](ex7-2.png?raw=true)
