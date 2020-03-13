<h1 align="center" style="box-shadow: 10px 5px 5px red">Compte rendu TP4</h1>                                   
<p>RIOUAL Matthieu :computer:</p>
<p>MORNEAU Hugo :computer:</P>

## Exercice 1

1) Pour créer deux groupes, on tape la commande suivante : >sudo addgroup groupex
2) >sudo useradd ux -m --shell /bin/bash
3) >sudo usermod -a -G groupex ux
4) >cat /etc/group|grep groupe2
   >cat /etc/gshadow|grep groupe2
5)>sudo chgrp groupex /home/ux
6)>sudo usermod -g groupex ux
7)>mkdir -p {groupe1,groupe2}
>chgrp groupe1 groupe1|chgrp groupe2 groupe2
>chmod go+rwx groupe1|chmod go+rwx groupe2
remarque : Il serait utile de changer les droits pour controller l'accès à ces dossiers (pour l'instant ouverts à tous).
8)chmod 007 fichier => donne tous les droits à l'utilisateur
9)Non car tout compte crée sans mot de passe est inactif jusqu'à l'attribution de celui ci.
10)>passwd u1
11)>id u1    uid=1001(u1) gid=1001
12)>sudo cat /etc/passwd u3 possède l'id 1003
13)>sudo cat /etc/group groupe1 possède l'id 1001
14)On regarde dans le fichier /etc/group
idgroup1 
15)gpasswd -d u3 groupe2
On peut constater que u3 a disparu des utilisateurs du groupe2 dans /etc/group
16)>usermod --expiredate 2020-06-01 u4
>passwd --warndays 14 u4
>passwd --maxdays 90 u4


