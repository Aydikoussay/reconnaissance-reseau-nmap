# 🛠️ Guide de Configuration de l'Environnement

Ce document décrit les étapes pour configurer le laboratoire de test sur VirtualBox.

### Prérequis

-   VirtualBox (ou VMware)
-   Image ISO de Kali Linux
-   Image ISO de Windows
-   Image de la machine vulnérable (ex: [Metasploitable 2](https.information.rapid7.com/download-metasploitable-2017.html) ou une installation manuelle de [DVWA](http://www.dvwa.co.uk/)).

### Étapes de Configuration

1.  **Création du Réseau Interne :**
    -   Dans VirtualBox, toutes les machines virtuelles doivent être configurées pour utiliser un "Réseau Interne" (`Internal Network`).
    -   Donnez un nom à ce réseau, par exemple `pentest-net`.
    -   Assurez-vous que les 3 VMs (Kali, Windows, Serveur) sont sur ce même réseau interne. Cela les isole de votre réseau principal tout en leur permettant de communiquer entre elles.

2.  **Configuration des Adresses IP :**
    -   **Kali Linux (Attaquant) :** Laisser en configuration DHCP. Après démarrage, utiliser la commande `ip a` pour trouver son adresse (ex: `10.0.2.15`).
    -   **Serveur Vulnérable & Windows (Cibles) :** Vous pouvez soit les laisser en DHCP, soit leur assigner des adresses IP fixes pour faciliter les scans (ex: `10.0.2.4` et `10.0.2.6`).

3.  **Vérification :**
    -   Depuis la machine Kali, lancez un `ping` vers les adresses IP des autres machines pour confirmer que la communication est établie.
    ```bash
    ping 10.0.2.4
    ping 10.0.2.6
    ```
