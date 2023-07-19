# Documentation environnement Chroot

## Création de l'utilisateur
Créez un utilisateur avec un dossier personnel dans /home/nom_du_user :

```
sudo adduser nom_du_user
```
ou
```
sudo useradd -m nom_user
```
```
sudo passwd nom_user
```

## Modification du shell par défaut de l'utilisateur

Modifiez le shell par défaut de l'utilisateur :
```
sudo usermod -s /bin/bash nom_du_user
```

Pour vérifier le shell de l'utilisateur
```
cat /etc/passwd | grep nom_du_user
```

## Création du dossier pour le site.

Créez un dossier pour le site dans /var/www/nom_du_user :

```
sudo mkdir /var/www/nom_du_user
```
## Modification des propriétaires et des permissions des dossiers.

On créer le repertoire du user :
```
sudo mkdir -pv /home/nom_user
```
```
sudo chown -Rv nom_user:nom_user /home/nom_user
```
```
sudo chmod -Rv 700 /home/nom_user
```

## On créer les dossiers & dépendances necessaires pour les users :

### On créer les repertoires :
```
sudo mkdir -pv /home/nom_user/{bin,lib,lib64,dev,usr,etc}
```
```
sudo cp -v --parents /etc/{passwd,group} /home/nom_user/
```
```
ls -l /dev/{null,zero,stdin,stdout,stderr,random,tty}
```
```
sudo mknod -m 666 /home/nom_user/dev/null c 1 3
```
```
sudo mknod -m 666 /home/nom_user/dev/random c 1 8
```
```
sudo mknod -m 666 /home/nom_user/dev/tty c 5 0
```
```
sudo mknod -m 666 /home/nom_user/dev/zero c 1 5
```
```
sudo ln -sv /proc/self/fd/2 /home/nom_user/dev/stderr
```
```
sudo ln -sv /proc/self/fd/0 /home/nom_user/dev/stdin
```
```
sudo ln -sv /proc/self/fd/1 /home/nom_user/dev/stdout
```

### On copie les commandes pour le user

Minimal
```
sudo cp -v /bin/{bash} /home/nom_user/bin
```

Optionel
```
sudo cp -v /bin/{bash,ls,cat,nano,mv,mkdir} /home/nom_user/bin
```

Minimal
```
dlist="$(ldd /bin/{bash} | egrep -o '/lib.*\.[0-9]')"
```
```
for i in $dlist; do sudo cp -v --parents "$i" "/home/nom_user"; done
```
Optionel
```
dlist="$(ldd /bin/{bash,ls,cat,nano,mv,mkdir} | egrep -o '/lib.*\.[0-9]')"
```
```
for i in $dlist; do sudo cp -v --parents "$i" "/home/nom_user"; done
```

### Ces commandes permettent egalement de copier les libraires necessaires au fonctionement de la commande

Les 2 prochaines commandes peuvent avoir besoin d'un accès Root (su)
```
ldd /bin/bash | grep "=>" | awk '{print $3}' | xargs -I '{}' cp -v '{}' /home/nom_du_user/lib
```
```
sudo cp --parents $(ldd /bin/bash | awk '/\/lib64/ {print $1}') /home/nom_du_user/lib64
```

## Ajout de l'utilisateur au groupe apache

Ajoutez l'utilisateur à un groupe pour lui donner accès au dossier www :

```
sudo usermod -aG www-data nom_user
```

## Création d'un lien symbolique
On créer le repertoire du user
```
sudo mkdir /home/nom_du_user/private
```
Créez un lien symbolique du dossier dans /var/www/nom_du_user vers le dossier personnel de l'utilisateur :
```
sudo ln -s /var/www/nom_du_user /home/nom_du_user/private/www
```


## On modifie la configuration SSH
```
sudo nano /etc/ssh/sshd_config
```
A mettre a la fin du fichier
```
Match User nom_user
  ChrootDirectory /memeusers/userNOM_USER/private
```

On redemarre le service ssh
```
sudo systemctl restart ssh
```
```
sudo systemctl status ssh
```


## Test de l'environnement chroot

Testez l'environnement chroot en vous connectant en tant qu'utilisateur :
```
sudo chroot /home/nom_du_user/chroot /bin/bash
```
