# Mini-HomeLab

### Requirements

Pour démarrer votre projet il vous faut quelques éléments de base

- Une VM avec Ubuntu server 24.04 installé (https://ubuntu.com/download/server)
- Un accès SSH à cette VM
- Ansible installé sur votre machine local

### Préparation

- Clonez ce repos sur votre machine local

```
git clone git@github.com:Anadris/mini-homelab.git
cd mini-homelab
```

Editez le fichier `hosts.yml` en renseignant les informations suivantes :
- adresse ip de votre machine serveur
- utilisateur de connection (avec droits sudo)
- l'emplacement de votre clé SSH sur votre machine locale.

### Lancement

Initiez le lancement du déploiement avec la commande :

```
cd ansible
ansible-playbook playbooks/playbook.yml
```

Si tout s'est bien déroulé, vous devriez pouvoir accéder à Portainer sur votre serveur :

`http://votre-ip-du-serveur:9000`

Vous pouvez également vérifier le fonctionnement de docker directement sur votre machine serveur :

```
ssh votreUser@votreIpServeur
docker ps
```