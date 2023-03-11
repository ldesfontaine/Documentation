# Documentation environnement Chroot

## Création de l'utilisateur
Créez un utilisateur avec un dossier personnel dans /home/nom_du_user :

```
sudo adduser nom_du_user
```
## Création du dossier pour le site.

Créez un dossier pour le site dans /var/www/nom_du_user :

```
sudo mkdir /var/www/nom_du_user
```
## Modification des propriétaires et des permissions des dossiers.

Changez les propriétaires et les permissions des dossiers :

```
sudo chown nom_du_user:nom_du_user /home/nom_du_user
```
```
sudo chown -R nom_du_user:www-data /var/www/nom_du_user
```
```
sudo chmod -R 755 /var/www/nom_du_user
```
## Copie des fichiers nécessaires pour l'environnement chroot :

```
sudo mkdir /home/nom_du_user/chroot
```
```
sudo cp /bin/bash /home/nom_du_user/chroot/bin
```
```
sudo mkdir -p /home/nom_du_user/chroot/{lib,lib64}
```
Les 2 prochaines commandes peuvent avoir besoin d'un accès Root (su)
```
ldd /bin/bash | grep "=>" | awk '{print $3}' | xargs -I '{}' cp -v '{}' /home/nom_du_user/chroot/lib
```
```
sudo cp --parents $(ldd /bin/bash | awk '/\/lib64/ {print $1}') /home/nom_du_user/chroot/
```
Ces commandes créent un dossier "chroot" dans le dossier personnel de l'utilisateur, copient le binaire "bash" et toutes ses bibliothèques partagées nécessaires pour l'environnement chroot.

## Création d'un lien symbolique
On créer le repertoire du user
```
sudo mkdir /home/nom_du_user/private
```
Créez un lien symbolique du dossier dans /var/www/nom_du_user vers le dossier personnel de l'utilisateur :
```
sudo ln -s /var/www/nom_du_user /home/nom_du_user/private/www
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

## Ajout de l'utilisateur à un groupe

Ajoutez l'utilisateur à un groupe pour lui donner accès au dossier www :

```
sudo usermod -aG www-data nom_du_user
```
## Test de l'environnement chroot

Testez l'environnement chroot en vous connectant en tant qu'utilisateur :

```
sudo chroot /home/nom_du_user/chroot /bin/bash
```
Une fois que l'environnement chroot est configuré, vous pouvez installer les applications nécessaires dans le dossier /var/www/nom_du_user, en veillant à ce que les fichiers soient accessibles à l'utilisateur "nom_du_user".
Les commandes ci-dessus devraient vous permettre de créer un environnement chroot pour chaque utilisateur de votre site WordPress.
