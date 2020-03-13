<h1 align="center" style="box-shadow: 10px 5px 5px red">Compte rendu TP4</h1>                                   
<p>RIOUAL Matthieu :computer:</p>
<p>MORNEAU Hugo :computer:</P>

## Exercice 1

1) Pour créer deux groupes, on tape la commande suivante : >sudo addgroup groupex
2) >sudo useradd ux -m --shell /bin/bash
3) >sudo usermod -a -G groupex ux
4) >cat /etc/group|grep groupe2
   >cat /etc/gshadow|grep groupe2
5) >sudo chgrp groupex /home/ux
6) >sudo usermod -g groupex ux
7) >mkdir -p {groupe1,groupe2}
 >chgrp groupe1 groupe1|chgrp groupe2 groupe2
 >chmod go+rwx groupe1|chmod go+rwx groupe2
remarque : Il serait utile de changer les droits pour controller l'accès à ces dossiers (pour l'instant ouverts à tous).
8) chmod 007 fichier => donne tous les droits à l'utilisateur
9) Non car tout compte crée sans mot de passe est inactif jusqu'à l'attribution de celui ci.
10) >passwd u1
11) >id u1    uid=1001(u1) gid=1001
12) >sudo cat /etc/passwd u3 possède l'id 1003
13) >sudo cat /etc/group groupe1 possède l'id 1001
14) On regarde dans le fichier /etc/group
idgroup1 
15) gpasswd -d u3 groupe2
On peut constater que u3 a disparu des utilisateurs du groupe2 dans /etc/group
16) 
> usermod --expiredate 2020-06-01 u4
> passwd --warndays 14 u4
> passwd --maxdays 90 u4
> passwd --inactive 30 u4
> passwd --mindays 5 u4
17) Grace à la commande ```cat /etc/passwd |grep "root"``` on peut constater que l'interpreteur de commande est le bash situé dans /bin/bash
18) Utilisateur qui représente l'utilisateur avec le moins de permissions
19) On retrouve le temps de mémoire tempon du mort de passe du superutilisateur dans le manuel grace à la commande ```man sudo```. Par défaut, le time stamp est de 15 minutes.
sudo -k permet d'effacer le mot de passe concervé en mémoire après une commande sudo

II)

1) >mkdir test|touch test/fichier
>ls -l
rwxr-xr-x dossier
rw-r--r-- fichier
2)chmod 000 test/fichier
En tant que root, on peut tout de meme le modifier et l'afficher. Par conséquent, les droits ne s'appliquent pas sur root
3)Les droits permettent d'empecher aux utilisateurs non autorisés d'accéder au contenu d'un fichier
4) La commande hello n est pas reconnu par l'interpreteur
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
chmod u-x,g+r,o=wx fic
chmod 620
14) On se place dans le dossier /etc et on effectue la commande ```ls -l|grep passwd```
Root autorisé à écrire dedans tandis que les autres peuvent juste lire ce qui est logique puisque root gère les utilisateurs.
