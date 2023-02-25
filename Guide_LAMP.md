# Guide d'installation d'un LAMP sur Debian 10

## Mise à jour du système

```
sudo apt-get update
sudo apt-get upgrade -y
```

## Installation de Apache

### On vériifie que le service apache2 est bien installé

```
sudo apachectl -v
```

### Si le service n'est pas installé, on l'installe

```
sudo apt-get install apache2 -y
```


## Installation de PHP

### On vériifie que le service php est bien installé

```
php -v
```

### Si le service n'est pas installé, on l'installe

```
sudo apt-get install php libapache2-mod-php -y
sudo apt-get install php-mysql -y
```


## Installation de MySQL

### On vériifie que le service mysql est bien installé

```
sudo mysql -V
```

### Si le service n'est pas installé, on l'installe

```
sudo apt-get install mysql-server -y
```
### Si MySql ne veux pas s'installer, on peut essayer d'installer MariaDB

```
sudo apt-get install mariadb-server -y
```

### On configure le service mysql

```
sudo mysql_secure_installation
```

[//]: # (---------------------------------------------------------------------------------------------)

## Configurations Apache

### ATTENTION ! Ne faite pas de copier/coller, il faut modifier certaines lignes en fonction de votre nom de site et de votre adresse mail.

## Etape 1

### On crée un fichier de configuration apache pour notre site
### On se place dans le dossier des sites-available
### On copie le fichier de configuration par défaut et on le renomme

````
cd /etc/apache2/sites-available
cp 000-default.conf nom_de_votre_site.conf
````

## Etape 2

### On modifie le fichier de configuration

```
sudo nano nom_de_votre_site.conf
```

### Modéle de fichier de configuration
    
```
<VirtualHost *:80>
    ServerAdmin Votre_Adresse_Mail
    ServerName URL_De_Votre_Site
    DocumentRoot /var/www/Nom_De_Votre_Site
    
    ErrorLog ${APACHE_LOG_DIR}/error-VotreNom.log
    CustomLog ${APACHE_LOG_DIR}/access-VotreNom.log combined
</VirtualHost>
```

## Etape 3

### On active le site

```
sudo a2ensite nom_de_votre_site.conf
```

## Etape 4

### On redémarre le service apache2

```
sudo systemctl restart apache2
```

## Etape 5

### On crée le dossier du site

```
sudo mkdir /var/www/Nom_De_Votre_Site
```

## Etape 6

### On se connecte à MySql

```
sudo mysql -u root -p
```

### On créer un utilisateur

```
CREATE USER 'Nom_De_Votre_Utilisateur'@'localhost' IDENTIFIED BY 'Mot_De_Passe';
```

### On créer une base de donnée

```
CREATE DATABASE Nom_De_Votre_BDD;
```

### On donne les droits à l'utilisateur

```
GRANT ALL PRIVILEGES ON Nom_De_Votre_BDD.* TO 'Nom_De_Votre_Utilisateur'@'localhost';
```

## Installation de Wordpress

### ATTENTION ! Utilisateur est à remplacer par le nom de votre utilisateur ou Debian

### On se place dans le dossier de l'utilisateur
### On télécharge Wordpress

```
cd /home/Utilisateur

wget https://wordpress.org/latest.tar.gz
```
### On donne les permissions au dossier

```
 sudo chmod 755 /var/www/Nom_De_Votre_Site
```

### On déplace le fichier dans le dossier

```
sudo mv latest.tar.gz /var/www/Nom_De_Votre_Site
```

### On se place dans le dossier du site

```
cd /var/www/Nom_De_Votre_Site
```

### On décompresse le fichier

```
sudo tar -xzvf latest.tar.gz
```

### On supprime le fichier

```
sudo rm latest.tar.gz
```

### On donne les droits au dossier

```
sudo chown -R www-data:www-data /var/www/Nom_De_Votre_Site

sudo chmod -R 755 /var/www/Nom_De_Votre_Site
```
