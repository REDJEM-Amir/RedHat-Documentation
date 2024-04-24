# Configuration serveur Red-Hat / CentOS

## Effacer l'ancienne empreinte digitale
> ssh-keygen -R ipserver

## Vérifier si le ping fonctionne avant ssh
> ping ipserver

## Connexion ssh vers le serveur
> ssh -lroot -p22 ipserver

> psswdserver

## Savoir qui est connecté sur le serveur 
> who

## Mises à jour système
### Mettez à jour la liste des paquets disponibles
> sudo yum update
### Mettez à jour les paquets installés
> sudo yum upgrade
### Pour mettre à jour le noyau et d'autres paquets
> sudo yum distro-sync
### Pour supprimer les paquets qui ne sont plus nécessaires
> sudo yum autoremove

## Ajouter un utilisateur
> sudo adduser nameuser

## Changez le nom d'utilisateur 
> sudo usermod -l newname oldname

## Modifier le mot de passe d'un utilisateur
> sudo passwd username

## Mise à jour du groupe 
> sudo groupmod -n newname oldname

## Changez le nom du répertoire home de l'utilisateur 
> sudo usermod -d /home/newname -m newname

## Ajouter l'utilisateur au groupe root
> sudo usermod -aG wheel username

## Vérifier le groupe de l'utilisateur
> groups username

## Changer le port de connexion SSH
### Ouvrez le fichier de configuration SSH
> sudo nano /etc/ssh/sshd_config
### Redémarrez le service SSH
> sudo systemctl restart sshd
### Vérifiez que le service SSH est actif
> sudo systemctl status sshd

## Désactivez le mot de passe du compte root
> sudo passwd -l root

## Désactiver la connexion root
### Ouvrez le fichier de configuration SSH 
> sudo nano /etc/ssh/sshd_config
### Recherchez la ligne PermitRootLogin
> PermitRootLogin no
### Redémarrez le service SSH
> sudo systemctl restart sshd

## Générer le certificat HTTPS

### Avec les sous domaine
> sudo certbot certonly --manual --preferred-challenges=dns-01 --server https://acme-v02.api.letsencrypt.org/directory -d "*.arecode.fr" -d arecode.fr

### Sans les sous domaine
> sudo certbot certonly --manual --preferred-challenges=dns-01 --server https://acme-v02.api.letsencrypt.org/directory -d arecode.fr
