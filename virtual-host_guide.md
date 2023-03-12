# Guide virtual-host pour un serveur web apache

## On créer votre répertoire dans /var/www
```
sudo mkdir -p /var/www/nom_de_votre_site
```

## On modifie les droits du répertoire
```
sudo chown -R www-data:www-data /var/www/votre_nom_de_domaine
```
```
sudo chmod -R 755 /var/www/votre_nom_de_domaine
```

## On créer le fichier de configuration de votre site

### On ce déplace dans le répertoire des virtual-host
``` 
cd /etc/apache2/sites-available
```

### On créer une copie du fichier 000-default.conf
```
sudo cp 000-default.conf nom_de_votre_site.conf
```
![Image Fichier Config](/images/vhost/config.png )

## Voici un exemple de configuration
```
<VirtualHost *:80>
    ServerAdmin Votre_Adresse_Mail
    ServerName URL_De_Votre_Site
    DocumentRoot /var/www/Nom_De_Votre_Site
    
    ErrorLog ${APACHE_LOG_DIR}/error-VotreNom.log
    CustomLog ${APACHE_LOG_DIR}/access-VotreNom.log combined
</VirtualHost>
```

## Une fois que vous avez terminé de configurer votre fichier de configuration
### On désactive le site par défaut
### On active le site que vous venez de créer
```
sudo a2dissite 000-default.conf
```
```
sudo a2ensite nom_de_votre_site.conf
```

## On redémarre le service apache2
```
sudo systemctl restart apache2
```

## On configure le certificat SSL

### On installe le paquet certbot
```
sudo apt install certbot python3-certbot-apache
```

### On génère le certificat SSL
```
sudo certbot --apache
```

### On redémarre le service apache2
```
sudo systemctl restart apache2
```