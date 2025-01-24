# Mini-HomeLab

Déployer votre mini-homelab avec Ansible en quelques secondes !
Le déploiement inclus actuellement :
- Jellyfin (Serveur Médias)
- Netdata (Supervision du serveur)
- VaultWarden (Gestionnaire de mot de passe)
- Nginx (Reverse Proxy)

Le projet peut fonctionner sur un Raspberry Pi, sur une VM, ou même en local.
Le projet est compatible amd64 et arm64

![Alt homelab](https://miro.medium.com/v2/resize:fit:1024/1*ltEkf2pvdnCa9c3VnvjIog.jpeg "homelab")

## Requirements

- Un serveur avec Ubuntu server 24.04 installé (https://ubuntu.com/download/server). 
- Un accès SSH à ce serveur.
- Ansible installé sur votre machine local (ou devcontainer) pour le déploiement automatique.

## Préparation

- Clonez ce repos sur votre machine local

```
git clone git@github.com:jonathanCarra/mini-homelab.git
cd mini-homelab
```
#### Hosts

Editez le fichier `hosts.yml` en renseignant les informations suivantes :
- adresse ip de votre machine serveur
- utilisateur de connection (avec droits sudo)
- l'emplacement de votre clé SSH sur votre machine locale.

## Lancement

Initiez le lancement du déploiement avec la commande :

```
cd ansible
ansible-playbook playbooks/playbook.yml
```

Si tout s'est bien déroulé, vous devriez pouvoir accéder à vos différentes applications

Jellyfin    : `http://votre-ip-du-serveur/` \
Netdata     : `http://votre-ip-du-serveur/netdata/` \
VaultWarden : `https://votre-ip-du-serveur/vault/`

> [!TIP]
> Nginx vous redirigera automatiquement entre http et https en fonction de l'application que vous ciblez.

## Debug

Vous pouvez vous connecter sur votre machine serveur via ssh :

```
ssh votreUser@votreIpServeur
```

Vous pouvez également vérifier le fonctionnement de docker directement sur votre machine serveur :

```
docker ps
```

Pour voir les logs des containers docker :
```
docker compose logs
```

Enfin, il est possible de voir les différents ports ouvert via la commande :
```
netstat -ntlp
```

> [!NOTE]  
> En cas de bon fonctionnement des containers, les ports `80`, `443`, `8080`, `8920` et `19999` devraient être ouvert.

> [!WARNING]  
> Si les ports sont utilisé, mais que les containers ne sont pas actif, vous pouvez forcer la fermeture d'un port via la commande `sudo kill $(sudo lsof -t -i:<PORT>)`