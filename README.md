# Guide de Configuration pour Serveurs Red-Hat / CentOS

## Effacer une Empreinte Digitale SSH
Avant de se connecter, nettoyez l'ancienne empreinte digitale SSH associée au serveur.

```bash
ssh-keygen -R ipserveur
```

## Vérification de la Connectivité
Assurez-vous que le serveur est accessible via ping avant de démarrer une session SSH.

```bash
ping ipserveur
```

## Connexion SSH
Connectez-vous au serveur via SSH en utilisant le compte root et le mot de passe associé.

```bash
ssh -l root -p 22 ipserveur
```

## Vérification des Utilisateurs Connectés
Vérifiez les utilisateurs actuellement connectés au serveur.

```bash
who
```

## Mises à Jour du Système

| Action                                  | Commande                  |
|-----------------------------------------|---------------------------|
| Mettre à Jour la Liste des Paquets      | `sudo yum update`         |
| Mettre à Jour les Paquets Installés     | `sudo yum upgrade`        |
| Mettre à Jour le Noyau et Autres Paquets| `sudo yum distro-sync`    |
| Supprimer les Paquets Obsolètes         | `sudo yum autoremove`     |

## Gestion des Utilisateurs

| Action                                  | Commande                                          |
|-----------------------------------------|---------------------------------------------------|
| Ajout d'un Utilisateur                  | `sudo adduser nomutilisateur`                     |
| Changement du Nom d'Utilisateur         | `sudo usermod -l nouveaunom ancienom`            |
| Modification du Mot de Passe            | `sudo passwd nomutilisateur`                      |
| Mise à Jour du Groupe                   | `sudo groupmod -n nouveaunom ancienom`           |
| Changement du Répertoire Home            | `sudo usermod -d /home/nouveaunom -m nouveaunom` |
| Ajout d'un Utilisateur au Groupe Root   | `sudo usermod -aG wheel nomutilisateur`          |
| Vérification du Groupe de l'Utilisateur | `groups nomutilisateur`                           |

## Configuration SSH

| Action                                     | Commande                                        |
|--------------------------------------------|-------------------------------------------------|
| Changement de Port SSH                     | 1. Ouvrez le fichier de configuration SSH.<br>`sudo nano /etc/ssh/sshd_config` <br><br> 2. Redémarrez le service SSH.<br>`sudo systemctl restart sshd` <br><br> 3. Vérifiez que le service SSH est actif.<br>`sudo systemctl status sshd` |
| Désactivation de l'Accès Root via SSH     | 1. Ouvrez le fichier de configuration SSH.<br>`sudo nano /etc/ssh/sshd_config` <br><br> 2. Recherchez la ligne `PermitRootLogin` et modifiez-la comme suit :<br>`PermitRootLogin no` <br><br> 3. Redémarrez le service SSH.<br>`sudo systemctl restart sshd` |

## Génération de Certificat HTTPS

| Avec Sous-Domaines                        | Sans Sous-Domaines                              |
|-------------------------------------------|-------------------------------------------------|
| `sudo certbot certonly --manual --preferred-challenges=dns-01 --server https://acme-v02.api.letsencrypt.org/directory -d "*.arecode.fr" -d arecode.fr` | `sudo certbot certonly --manual --preferred-challenges=dns-01 --server https://acme-v02.api.letsencrypt.org/directory -d arecode.fr` |
