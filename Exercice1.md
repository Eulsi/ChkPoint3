## Partie 1 : Gestion des utilisateurs

### Q.2.1.1

````
useradd -m -G sudo frank
passwd frank
````

### Q.2.1.2

En supposant qu'on souhaite se créer un utilisateur ayant malgré tout des privilèges d'administration mais pour un usage personne,
on le placera à sa création dans le groupe "sudo" tout en ajoutant "-m" pour que lui soit associé un répertoire personnel.
Puis on lui définit un mot de passe.
La préconisation principale étant de forcer la sortie des privilèges de l'utilisateur root en utilisant un utilisateur du groupe "sudo" pour des raisons de sécurité.

## Partie 2 : Configuration de SSH

### Q.2.2.1 

````
nano /etc/ssh/sshd_config
````
![permitRootNo](https://github.com/user-attachments/assets/b195f26d-475b-47a2-b3ec-8846c7af382b)



### Q.2.2.2

Ajout de deux lignes dans le fichier "sshd_config"

![sshd_DenyUSErs](https://github.com/user-attachments/assets/b9dcda04-8297-47e5-a959-a6efd805883f)


### Q.2.2.3

De la même manière, on modifie et décommente dans le fichiers "sshd_config" les lignes "PasswordAuthentication yes" en "PasswordAuthentication no"
ainsi que simplement décommenter "PubkeyAuthentication yes"
Enfin pour appliquer ces changements on redémarre le service SSH:
````
systemctl restart ssh
````
(Pour terminer, le serveur ssh est paramétré, mais pour mettre en place une authentification par clés il faut bien sûr la génération et partage d'une clé publique entre serveur et machine cliente)

## Partie 3: Analyse du stockage

### Q.2.3.1

``lsblk`` nous permet d'observer les systèmes de fichiers montés sur la machine.
Les systèmes de fichiers montés sont sur un disque physique "sda" disposant d'une partition "sda1" sur laquelle se trouve le volume raid1 "md0" lui même partitionné en un point de montage de démarrage /boot "md0p1", une partition "md0p2" et "md0p5".
La partition md0p5 semble disposer de deux groupes de volumes gérés par LVM, un groupe monté à la racine et un autre monté en espace swap.

### Q.2.3.2

Ces systèmes de fichiers semblent reposer sur un disque dur physique.

### Q.2.3.3


