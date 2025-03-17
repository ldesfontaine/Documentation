# Documentation : Installation et Configuration de MicroK8s sur Debian

Ce guide détaille étape par étape comment installer MicroK8s sur une machine Debian, activer et configurer les addons essentiels (y compris un registre privé sécurisé et le Dashboard), et enfin déployer un site web. Il inclut également quelques recommandations de configuration de pare-feu pour sécuriser l'accès aux services.

---

## Table des Matières

- [Introduction](#introduction)
- [Prérequis](#prérequis)
- [Installation de MicroK8s sur Debian](#installation-de-microk8s-sur-debian)
- [Configuration et Activation des Addons](#configuration-et-activation-des-addons)
    - [Activation des Addons de Base](#activation-des-addons-de-base)
    - [Configurer le Registre Privé avec Authentification](#configurer-le-registre-privé-avec-authentification)
    - [Configurer le Dashboard Kubernetes](#configurer-le-dashboard-kubernetes)
- [Exemple d’Hébergement d’un Site Web](#exemple-dhébergement-dun-site-web)
    - [Fichier de Déploiement (Deployment YAML)](#fichier-de-déploiement-deployment-yaml)
    - [Fichier de Service (Service YAML)](#fichier-de-service-service-yaml)
    - [Fichier Ingress avec Let's Encrypt (Ingress YAML)](#fichier-ingress-avec-lets-encrypt-ingress-yaml)
- [Recommandations pour le Pare-feu](#recommandations-pour-le-pare-feu)
- [Conclusion](#conclusion)

---

## Introduction

Ce guide a pour but de te permettre de :
- Installer MicroK8s sur une machine Debian en mode standalone.
- Activer et configurer des addons essentiels tels que DNS, Ingress, Storage, Cert-Manager, Registry et Dashboard.
- Configurer un registre privé avec authentification pour stocker et récupérer tes images Docker.
- Déployer un exemple de site web (hébergé via un Deployment, Service et Ingress avec certificat SSL Let's Encrypt).
- Appliquer une règle de pare-feu pour limiter l'accès aux services.

---

## Prérequis

- Une machine Debian (ou dérivée) avec accès à Internet.
- Accès en sudo (root).
- Snapd installé (pour installer les snaps).
- Un nom de domaine (par exemple `site1.lalaland.com`) pointé vers l’IP publique de ton serveur.
- (Optionnel) Un dépôt Git contenant ton projet ou une application à déployer.

---

## Installation de MicroK8s sur Debian

1. **Mettre à jour les paquets :**
   ```bash
   sudo apt update
   ```

2. **Installer Snapd :**
   ```bash
   sudo apt install snapd -y
   sudo systemctl enable --now snapd.socket
   ```

3. **Installer MicroK8s :**
   ```bash
   sudo snap install microk8s --classic
   ```

4. **Ajouter l'utilisateur courant au groupe MicroK8s :**
   ```bash
   sudo usermod -a -G microk8s $USER
   sudo chown -f -R $USER ~/.kube
   ```
   Déconnecte-toi et reconnecte-toi (ou utilise `newgrp microk8s`) pour appliquer le changement.

5. **Vérifier l'installation :**
   ```bash
   microk8s status --wait-ready
   microk8s kubectl get nodes
   ```
   Ton nœud doit apparaître avec le statut "Ready".

---

## Configuration et Activation des Addons

### Activation des Addons de Base

Active les addons indispensables :
```bash
microk8s enable dns ingress storage cert-manager registry dashboard
```
- **dns** : pour la résolution interne.
- **ingress** : pour exposer tes applications via un Ingress.
- **storage** : pour la gestion du stockage persistant.
- **cert-manager** : pour obtenir automatiquement des certificats Let's Encrypt.
- **registry** : pour disposer d'un registre Docker privé accessible sur le port 32000.
- **dashboard** : pour accéder à une interface graphique de gestion du cluster.

---

### Configurer le Registre Privé avec Authentification

1. **Générer un fichier d’authentification :**
   ```bash
   sudo apt install apache2-utils -y
   htpasswd -c auth admin
   ```
   *Saisis le mot de passe souhaité pour l’utilisateur "admin".*

2. **Créer un Secret Kubernetes pour le registre :**
   ```bash
   microk8s kubectl create secret generic registry-basic-auth --from-file=auth
   ```

3. **Modifier le déploiement du registre :**
   ```bash
   microk8s kubectl edit deployment registry -n container-registry
   ```
   Ajoute les variables d’environnement :
   ```yaml
   env:
     - name: REGISTRY_AUTH
       value: "htpasswd"
     - name: REGISTRY_AUTH_HTPASSWD_REALM
       value: "Registry Realm"
     - name: REGISTRY_AUTH_HTPASSWD_PATH
       value: "/auth/auth"
   ```
   Ajoute ensuite un volumeMount pour monter le secret :
   ```yaml
   volumeMounts:
     - name: auth
       mountPath: /auth
   ```
   Dans la section `volumes` du pod, ajoute :
   ```yaml
   - name: auth
     secret:
       secretName: registry-basic-auth
   ```
   Sauvegarde et quitte l’éditeur.

---

## Recommandations pour le Pare-feu

Pour sécuriser l'accès à tes services, configure ton pare-feu pour n’autoriser que le trafic nécessaire.

### Exemple pour le Registre Privé (port 32000)

Si tu utilises **ufw** sur Debian :

```bash
# Bloquer le trafic par défaut sur le port 32000
sudo ufw deny 32000/tcp

# Autoriser uniquement une plage d'IP (exemple : 192.168.1.0/24)
sudo ufw allow from 192.168.1.0/24 to any port 32000 proto tcp
```
---

## Conclusion

Ce guide t’a présenté :

- **L'installation de MicroK8s sur Debian** (via snap).
- **La configuration et activation d'addons essentiels** (DNS, Ingress, Storage, Cert-Manager, Registry, Dashboard).
- **La sécurisation d'un registre privé** avec authentification et la configuration d'un compte admin pour le Dashboard.
- **Des recommandations de configuration de pare-feu** pour limiter l'accès aux services critiques.

MicroK8s offre une solution légère et évolutive qui peut être utilisée sur un serveur standalone et étendue en cluster si nécessaire.

---
