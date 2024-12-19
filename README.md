# Mini-HomeLab

Déployer votre mini-homelab avec Ansible en quelques secondes !
Le déploiement inclus actuellement :
- Portainer (Container management)
- qBittorrent (Téléchargement de torrents)
- Jellyfin (Serveur Médias)

Le projet peut fonctionner sur un Raspberry Pi, sur une VM, ou même en local.
Le projet est compatible amd64 et arm64

![Alt homelab](https://ibb.co/YhZRN70 "homelab")

## Requirements

- Un serveur avec Ubuntu server 24.04 installé (https://ubuntu.com/download/server). 
- Un accès SSH à ce serveur.
- Ansible installé sur votre machine local (ou devcontainer) pour le déploiement automatique.

## Préparation

- Clonez ce repos sur votre machine local

```
git clone git@github.com:Anadris/mini-homelab.git
cd mini-homelab
```
#### Hosts

Editez le fichier `hosts.yml` en renseignant les informations suivantes :
- adresse ip de votre machine serveur
- utilisateur de connection (avec droits sudo)
- l'emplacement de votre clé SSH sur votre machine locale.

#### qBittorrent

> Vous pouvez ignorer cette étape si vous souhaitez utiliser le mot de passe par defaut (non recommandé) \
*login : admin* \
*password : adminadmin*

qBittorrent génère normalement un mot de passe aléatoire pour acceder à l'interface Web, qu'il faut récupérer dans les logs du container.
Ce déploiement avec Ansible contourne cette étape en vous permettant de générer votre propre password hashé et de l'intégrer à la configuration de l'application. \
Commencez par créer le hash de votre password en utilisant le script python dans `/utils/qbittorrent/qbittorrent_hash.py`

```
python3 ./utils/qbittorrent/qbittorrent_hash.py
```
Le script vous demande d'entrer votre password, lorsque vous valider il vous affichera votre hash précédé de 'WebUI\Password_PBKDF2=' \
Copiez cette ligne complète et collez là dans le fichier de variables de qBittorrent qui se situe ici : `ansible/playbooks/roles/qbittorrent/vars/main.yml`

## Lancement

Initiez le lancement du déploiement avec la commande :

```
cd ansible
ansible-playbook playbooks/playbook.yml
```

Si tout s'est bien déroulé, vous devriez pouvoir accéder à vos différentes applications

Portainer : `http://votre-ip-du-serveur:9000` \
qBittorrent : `http://votre-ip-du-serveur:8082` \
Jellyfin : `http://votre-ip-du-serveur:8096` \

Vous pouvez également vérifier le fonctionnement de docker directement sur votre machine serveur :

```
ssh votreUser@votreIpServeur
docker ps
```
