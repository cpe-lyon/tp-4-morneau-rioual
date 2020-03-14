<h1 align="center" style="box-shadow: 10px 5px 5px red">Compte rendu TP4</h1>                                   
<p>RIOUAL Matthieu :computer:</p>
<p>MORNEAU Hugo :computer:</P>

## Exercice 1

1) La commande permettant d'ajouter un groupe au système :
>sudo addgroup groupe1
2) Pour créer nos différents utilisateurs on fait appel à la commande useradd avec les option m pour que ceux ci aient leur dossier home et --shell pour indiquer le chemin de son interprétateur de commande (ici bash).
>sudo useradd ux -m --shell /bin/bash
3) On ajoute les utilisateurs dans leurs différents groupes (secondaires) de la manière suivante :
>sudo usermod -a -G groupex ux
4) On affiche les membres de groupe2 de deux facon possibles :
   > * cat /etc/group|grep groupe2
   >
   > * cat /etc/gshadow|grep groupe2
5) Pour changer le groupe propriétaire de nos fichiers ```/home/ux```, nous procédons ainsi pour chaque utilisateur:
>sudo chgrp groupex /home/ux
6) Pour changer le groupe primaire de nos utilisateurs, nous procédons ainsi pour chaque utilisateur:
>sudo usermod -g groupex ux
7) Les lignes suivantes permettent de créer deux fichiers ne pouvant etre lus et modifiés que par les membres de leur groupe respectif :
> * mkdir -p {groupe1,groupe2}
> * chgrp groupe1 groupe1|chgrp groupe2 groupe2
> * chmod 070 groupe1|chmod 070 groupe2
8) Pour permettre la suppression et le renomage uniquement par le propriétaire, on active le sticky bit de la maniere suivante ;
>chmod +t fichier
9) Si nous ne sommes pas connecté en tant que root, il nous est impossible d'effectuer la commande ```su u1``` ca aucun mot de passe n'a été défini lors de la crétion de cet utilisateur.
10) Pour activer cet utilisateur, nous devons définir un mot de passe avec la commande suivante ```passwd u1``` ce qui nous permet ensuite de nous connecter en tant que user u1. Le début de la ligne de commande devient alors u1@serveur.
11) Nous obtenons les informations suivantes en tapant la commande ```id u1```:
* uid=1001(u1)
* gid=1001(groupe1)
Ces résultats sont cohérents avec les données receuilli dans ```/etc/passwd``` et ```/etc/group```
12) En regardant dans le fichier /etc/passwd, on s'apercoit que u3 possède l'uid 1003.
13)En regardant dans le fichier /etc/group, le groupe1 possède le gid 1001
14) En effectuant la commande :
>cat /etc/group|grep :1002: 
On obtient le groupe2 et on évite tout risque de conflit entre guid et nom de groupe
15) On retire l'utilisateur u3 de groupe 2 de la manière suivante :
>gpasswd -d u3 groupe2
On peut alors constater que u3 a disparu des utilisateurs du groupe2 dans /etc/group.
16) Voici une série d'instruction ainsi que les fonctions qu'elles réalisent :

|          Commande                  |                                     Fonction                                               |
|------------------------------------|--------------------------------------------------------------------------------------------|
| usermod --expiredate 2020-06-01 u4 |  configurer une date d'expiration d'un utilisateur                                         |
| passwd --maxdays 90 u4             |    nécessite le changement de mot de passe sous 90 jours maximum                           |
| passwd --mindays 5 u4              | impose un délai minimum entre deux changement de mot de passe                              |
| passwd --warndays 14 u4            | crée un avertissement 14 jours avant l’expiration de son mot de passe                      |
| passwd --inactive 30 u4            | désactive un compte utilisateur sous un délai de 30 jours après expiration de mot de passe |

17) Grace à la commande ```cat /etc/passwd |grep "root"``` on peut constater que l'interpreteur de commande est le bash situé dans /bin/bash
18) Il s'agit de l'utilisateur qui représente l'utilisateur avec le moins de permissions
19) On retrouve le temps de mémoire tempon du mort de passe du superutilisateur dans le manuel grace à la commande ```man sudo```. Par défaut, le time stamp est de 15 minutes.
```sudo -k``` permet d'effacer le mot de passe concervé en mémoire après une commande sudo

## Exercice 2

1) >mkdir test|touch test/fichier
>ls -l
rwxr-xr-x dossier
rw-r--r-- fichier
2)chmod 000 test/fichier
En tant que root, on peut tout de meme le modifier et l'afficher. Par conséquent, les droits ne s'appliquent pas sur root
3)Les droits permettent d'pas reconnu par l'interpreteur
5) Permission denied On ne peut pas lister le contenu du répertoire. Les droits du dossier s'appliquent sur son contenu
6) 
chmod -w nom_fichier
chmod -w nom_dossier

On ne peut pas écrire dans le fichier nouveau mais on peut le supprimer.
Pour empecher la supression, nous devons configurer les droits du dossier 

7) On ne peut plus se déplacer ni lire le contenu après avoir supprimé le droit d'exécution.
cd ..|chmod -x test
8) En se placant dans le répertoire, on ne peut plus rien faire, en outre on ne peut plus aller dans les sous dossiers. Les droits du repertoire parent s'applique aux repertoires enfants. La commande cd .. fonctionne car elle ne s'applique pas au repertoire dont on ne possède pas les droits
9) chmod 740 test_fichier 
10) umask 077
11) umask 022
12) umask 033
13) chmod 534
chmod 602
chmod u-x,g+r,o+w fic
chmod 620
14) On se place dans le dossier /etc et on effectue la commande ```ls -l|grep passwd```
Root autorisé à écrire dedans tandis que les autres peuvent juste lire ce qui est logique puisque root gère les utilisateurs.
