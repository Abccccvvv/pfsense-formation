markdown
# pfSense Formation

![CI](https://pfst.cf2.poecdn.net/base/image/c30913320507afef1b087f6f14f08ce41faccb659260e0ed708750fa53e6c344?pmaid=579674275) ![Licence](https://pfst.cf2.poecdn.net/base/image/4afe82b6f9e727dd5f995c86765b5458003301d7e024c3838581959b37982d63?pmaid=579674274) ![Security](https://pfst.cf2.poecdn.net/base/image/1703819205cd8780a28d2b92994f626abad578cbd2a954e58d718b820cc80b8d?pmaid=579674273)

Version : 1.0.0  
Licence : GPL‑3.0

Résumé
-------
Ce dépôt fournit un cursus de formation professionnel autour de pfSense (pare‑feu et routeur open source). Il inclut :
- guides d'installation et d'administration,
- scripts d'automatisation et artefacts reproductibles,
- laboratoires pratiques et topologies pédagogiques,
- pipelines CI pour validation automatique,
- documents de conformité et recommandations de durcissement.

Le cours s'appuie sur des bonnes pratiques inspirées par NIST SP 800‑53, CIS Benchmarks et ISO/IEC 27001 pour assurer sécurité, traçabilité et qualité.

Public cible
------------
- Administrateurs réseaux débutants à intermédiaires.
- Techniciens système devant déployer/maintenir pfSense en production.
- Étudiants en cybersécurité et opérations réseau.

Durée et format
---------------
- Durée recommandée : 16 heures (4 sessions de 4h) — adaptable.
- Format : présentiel ou distanciel (avec laboratoires en VM).
- Niveau requis : notions de réseau (IP, routage, NAT), bases Linux/UNIX utiles.

Badges recommandés
------------------
- CI: ![CI](https://pfst.cf2.poecdn.net/base/image/c30913320507afef1b087f6f14f08ce41faccb659260e0ed708750fa53e6c344?pmaid=579674275) (intégration continue)
- Licence: ![GPL-3.0](https://pfst.cf2.poecdn.net/base/image/4afe82b6f9e727dd5f995c86765b5458003301d7e024c3838581959b37982d63?pmaid=579674274)
- Security: ![SCA](https://pfst.cf2.poecdn.net/base/image/1703819205cd8780a28d2b92994f626abad578cbd2a954e58d718b820cc80b8d?pmaid=579674273)

Table des matières
------------------
- Objectifs
- Plan (modules)
- Matériel et prérequis
- Installation rapide
- Guides détaillés (extraits)
- Laboratoires pratiques (TP)
- Tests & CI
- Sécurité et conformité
- Modèles et artefacts fournis
- Contribution
- Support & contact
- Références

Objectifs pédagogiques
----------------------
À la fin de la formation, les participants seront capables de :
- Installer pfSense (VM ou bare‑metal) et réaliser une configuration initiale sécurisée.
- Mettre en place NAT, NAT64/IPv6 basique, VLANs, et routage statique.
- Configurer VPN site‑à‑site (IPsec) et VPN client (OpenVPN / WireGuard si disponible).
- Appliquer des règles de firewall granulaires, gérer les règles de NAT et les politiques de QoS de base.
- Surveiller, journaliser et intégrer pfSense à une solution de SIEM/centralisation (rsyslog/Graylog/ELK).
- Automatiser des déploiements reproductibles et gérer les configurations via scripts.
- Appliquer des mesures de durcissement conformes aux bonnes pratiques (CIS / NIST).

Plan détaillé (modules)
-----------------------
1. Introduction & concepts (1h)
   - Présentation pfSense / architecture / cas d'usage.
2. Installation & démarrage (2h)
   - Préparation d'une VM, options d'installation (ISO, USB).
   - Installation guidée et configuration initiale.
3. Interfaces, VLANs et routage (2h)
   - Configuration des interfaces, VLAN tagging, routage interne.
4. Firewall, NAT et règles (3h)
   - Écriture et optimisation des règles, gestion des états, port forwarding.
5. VPNs (3h)
   - IPsec site‑à‑site, OpenVPN serveurs/clients, bonnes pratiques d'authentification.
6. Haute disponibilité et sauvegarde (1h)
   - CARP, synchronisation de configuration, backups chiffrés.
7. Monitoring & logs (1h)
   - Intégration Prometheus/Grafana, centralisation des logs.
8. Durcissement & conformité (1h)
   - Checklist CIS/NIST, rotation de clés, gestion des correctifs.
9. Atelier pratique / examen (2h)
   - TP noté : déployer une topologie complète et vérifier conformité.

Matériel et prérequis
---------------------
- Machine hôte : 8+ Go RAM, 2+ vCPU recommandés pour VM de labo.
- Virtualisation : VirtualBox, VMware Workstation/ESXi, KVM/QEMU.
- ISO pfSense : cf. "Installation rapide" ci‑dessous.
- Accès Internet recommandé pour téléchargement de paquets et mises à jour.
- Compte GitHub pour récupérer les artefacts et contribuer.

Installation rapide
-------------------
1) Télécharger l'installateur pfSense officiel  
   - Netgate Installer / pfSense ISO : https://shop.netgate.com/products/netgate-installer
     (Sélectionner l'image adaptée : AMD64 Memstick, AMD64 ISO pour VM/IPMI, ou AARCH64 pour appareils ARM.)
   - Vérifier l'intégrité du fichier avec SHA256 (page "pfSense Plus Installer Checksums").

2) Exemple : déployer en VM (script fourni)
```bash
# placer l'ISO dans ./isos/
./scripts/deploy-vm.sh --name pfsense-lab --iso ./isos/pfSense-CE-2.6.0-amd64.iso --ram 2048 --cpu 2

Importer une configuration de départ (exemple)
bash
# depuis la racine du repo
scp configs/base/config.xml admin@pfsense-lab:/cf/conf/config.xml
# ou via l'interface web : Diagnostics > Backup & Restore

Guides & extraits (sélection)
Guide d'installation complet : docs/install.md
Guide de migration vers pfSense Plus : docs/migration.md
Durcissement et checklist CIS/NIST : docs/hardening.md
VPN / IPsec pas à pas : docs/vpn_ipsec.md
Monitoring (Prometheus + Grafana) : docs/monitoring.md
Laboratoires pratiques (TP)
Chaque TP contient : objectifs, topologie, étapes, fichier de configuration solution, et critères d'évaluation.

Exemples :

TP1 — Installation et configuration initiale
Topologie : 1 WAN, 2 LAN (VLANs)
Livrables : capture d'écran de l'interface web, export config.xml
TP2 — VPN site‑à‑site
Topologie : 2 appliances pfSense (site A / site B)
Livrables : tunnel UP (phase 1/2), preuve de passage ICMP inter-sites
TP3 — Durcissement et audit
Exécuter checklist, corriger 5 risques majeurs, rapport final
Tests & Intégration Continue (CI)
Le dépôt inclut une pipeline CI (exemples : GitHub Actions) pour valider :

Linting : shellcheck pour scripts, yamllint pour fichiers YAML.
Validation : jq pour JSON, yamllint pour YAML.
Scans de sécurité : trivy (images), snyk (dépendances) — générer artefacts et rapports.
Tests d'intégration basiques : scripts qui démarrent une VM minimale et vérifient l'accès web/admin.
Publication d'artefacts : exports de configuration, rapports de scan, logs (artefacts CI).
Exemple (GitHub Actions) : .github/workflows/ci.yml

jobs:
lint
security-scan
unit-tests
integration-tests (optionnel, runner auto‑hébergé recommandé pour VM)
Sécurité et conformité
Principales recommandations de sécurité :

Authentification : activer 2FA pour les comptes admin si possible.
Accès web : restreindre l'interface d'administration par IP allowlist et ACLs.
Chiffrement : forcer TLS (certificat valide) pour l'administration Web et VPN.
Sauvegardes : sauvegardes régulières chiffrées (GPG) et stockage hors site.
Patching : appliquer les MAJ régulièrement ; tester les mises à jour en labo avant prod.
Journalisation : envoyer logs vers un serveur centralisé et conserver selon la politique.
Rotation : rotation de clés / mots de passe (ex. 90 jours), gérer via Vault si possible.
Conformité :
Cartographie des contrôles NIST/CIS correspondants fournie dans docs/compliance.md
Modèle de preuve d'audit et checklist sont fournis.
Modèles et artefacts fournis
configs/ : configurations exemples (base, vpn, ha)
scripts/ : scripts d'automatisation (deploy, backup, restore, checks)
docs/ : guides, checklists, syllabus
.github/workflows/ : pipelines d'intégration continue
lab/topologies/ : diagrammes et fichiers de topologie (textuels)
Contribution
Nous accueillons contributions, issues et PRs. Merci de suivre ces règles :

Fork -> Branch feature/bugfix -> Commit descriptif -> PR.
Respecter la convention de commit (ex. Conventional Commits).
Ouvrir une issue avant les changements majeurs (design / architecture).
Tests : ajouter/mettre à jour tests pour tout changement logique.
Signer le CLA si demandé [optionnel].
Modèle de PR

Titre clair
Description (résumé, motivation, impact)
Checklist : tests passés, lint OK, documentation à jour
Support & contact
Pour questions et support :

Mainteneur : [ton-nom] — [votre-email@example.com]
Issues : ouvre une issue sur GitHub.
Pour formations payantes / accompagnement : contact@exemple.com
Licence
Ce projet est sous licence GPL‑3.0 — voir fichier LICENSE.

Annexes & Références
Netgate / pfSense installer : https://shop.netgate.com/products/netgate-installer
pfSense Documentation officielle : https://docs.netgate.com/pfsense/
CIS Benchmarks pour pfSense / FreeBSD (guides généraux)
NIST SP 800‑53 : https://csrc.nist.gov
ISO/IEC 27001 : https://www.iso.org
Remarques finales
Adapte les scripts et exercices à ton environnement. Si tu veux, je peux :

Générer un template de script deploy-vm.sh personnalisé pour VirtualBox/VMware/KVM.
Rédiger les fichiers docs/install.md et docs/hardening.md en détail.
Préparer un workflow GitHub Actions complet pour CI (avec exemples).

Souhaites-tu que je rédige automatiquement les fichiers suivants pour ton dépôt maintenant ?
- docs/install.md complet
- scripts/deploy-vm.sh (VirtualBox et VMware)
- .github/workflows/ci.yml (exemple avec lint, security scan, tests)

Si oui, indique lesquels et tes préférences (système de virtualisation, version pfSense ciblée, exigences CI).

