## Etape 1 : Mise à jour du système
```
sudo apt update
sudo apt upgrade
```

<hr>

## Etape 2 : SSH et Firewall

### On installe UFW
```
sudo apt install ufw
```
### On active UFW
```
sudo ufw enable
```
### On autorise le trafic nécessaire au fonctionnement du serveur
```
sudo ufw allow OpenSSH
sudo ufw allow in "WWW Full"
```

### On modifie le port SSH
```
sudo nano /etc/ssh/sshd_config
```
On modifie la ligne `Port 22` en `Port 2222` et on sauvegarde le fichier.

### On autorise le trafic sur le port 2222
```
sudo ufw allow 2222/tcp
```

### On redémarre le service SSH
```
sudo systemctl restart ssh
```

### On redémarre UFW
```
sudo systemctl restart ufw
```

### On génère une clé SSH
```
sudo ssh-keygen -t ed25519
```

<hr>

## Etape 3 : Installation d'un LAMP

### On installe Apache
```
sudo apt install apache2
```

### On installe MariaDB
```
sudo apt install mariadb-server
sudo mysql_secure_installation
```

### On installe PHP
```
sudo apt install php libapache2-mod-php php-mysql
```

<hr>

## Etape 4 : On insalle Certbot
```
sudo apt install snapd
sudo snap install core
sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

<hr>

## Etape 5 : On installe Git
```
sudo apt install git
```