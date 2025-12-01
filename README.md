#  Projet KapsuleKorp - Infrastructure as Code

##  Description

Ce projet implémente une solution d'automatisation d'infrastructure pour KapsuleKorp 
en utilisant **Ansible** pour déployer une pile LEMP (Linux, Nginx, MySQL, PHP).

##  Architecture

### Environnement Staging
- 2 serveurs web (Nginx + PHP-FPM)
- 1 serveur de base de données (MySQL 8.0)

### Environnement Production
- 3 serveurs web (Nginx + PHP-FPM)
- 1 serveur de base de données (MySQL 8.0)

##  Structure du Projet
projet-kapsulekorp-iac/
├── ansible.cfg # Configuration Ansible
├── inventory.ini # Inventaire des serveurs
├── site.yml # Playbook principal
├── group_vars/
│ ├── all/
│ │ ├── vars.yml # Variables globales
│ │ └── vault.yml # Secrets (chiffrés)
│ ├── staging.yml # Variables staging
│ └── production.yml # Variables production
└── roles/
├── common/ # Configuration de base
├── nginx/ # Serveur web
├── mysql/ # Base de données
├── php/ # PHP-FPM
└── app/ # Application web

## 🛠️ Prérequis

- Ansible >= 2.9
- Python 3 sur les machines cibles
- Accès SSH par clé configuré
- Ubuntu 22.04 LTS sur les cibles

##  Installation

### 1. Cloner le projet
git clone <url-du-depot>
cd projet-kapsulekorp-iac


### 2. Configurer l'inventaire

Modifier `inventory.ini` avec les adresses IP de vos serveurs :
[staging_webservers]
staging-web1 ansible_host=<IP_SERVEUR>

### 3. Configurer les secrets

Éditer `group_vars/all/vault.yml` puis chiffrer :
ansible-vault encrypt group_vars/all/vault.yml

### 4. Déployer

Déployer tout
ansible-playbook site.yml --ask-vault-pass

Déployer staging uniquement
ansible-playbook site.yml --ask-vault-pass --limit staging

Déployer production uniquement
ansible-playbook site.yml --ask-vault-pass --limit production


## 🔐 Gestion des Secrets

Les secrets sont gérés via **Ansible Vault** :
Chiffrer le fichier
ansible-vault encrypt group_vars/all/vault.yml

Éditer le fichier chiffré
ansible-vault edit group_vars/all/vault.yml

Voir le contenu
ansible-vault view group_vars/all/vault.yml

## 🏷️ Tags Disponibles

| Tag | Description |
|-----|-------------|
| common | Configuration de base |
| database | MySQL uniquement |
| webserver | Nginx + PHP + App |
| staging | Environnement staging |
| production | Environnement production |

## 📊 Vérifications

Vérifier la syntaxe
ansible-playbook site.yml --syntax-check

Mode dry-run
ansible-playbook site.yml --check --ask-vault-pass

Tester la connectivité
ansible all -m ping

Commandes Importantes

# Créer la structure du projet
mkdir -p projet-kapsulekorp-iac/{group_vars/all,roles/{common,nginx,mysql,php,app}/{tasks,templates,handlers}}

# Initialiser Git
cd projet-kapsulekorp-iac
git init
git add .
git commit -m "Initial commit - Projet Ansible KapsuleKorp"

# Chiffrer le vault
ansible-vault encrypt group_vars/all/vault.yml

# Tester la connexion
ansible all -m ping -i inventory.ini

# Lancer le déploiement
ansible-playbook -i inventory.ini site.yml --ask-vault-pass

