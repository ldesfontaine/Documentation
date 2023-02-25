# Guide de sécurisation d'un serveur web

## Introduction

La sécurité est une préoccupation majeure pour les administrateurs de serveurs web. Il est important de prendre des mesures pour protéger votre serveur contre les attaques malveillantes et les violations de données. Ce guide fournit des méthodes recommandées pour sécuriser votre serveur web sous Debian 10.

## Configuration du pare-feu

La première étape pour sécuriser votre serveur web consiste à configurer le pare-feu pour bloquer tout trafic non autorisé. La commande suivante installe le pare-feu ufw :

```
sudo apt-get install ufw
```
Ensuite, vous pouvez activer le pare-feu en exécutant les commandes suivantes :

```
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
```
Cela permet de bloquer tout trafic entrant, sauf celui que vous avez expressément autorisé. Par exemple, si vous voulez autoriser le trafic HTTP (port 80), vous pouvez exécuter la commande suivante :

```
sudo ufw allow 80/tcp
```
Vous pouvez également autoriser le trafic HTTPS (port 443) en exécutant la commande suivante :

```
sudo ufw allow 443/tcp
```
## Mise à jour du système

Il est important de maintenir votre système à jour avec les derniers correctifs de sécurité et les mises à jour logicielles. Pour mettre à jour votre système, exécutez les commandes suivantes :

```
sudo apt-get update
sudo apt-get upgrade
```
## Configuration SSH

L'accès SSH à votre serveur doit être sécurisé pour empêcher les attaques par force brute. Vous pouvez renforcer la sécurité de SSH en modifiant le port par défaut et en utilisant des clés d'authentification plutôt que des mots de passe. Pour modifier le port SSH par défaut, ouvrez le fichier de configuration SSH avec la commande suivante :

```
sudo nano /etc/ssh/sshd_config
```
Modifiez la ligne #Port 22 pour spécifier un nouveau port (par exemple, Port 2200), puis enregistrez le fichier. Vous pouvez maintenant vous connecter en utilisant le nouveau port :

```
ssh user@your_server_ip -p 2200
```
Pour utiliser des clés d'authentification, vous devez générer une paire de clés sur votre ordinateur local et transférer la clé publique sur votre serveur. Exécutez la commande suivante sur votre ordinateur local pour générer une paire de clés :

```
ssh-keygen
```
Ensuite, copiez la clé publique sur votre serveur avec la commande suivante :

```
ssh-copy-id user@your_server_ip
```
Maintenant, vous pouvez vous connecter à votre serveur en utilisant la clé privée :

```
ssh user@your_server_ip -i ~/.ssh/id_rsa
```
## SSL/TLS

SSL/TLS est une technologie de chiffrement qui protège les données transitant entre votre serveur web et les navigateurs des utilisateurs. Pour activer SSL/TLS, vous devez installer un certificat SSL sur votre serveur. Il existe de nombreuses autorités de certification (CA) qui fournissent des certificats SSL .


Alternativement, vous pouvez utiliser Let's Encrypt, qui fournit des certificats SSL gratuits et automatisés. Pour installer Let's Encrypt, exécutez les commandes suivantes :

```
sudo apt-get install certbot python-certbot-apache
```
Ensuite, exécutez la commande suivante pour obtenir un certificat SSL Let's Encrypt :

```
sudo certbot --apache
```
Suivez les instructions pour fournir votre adresse e-mail et choisir le nom de domaine pour lequel vous souhaitez obtenir un certificat SSL. Une fois le certificat installé, votre serveur web sera automatiquement configuré pour utiliser HTTPS.

## Sécurisation des applications web

Il est important de sécuriser les applications web que vous exécutez sur votre serveur. Voici quelques mesures de sécurité recommandées :

Utilisez des mots de passe forts et différents pour chaque application web.
Désactivez les comptes d'utilisateurs inactifs.
Restreignez l'accès aux fichiers et dossiers sensibles.
Utilisez des frameworks et des bibliothèques sécurisés pour votre application web.
Limitez la quantité de données téléchargées sur votre serveur.

## Installation et configuration de Fail2ban

Fail2ban est un outil de sécurité qui surveille les fichiers journaux du serveur pour détecter les tentatives de connexion échouées et les attaques par force brute, et bannit les adresses IP des attaquants en réponse. Pour installer Fail2ban, exécutez la commande suivante :

```
sudo apt-get install fail2ban
```
Une fois l'installation terminée, vous devez configurer Fail2ban en modifiant le fichier de configuration principal, qui se trouve dans le dossier /etc/fail2ban/jail.conf. Vous pouvez utiliser un éditeur de texte tel que nano pour modifier ce fichier :

```
sudo nano /etc/fail2ban/jail.conf
```
Dans ce fichier, vous pouvez configurer les règles de sécurité pour différents services. Par exemple, vous pouvez ajouter la règle suivante pour protéger votre serveur SSH :

```
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600
```
Cette règle active la surveillance du service SSH, défini le nombre maximum de tentatives de connexion autorisées avant le bannissement, et le temps de bannissement en secondes.

Ensuite, vous devez redémarrer le service Fail2ban pour appliquer les modifications de configuration :

```
sudo systemctl restart fail2ban
```

## Mise en place d'une solution de journalisation

## Installation de rsyslog

Le service de journalisation par défaut sur Debian 10 est rsyslog. Pour installer rsyslog, utilisez la commande suivante :

```
sudo apt-get update
sudo apt-get install rsyslog
```
## Configuration de rsyslog

Une fois rsyslog installé, vous devez configurer les règles de journalisation. Pour cela, ouvrez le fichier /etc/rsyslog.conf dans votre éditeur de texte préféré :

```
sudo nano /etc/rsyslog.conf
```
Dans ce fichier, vous pouvez ajouter des règles pour spécifier où stocker les fichiers journaux et quels types d'événements doivent être enregistrés. Par exemple, vous pouvez ajouter la règle suivante pour enregistrer tous les événements dans un fichier journal spécifique :

```
*.* /var/log/mylogfile.log
```
Une fois que vous avez ajouté vos règles de journalisation, enregistrez et quittez le fichier.

## Redémarrage de rsyslog

Pour que les modifications apportées à la configuration de rsyslog prennent effet, vous devez redémarrer le service rsyslog :

```
sudo systemctl restart rsyslog
```


## Conclusion

La sécurité est un processus continu et en évolution. Ce guide fournit des méthodes de sécurité recommandées pour sécuriser votre serveur web sous Debian 10. En suivant ces étapes, vous pouvez aider à protéger votre serveur contre les attaques malveillantes et les violations de données.


## Autres outils de sécurité recommandés

ModSecurity : un pare-feu applicatif Web (WAF) qui détecte et bloque les attaques de sécurité HTTP.

AppArmor : un outil de sécurité qui limite les privilèges des applications pour réduire les risques de violation de sécurité.

ClamAV : un logiciel antivirus open source qui peut être utilisé pour détecter les virus et autres logiciels malveillants sur votre serveur.

RKHunter : un outil de détection de rootkits qui peut être utilisé pour vérifier la sécurité de votre système.