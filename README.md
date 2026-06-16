# CyberSight Dashboard

**Cyber Threat Intelligence — Healthcare**

Tableau de bord de veille cyber (CTI) développé pour **OC Santé**, groupe de cliniques privées en Occitanie (Montpellier). Il consolide en temps réel les informations de sécurité essentielles pour permettre aux équipes techniques et aux dirigeants de prendre des décisions éclairées face aux menaces cybernétiques visant le secteur de la santé.

Projet **OpenInnov 2025–2026** · M1 Cybersécurité

🔗 **Démo en ligne** : [ashrza1.github.io/oc-sante-cti](https://ashrza1.github.io/oc-sante-cti/)

---

## Sommaire

- [Présentation du projet](#présentation-du-projet)
- [Contexte et enjeux](#contexte-et-enjeux)
- [Architecture technique](#architecture-technique)
- [Sources de données](#sources-de-données)
- [Fonctionnalités](#fonctionnalités)
- [Déploiement](#déploiement)
- [Recommandations d'évolution](#recommandations-dévolution)

---

## Présentation du projet

CyberSight est une application web **statique** (fichier HTML unique) hébergée sur GitHub Pages, accessible sans installation ni serveur applicatif. Elle a pour objectif de donner une vision tactique consolidée des menaces cyber ciblant le secteur santé, afin d'orienter les décisions de priorisation sécurité d'OC Santé.

## Contexte et enjeux

- **Contexte** : le secteur de la santé représente **67 %** des cibles des groupes RaaS (Ransomware-as-a-Service) en 2026.
- **Surface** : les cliniques OC Santé exposent **43 actifs numériques** (domaines et adresses IP) accessibles depuis Internet.
- **Menaces** : des groupes comme **LockBit 3.0**, **RansomHub**, **Medusa** et **Lazarus Group** ciblent activement les établissements de santé français.
- **Niveau** : le niveau de menace actuel sur OC Santé est évalué à **ÉLEVÉ**.

## Architecture technique

Le dashboard est conçu selon une architecture légère, sans dépendance serveur, permettant un déploiement immédiat et gratuit.

### Technologies utilisées

| Composant | Technologie | Rôle |
|---|---|---|
| Interface | HTML5 / CSS3 / JavaScript vanilla | Structure, style et logique du dashboard |
| Graphiques | Chart.js 4.4.1 (CDN) | Courbes de tendances, radars, camemberts |
| Flux RSS | Proxies CORS en cascade (rss2json, codetabs, corsproxy.io, allorigins, thingproxy) | Conversion RSS → JSON pour les flux institutionnels |
| Hébergement | GitHub Pages | Déploiement statique, gratuit, HTTPS |
| Export PDF | `window.print()` + CSS `@media print` | Export natif du navigateur, aucun serveur requis |
| Notifications | Web Notifications API | Alertes push navigateur en temps réel |
| Carte géo. | SVG inline + animations CSS | Cartographie des menaces géolocalisées |

### Gestion des flux RSS

Les flux RSS institutionnels ne peuvent pas être appelés directement depuis un navigateur (restriction CORS). Le dashboard interroge automatiquement **plusieurs proxies CORS en cascade** : si le premier échoue (quota dépassé, panne), le suivant est tenté automatiquement, jusqu'à 5 proxies différents par flux. Un filtre de fraîcheur à 6 mois élimine les articles obsolètes, et une validation d'URL filtre les liens malformés générés par certains flux. En cas d'échec de tous les proxies, des données de secours (mock) régulièrement actualisées sont affichées à la place, avec une mention explicite à l'utilisateur.

## Sources de données

- **CERT-FR** ([cert.ssi.gouv.fr](https://www.cert.ssi.gouv.fr/)) — flux RSS officiels des alertes, avis, rapports CTI, indicateurs de compromission (IOC), recommandations de durcissement (DUR) et bulletins d'actualité
- **ANS Cyberveille Santé** ([cyberveille.esante.gouv.fr](https://cyberveille.esante.gouv.fr/alertes-et-vulnerabilites)) — flux RSS spécialisé secteur santé (alertes et vulnérabilités)
- **NVD NIST** — base de données nationale des vulnérabilités (CVE) américaine
- **CNIL** — sanctions et actualités RGPD, en particulier sur les données de santé
- **Flux de veille générale** : BleepingComputer, Krebs on Security, The Hacker News, Healthcare IT News, HIPAA Journal, SecurityWeek, Dark Reading, Help Net Security, Graham Cluley, Cybersecurity Dive, EDPB

## Fonctionnalités

### À destination des dirigeants

- **Export PDF** — génération en un clic d'une capture complète du dashboard, sans logiciel supplémentaire, adaptée à une présentation COMEX ou un rapport mensuel
- **Indicateurs clés (KPIs)** — CVE critiques actives, niveau de menace global, groupes de menaces actifs, actifs surveillés, sources CTI actives
- **Résumé exécutif — Questions RSSI** — statut immédiat (à risque / sous contrôle) sur les questions stratégiques qu'un RSSI doit pouvoir répondre à tout moment
- **Alertes Push** — notifications navigateur en temps réel dès qu'une CVE critique (CVSS ≥ 9.0) ou une alerte CERT-FR critique est détectée
- **Graphique de tendances** — évolution des CVE publiées, alertes santé et incidents secteur sur les jours récents, avec seuil d'alerte visuel
- **Cartographie géographique** — visualisation animée des flux d'attaques par origine géographique (Russie, Corée du Nord, Chine, Iran) vers OC Santé

### Techniques avancées

- **Veille CTI institutionnelle** — panneau ANS Cyberveille Santé en temps réel, avec données de secours en cas d'indisponibilité du flux
- **Table de CVE critiques** — identifiant cliquable vers la fiche NVD, score CVSS, statut d'exploitation active, actifs OC Santé concernés
- **Gestion des correctifs (Patch Management)** — calendrier de priorisation des mises à jour de sécurité
- **Surveillance OSINT** — veille en sources ouvertes sur les mentions, fuites ou expositions potentielles d'OC Santé
- **Acteurs de menaces** — fiches expansibles des groupes cybercriminels actifs (TTPs MITRE ATT&CK, IOC, liens vers rapports ANSSI/CISA/FBI)
- **Surface d'attaque surveillée** — recensement des 43 actifs numériques exposés (masqué dans la démo pour confidentialité)
- **Diagnostic des flux RSS** — tableau de bord interne indiquant pour chaque flux quel proxy a réussi ou échoué, pour faciliter le suivi technique

## Déploiement

Le dashboard est hébergé sur **GitHub Pages** : [ashrza1.github.io/oc-sante-cti](https://ashrza1.github.io/oc-sante-cti/). Toute modification du fichier `index.html` poussée sur la branche principale est automatiquement republiée en ligne.

Les données en temps réel (flux CERT-FR, ANS, etc.) sont récupérées à chaque chargement de la page. Les données structurelles (liste des CVE, acteurs de menaces, actifs surveillés) sont mises à jour manuellement dans le fichier source lors de chaque revue de sécurité.

### Mettre à jour le site

1. Modifier `index.html` localement ou directement dans l'éditeur GitHub
2. Committer les changements sur la branche `main`
3. GitHub Pages republie automatiquement le site (généralement en moins d'une minute)

## Recommandations d'évolution

- Intégrer une API NVD officielle pour récupérer automatiquement les CVE en temps réel
- Connecter un SIEM pour alimenter les KPIs depuis des données réelles
- Ajouter une authentification (OAuth) pour restreindre l'accès au dashboard
- Mettre en place des alertes e-mail automatiques pour les CVE critiques
- Développer une version mobile optimisée pour les dirigeants en déplacement

---

*Projet OpenInnov 2025–2026 · OC Santé CTI Dashboard*
