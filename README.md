# 🧭 Projet : Audit de Sécurité d'un Réseau Local Simulé

Ce projet a pour objectif de simuler un test d'intrusion (pentest) sur un réseau local virtualisé. Il couvre les premières étapes de la reconnaissance : la découverte des machines actives et l'analyse des ports et services exposés.

## 🏛️ Architecture du Laboratoire

Le laboratoire est composé des machines virtuelles suivantes, configurées en réseau interne (`Internal Network` sur VirtualBox) :

- **Machine Attaquant :**
  - **OS :** Kali Linux
  - **IP :** `10.0.2.15` (obtenue via DHCP)
- **Serveur Web Vulnérable :**
  - **OS :** Linux (via l'image Metasploitable ou DVWA)
  - **IP :** `10.0.2.4` (IP fixe ou DHCP)
- **Machine Cible :**
  - **OS :** Windows 10
  - **IP :** `10.0.2.6` (IP fixe ou DHCP)

## 📂 Structure du Dépôt

- **01-Configuration_Environnement** : Contient les instructions pour recréer l'environnement de test.
- **02-Resultats_Scans** : Contient les résultats bruts des scans `nmap`.
- **03-Rapport_Analyse** : Contient l'analyse détaillée des résultats et les conclusions.

## 🚀 Étapes du Projet

1.  **Configuration de l'environnement** : Mise en place du réseau et des VMs.
2.  **Scan du réseau** : Identification des hôtes actifs.
3.  **Analyse des ports et services** : Découverte des points d'entrée potentiels.
4.  **Rapport** : Synthèse des informations collectées.
