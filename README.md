# Project Network Azoid

## Présentation

**Project Azoid** est un projet pédagogique de cybersécurité pour **Azuria Distribution**, une entreprise fictive de 42 employés.

L'objectif est de construire une infrastructure réseau virtuelle, segmentée et sécurisée, avec une protection contre les ransomwares.

## Technologies

- Oracle VirtualBox
- OPNsense 26.7
- Cisco Packet Tracer
- Windows Server 2022 (prévu)
- Debian Linux (prévu)
- Git et GitHub

## Travail réalisé

- Création des dossiers du projet : `Backups`, `BlueTeam_Evidence`, `Configs`, `Documentation`, `ISO` et `VMs`.
- Téléchargement des ISO nécessaires.
- Installation de la VM `AZOID-FW01` avec OPNsense.
- Configuration du WAN via VirtualBox NAT.
- Configuration des réseaux SERVERS, ADMIN et RH.
- Activation du DHCP sur ces trois réseaux.
- Conservation de HTTPS pour l'administration d'OPNsense.
- Création d'une première topologie Cisco Packet Tracer.
- Création du dépôt GitHub privé et du fichier `.gitignore`.

## Plan d'adressage

| Réseau | Interface | Adresse IP | État |
|---|---|---|---|
| WAN | em0 | 10.0.2.15/24 | Configuré |
| SERVERS | em1 | 10.10.20.1/24 | Configuré |
| ADMIN | em2 | 10.10.10.1/24 | Configuré |
| RH | em3 | 10.10.30.1/24 | Configuré |
| COMPTA | em4 | 10.10.40.1/24 | À faire |
| TECH | em5 | 10.10.50.1/24 | À faire |
| GUESTS | em6 | 10.10.60.1/24 | À faire |
| BACKUP | em7 | 10.10.70.1/24 | À faire |
| VPN | WireGuard | 10.10.80.0/24 | À faire |

### Plages DHCP configurées

- SERVERS : `10.10.20.100` à `10.10.20.199`
- ADMIN : `10.10.10.100` à `10.10.10.199`
- RH : `10.10.30.100` à `10.10.30.199`

> Les règles de pare-feu et l'isolation effective des réseaux restent à configurer et à tester.

## Prochaines étapes

1. Terminer les réseaux COMPTA, TECH, GUESTS et BACKUP.
2. Configurer les règles de sécurité OPNsense.
3. Installer Active Directory sur DC01.
4. Configurer le serveur de fichiers FS01.
5. Déployer Nextcloud et les applications Web.
6. Mettre en place les sauvegardes et tester une restauration.
7. Configurer le VPN WireGuard.
8. Documenter les tests et préparer la démonstration finale.

## Avancement

**Phase 1 : infrastructure réseau et pare-feu — en cours.**

Trois des sept réseaux internes physiques ont leur adressage configuré.
