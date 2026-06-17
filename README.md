# CyberSight Dashboard

**Cyber Threat Intelligence — Healthcare**

Tableau de bord de veille cyber (CTI) développé pour un groupe de cliniques privées en Occitanie. Il consolide en temps réel les informations de sécurité essentielles pour permettre aux équipes techniques et aux dirigeants de prendre des décisions éclairées face aux menaces cybernétiques visant le secteur de la santé.

Projet **OpenInnov 2025–2026** · M1 Cybersécurité

🔗 **Démo en ligne** : [ashrza1.github.io/oc-sante-cti](https://ashrza1.github.io/oc-sante-cti/)

## Présentation du projet

CyberSight est une application web **statique** (fichier HTML unique) hébergée sur GitHub Pages, accessible sans installation ni serveur applicatif. Elle a pour objectif de donner une vision tactique consolidée des menaces cyber ciblant le secteur santé, afin d'orienter les décisions de priorisation sécurité d'OC Santé.

## Contexte et enjeux

- **Contexte** : le secteur de la santé représente **67 %** des cibles des groupes RaaS (Ransomware-as-a-Service) en 2026.
- **Surface** : les cliniques OC Santé exposent ** des actifs numériques** accessibles depuis Internet.
- **Menaces** : des groupes comme **LockBit 3.0**, **RansomHub**, **Medusa** et **Lazarus Group** ciblent activement les établissements de santé français.
  
## Architecture technique

Le dashboard est conçu selon une architecture légère, sans dépendance serveur, permettant un déploiement immédiat et gratuit.

## Sources de données

- **CERT-FR** ([cert.ssi.gouv.fr](https://www.cert.ssi.gouv.fr/)) — flux RSS officiels des alertes, avis, rapports CTI, indicateurs de compromission (IOC), recommandations de durcissement (DUR) et bulletins d'actualité
- **ANS Cyberveille Santé** ([cyberveille.esante.gouv.fr](https://cyberveille.esante.gouv.fr/alertes-et-vulnerabilites)) — flux RSS spécialisé secteur santé (alertes et vulnérabilités)
- **NVD NIST** — base de données nationale des vulnérabilités (CVE) américaine
- **CNIL** — sanctions et actualités RGPD, en particulier sur les données de santé
- **Flux de veille générale** : BleepingComputer, Krebs on Security, The Hacker News, Healthcare IT News, HIPAA Journal, SecurityWeek, Dark Reading, Help Net Security, Graham Cluley, Cybersecurity Dive, EDPB

*Projet OpenInnov 2025–2026 · OC Santé CTI Dashboard*
