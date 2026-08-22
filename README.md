# 🚀 Réseau Universitaire — Cisco Packet Tracer

## 📌 Présentation

Ce projet consiste à concevoir et simuler une **infrastructure réseau universitaire structurée** avec **Cisco Packet Tracer**.

L'objectif est de remplacer une architecture réseau initialement **plate et non segmentée** par une infrastructure organisée autour de plusieurs départements, avec un **plan d'adressage IP structuré**, un **routage dynamique RIP** et une **salle serveurs centralisée** fournissant les services DNS, Web et FTP.

Le projet met en pratique les principaux concepts de **réseaux informatiques, routage IP, services réseau et interconnexion WAN**.

---

## 🎯 Objectifs du projet

* Concevoir une architecture réseau universitaire structurée
* Séparer les différents départements en sous-réseaux IP
* Mettre en place un routage dynamique avec **RIP**
* Interconnecter plusieurs routeurs via des liaisons WAN
* Centraliser les services réseau dans une salle serveurs
* Déployer les services **DNS, HTTP et FTP**
* Tester la connectivité entre les différents réseaux
* Vérifier le fonctionnement des services applicatifs
* Identifier les limites de l'architecture et proposer des améliorations

---

## 🏗️ Architecture réseau

L'infrastructure comprend :

* **3 routeurs**
* **6 commutateurs**
* **3 serveurs**

  * DNS
  * Web / HTTP
  * FTP
* Environ **20 PC**
* Plusieurs imprimantes
* **1 ordinateur portable**
* **2 liaisons WAN série**
* Plusieurs réseaux LAN départementaux

Les trois routeurs sont interconnectés et utilisent **RIP** pour échanger dynamiquement les informations de routage.

### 🔹 Schéma logique

```text
                    ┌─────────────────┐
                    │    Router0      │
                    │  Département IT│
                    └────────┬────────┘
                             │
                       WAN 10.10.0.0
                             │
                    ┌────────▼────────┐
                    │    Router1      │
                    │   Routeur Core  │
                    └────────┬────────┘
                             │
                       WAN 20.20.0.0
                             │
                    ┌────────▼────────┐
                    │    Router2      │
                    │ Serveurs / Labo │
                    └─────────────────┘
```

---

## 🌐 Plan d'adressage IP

| Département / Service    | Réseau           | Passerelle    |
| ------------------------ | ---------------- | ------------- |
| Département IT           | `192.168.1.0/24` | `192.168.1.1` |
| Département Informatique | `192.168.2.0/24` | `192.168.2.1` |
| Administration           | `192.168.3.0/24` | `192.168.3.1` |
| Bureau du directeur      | `192.168.4.0/24` | `192.168.4.1` |
| Salle des serveurs       | `1.0.0.0/24`     | `1.0.0.1`     |
| Laboratoire Internet     | `128.168.0.0/24` | `128.168.0.1` |

Les adresses et équipements terminaux sont organisés par département afin de faciliter l'identification et l'administration du réseau.

---

## 🔄 Routage dynamique — RIP

Le protocole **RIP (Routing Information Protocol)** est utilisé pour permettre aux trois routeurs d'échanger automatiquement leurs routes.

### Liaisons WAN

| Liaison           | Réseau      |
| ----------------- | ----------- |
| Router0 ↔ Router1 | `10.10.0.0` |
| Router1 ↔ Router2 | `20.20.0.0` |

RIP permet aux réseaux qui ne sont pas directement connectés à un routeur d'être appris automatiquement via les routeurs voisins.

### Vérification

```bash
show ip route
```

Les routes apprises dynamiquement apparaissent avec le code :

```text
R
```

Exemple :

```text
R 192.168.2.0/24 [120/1] via 10.10.0.2
```

---

## 🖥️ Services réseau

Une salle serveurs centralisée regroupe trois services principaux.

### DNS

**Adresse IP :**

```text
1.0.0.2
```

Le serveur DNS assure la résolution des noms internes.

Exemple :

```text
www.universite.local
        ↓
    1.0.0.3
```

Test :

```bash
ping www.universite.local
```

La documentation du projet indique que la résolution DNS a été vérifiée avec succès.

---

### 🌐 Serveur Web

**Adresse IP :**

```text
1.0.0.3
```

Service :

```text
HTTP
```

Test depuis un PC :

```text
http://1.0.0.3
```

La page Web est accessible depuis les postes clients.

---

### 📁 Serveur FTP

**Adresse IP :**

```text
1.0.0.4
```

Service :

```text
FTP
```

Le serveur FTP utilise une authentification par nom d'utilisateur et mot de passe.

Exemple de test :

```bash
ftp 1.0.0.4
```

Le test de connexion FTP a été réalisé avec succès depuis un poste du département IT.

---

## 🧪 Tests et validation

Plusieurs tests ont été réalisés afin de vérifier le fonctionnement de l'infrastructure.

### Test 1 — Connectivité IP

```bash
ping <adresse-ip>
```

Permet de vérifier la communication entre les différents réseaux.

### Test 2 — Routage

```bash
show ip route
```

Permet de vérifier les routes directement connectées et les routes apprises par RIP.

### Test 3 — DNS

```bash
ping www.universite.local
```

Permet de vérifier la résolution du nom DNS.

### Test 4 — HTTP

Depuis un PC :

```text
http://1.0.0.3
```

Permet de vérifier l'accès au serveur Web.

### Test 5 — FTP

```bash
ftp 1.0.0.4
```

Permet de vérifier l'accès au serveur FTP avec authentification.

Les tests Web et FTP sont documentés comme réussis dans le projet.

---

## 🔐 Sécurité

La version actuelle du projet met principalement en œuvre une **segmentation par sous-réseaux IP** et une authentification sur le service FTP.

Les mécanismes de sécurité avancés suivants ne sont pas encore implémentés :

* ACL
* SSH
* Port Security
* Pare-feu
* VLAN de gestion
* DHCP Snooping
* Dynamic ARP Inspection
* SNMP / Syslog

Ils sont proposés comme évolutions futures.

---

## 📈 Évolutions futures

Plusieurs améliorations peuvent être apportées au projet :

### 🔹 Sécurité

* Mise en place d'**ACL**
* Administration distante avec **SSH**
* **Port Security**
* VLAN de gestion
* Déploiement d'un pare-feu
* DHCP Snooping
* Dynamic ARP Inspection

### 🔹 Routage

Une migration de **RIP vers OSPF** pourrait être envisagée pour une architecture plus importante, notamment grâce à une convergence plus rapide et une meilleure évolutivité.

### 🔹 Haute disponibilité

* Liens WAN redondants
* HSRP / VRRP
* Redondance des serveurs
* Sauvegardes planifiées
* Rapid PVST+

### 🔹 Supervision

* SNMPv3
* Syslog
* NTP
* Supervision centralisée

### 🔹 Connectivité Internet

* Ajout d'une connexion Internet
* Route par défaut
* NAT
* Pare-feu en périphérie


## 🛠️ Technologies utilisées

| Technologie         | Utilisation                 |
| ------------------- | --------------------------- |
| Cisco Packet Tracer | Simulation réseau           |
| IPv4                | Adressage réseau            |
| RIP                 | Routage dynamique           |
| DNS                 | Résolution de noms          |
| HTTP                | Service Web                 |
| FTP                 | Transfert de fichiers       |
| LAN                 | Réseaux locaux              |
| WAN                 | Interconnexion des routeurs |
| TCP/IP              | Communication réseau        |

---

## 📚 Compétences mises en pratique

Ce projet permet de démontrer des compétences en :

* Conception d'architectures réseau
* Adressage IPv4
* Subnetting
* Routage dynamique
* Configuration de routeurs Cisco
* Configuration de commutateurs
* Services DNS
* Services Web / HTTP
* Services FTP
* Diagnostic réseau
* Troubleshooting
* Documentation technique
* Analyse d'architecture réseau

---

## 📊 Résultats

Le projet permet d'obtenir une infrastructure réseau universitaire structurée avec :

✅ 6 segments réseau
✅ 3 routeurs interconnectés
✅ Routage dynamique RIP
✅ Salle serveurs centralisée
✅ Service DNS
✅ Service Web / HTTP
✅ Service FTP
✅ Connectivité inter-départements
✅ Tests de connectivité et services applicatifs

Les services Web et FTP ont notamment été validés depuis des postes clients situés dans différents segments du réseau.


## 👨‍💻 Auteur

**Nasser Souidi**

Projet réalisé avec **Cisco Packet Tracer** dans le cadre de la conception et de la simulation d'une infrastructure réseau universitaire.


## ⭐ Conclusion

Ce projet constitue une mise en pratique des fondamentaux de l'ingénierie réseau : **adressage IP, routage dynamique, interconnexion LAN/WAN et déploiement de services réseau**.

Il fournit également une base évolutive permettant d'intégrer progressivement des mécanismes plus avancés tels que **VLAN, ACL, SSH, OSPF, pare-feu, supervision et haute disponibilité**.

⭐ Si ce projet vous intéresse, n'hésitez pas à explorer le dépôt et à consulter la documentation complète.

