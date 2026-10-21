# Project-Network-Azoid

## Présentation

**Project Azoid** est un projet de cybersécurité visant à concevoir et sécuriser l'infrastructure réseau virtuelle d'une entreprise fictive, **Azuria Distribution**, composée de 42 employés.

L'objectif est de mettre en place une infrastructure segmentée, administrée et résiliente face aux cyberattaques, notamment aux ransomwares.

Le projet est réalisé dans **Oracle VirtualBox**, avec **OPNsense** comme pare-feu principal.

## Technologies utilisées

- Oracle VirtualBox
- OPNsense 26.7
- Debian 13
- Windows Server 2022 (prévu)
- Windows 11 Education (prévu)
- Cisco Packet Tracer
- Git et GitHub
- Visual Studio Code

## Architecture réseau

Le pare-feu `AZOID-FW01` possède une interface WAN et sept interfaces internes.

| Interface | Réseau | Adresse de passerelle | Fonction |
|---|---|---|---|
| WAN | Internet (NAT VirtualBox) | DHCP | Accès Internet |
| SERVERS | 10.10.20.0/24 | 10.10.20.1 | Serveurs internes |
| ADMIN | 10.10.10.0/24 | 10.10.10.1 | Administration informatique |
| RH | 10.10.30.0/24 | 10.10.30.1 | Ressources humaines |
| COMPTA | 10.10.40.0/24 | 10.10.40.1 | Comptabilité |
| TECH | 10.10.50.0/24 | 10.10.50.1 | Service technique |
| GUESTS | 10.10.60.0/24 | 10.10.60.1 | Appareils invités |
| BACKUP | 10.10.70.0/24 | 10.10.70.1 | Infrastructure de sauvegarde |

**Remarque :** les adresses de TECH, GUESTS et BACKUP sont planifiées mais pas encore configurées.

Les interfaces ont été nommées dans OPNsense. La configuration complète des règles d'isolation reste à réaliser.

## Machines virtuelles

### AZOID-FW01

- Système : OPNsense 26.7
- Rôle : pare-feu, routage, segmentation réseau et DHCP
- WAN : NAT VirtualBox
- Réseaux internes : SERVERS, ADMIN, RH, COMPTA, TECH, GUESTS et BACKUP
- Interface d'administration HTTPS accessible depuis le réseau SERVERS

### TEST01

- Système : Debian 13
- Compte utilisateur : `azoid-admin`
- Environnement graphique : XFCE
- Navigateur : Firefox
- Connexion réseau actuelle : `AZOID-SERVERS`
- Adresse IPv4 obtenue par DHCP lors des tests : `10.10.20.135/24`
- Passerelle : `10.10.20.1`

TEST01 sert à vérifier la connectivité, les services réseau et les règles du pare-feu.

## Travaux réalisés

### 1. Préparation de l'environnement

- Création de la structure du projet.
- Téléchargement des images ISO nécessaires.
- Installation et configuration de VirtualBox.
- Création d'un dépôt GitHub privé.
- Ajout de la documentation et du fichier Cisco Packet Tracer au dépôt.

### 2. Installation d'OPNsense

- Création de la VM `AZOID-FW01`.
- Installation d'OPNsense.
- Configuration de l'interface WAN avec DHCP.
- Attribution des interfaces réseau internes.
- Configuration des adresses IPv4 de SERVERS, ADMIN, RH et COMPTA.
- Configuration du DHCP sur les premiers réseaux internes.
- Activation de l'administration HTTPS.
- Renommage des interfaces dans l'interface web.

### 3. Installation de TEST01

- Création de la VM Debian 13.
- Installation du système d'exploitation.
- Installation du serveur SSH.
- Installation de XFCE et Firefox.
- Connexion réussie à l'environnement graphique.
- Accès à l'interface web OPNsense depuis Firefox.

### 4. Tests réseau réussis

| Test | Résultat |
|---|---|
| Attribution DHCP à TEST01 | Réussi |
| Ping vers `10.10.20.1` | Réussi |
| Ping vers `1.1.1.1` | Réussi |
| Résolution DNS de `debian.org` | Réussi |
| Vérification de la route par défaut | Réussi |
| Connexion HTTPS à OPNsense | Réussi |
| Accès au tableau de bord OPNsense | Réussi |

Ces tests confirment que TEST01 peut communiquer avec le pare-feu et accéder à Internet depuis le réseau SERVERS.

### 5. Première règle de pare-feu ADMIN

Une règle a été créée et appliquée sur l'interface ADMIN :

| Paramètre | Valeur |
|---|---|
| Action | Pass |
| Direction | In |
| Version | IPv4 |
| Protocole | TCP |
| Source | ADMIN network |
| Destination | ADMIN address |
| Port de destination | HTTPS (443) |

Cette règle autorise les machines du réseau ADMIN à accéder à l'interface d'administration HTTPS d'OPNsense.

**La règle est appliquée, mais son fonctionnement depuis une machine connectée à ADMIN reste à tester.**

## État actuel

- OPNsense fonctionne et son tableau de bord est accessible.
- TEST01 fonctionne avec Debian 13 et XFCE.
- Les tests réseau depuis SERVERS sont réussis.
- Les interfaces réseau ont été renommées.
- La première règle de gestion HTTPS depuis ADMIN est appliquée.
- TEST01 est actuellement éteinte.

## Prochaine étape

La prochaine session commencera par le test du réseau ADMIN :

1. Modifier l'adaptateur réseau VirtualBox de TEST01 de `AZOID-SERVERS` vers `AZOID-ADMIN`.
2. Démarrer TEST01.
3. Vérifier son adresse IP.
4. Tester la connectivité vers `10.10.10.1`.
5. Ouvrir `https://10.10.10.1` dans Firefox.
6. Vérifier que la règle HTTPS ADMIN fonctionne.

## Fonctionnalités restant à réaliser

- Finaliser la configuration des interfaces et du DHCP.
- Définir les règles de filtrage et d'isolation entre les réseaux.
- Installer Windows Server 2022 et Active Directory.
- Configurer les utilisateurs, groupes et politiques de sécurité.
- Mettre en place le serveur de fichiers et les permissions.
- Installer Nextcloud et les services web HTTPS.
- Configurer les sauvegardes automatisées, chiffrées et isolées.
- Mettre en place le VPN WireGuard.
- Effectuer les tests de sécurité et de restauration.
- Compléter les schémas, procédures et preuves techniques.

## Organisation du dépôt

```text
Project-Network-Azoid/
├── Backups/
├── BlueTeam_Evidence/
├── Configs/
├── Documentation/
│   └── Reseau-projet-Azoid.pkt
├── ISO/
├── VMs/
├── .gitignore
└── README.md
```

Les fichiers volumineux des machines virtuelles, les images ISO, les sauvegardes sensibles et les secrets ne doivent pas être publiés dans Git.

---

**Projet :** Project Azoid  
**Environnement :** VirtualBox / OPNsense / Debian  
**Dernière mise à jour :** 21 octobre 2026  
**Statut :** Infrastructure réseau en cours de configuration et de validation
