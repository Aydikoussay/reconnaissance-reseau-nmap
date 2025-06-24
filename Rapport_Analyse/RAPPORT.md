# 📜 Rapport d'Analyse des Scans

## 1. Résumé des Hôtes Identifiés

Le scan de découverte a permis d'identifier **3 cibles potentielles** sur le réseau `10.0.2.0/24` en plus de notre machine d'attaque :

| Adresse IP | Rôle supposé             | OS probable (basé sur le scan) |
| :--------- | :----------------------- | :----------------------------- |
| `10.0.2.4` | Serveur Web Vulnérable   | Linux (Ubuntu)                 |
| `10.0.2.6` | Poste de travail         | Windows 10                     |
| `10.0.2.1` | Passerelle réseau        | (Non scanné en détail)         |

## 2. Analyse Détaillée par Hôte

### Hôte : `10.0.2.4` (Serveur Linux)

Cet hôte expose plusieurs services critiques.

-   **Port 80 (HTTP)** : Un serveur web **Apache 2.2.8** est en cours d'exécution. Le titre de la page (`DVWA`) confirme qu'il s'agit de notre cible principale pour les attaques web (XSS, SQL Injection, etc.). La version d'Apache est ancienne et potentiellement vulnérable.
-   **Port 21 (FTP)** : Le service `vsftpd 2.3.4` est connu pour avoir une **backdoor critique** (CVE-2011-2523). C'est un point d'entrée potentiel pour obtenir un shell sur la machine.
-   **Port 22 (SSH)** : La version d'OpenSSH est également datée. Une énumération des utilisateurs pourrait être tentée.
-   **Ports 139/445 (Samba)** : Le service de partage de fichiers Samba est actif. Il pourrait être vulnérable à des attaques comme SambaCry si la version est affectée.
-   **Port 3306 (MySQL)** : La base de données est exposée sur le réseau. Des tentatives de connexion avec des identifiants par défaut (`root:root`, `admin:password`, etc.) pourraient aboutir.

### Hôte : `10.0.2.6` (Machine Windows)

Cette machine semble être un poste de travail standard.

-   **Ports 139/445 (SMB)** : Les services de partage de fichiers Windows (SMB) sont ouverts. C'est une surface d'attaque très commune.
    -   **Vecteur d'attaque potentiel** : Si la machine n'est pas à jour, elle pourrait être vulnérable à des exploits comme **EternalBlue (MS17-010)**. Une vérification avec des scripts `nmap` spécifiques (`--script smb-vuln*`) est nécessaire.
-   **Port 135 (MSRPC)** : Le service RPC est accessible, ce qui peut permettre une énumération plus poussée des services et utilisateurs du domaine Windows.

## 3. Conclusion et Prochaines Étapes

La phase de reconnaissance a été un succès. Nous avons identifié deux cibles avec de multiples vecteurs d'attaque potentiels.

Les prochaines étapes seraient :
1.  **Exploitation du FTP sur `10.0.2.4`** : Tenter d'exploiter la backdoor de vsftpd 2.3.4.
2.  **Audit Web sur `10.0.2.4`** : Lancer des outils comme Nikto, Dirb et Burp Suite contre le serveur Apache/DVWA.
3.  **Scan de vulnérabilités SMB sur `10.0.2.6`** : Confirmer la présence de la vulnérabilité MS17-010.
