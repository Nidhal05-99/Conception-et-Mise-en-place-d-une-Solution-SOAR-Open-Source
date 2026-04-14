# 🔹 Mise en place du SIEM

Dans le cadre de ce projet SOAR, la première étape a consisté à déployer la brique **SIEM (Security Information and Event Management)**.

Le SIEM permet la **centralisation, l’analyse et la corrélation des événements de sécurité**, afin de détecter en temps réel les activités suspectes et les comportements anormaux au sein du système d’information.

La solution open source **Wazuh** a été retenue pour cette implémentation, en raison de ses capacités avancées en matière de supervision, de détection d’intrusion et de gestion des événements de sécurité.

---

## ⚙️ 1. Installation et configuration du serveur Wazuh

Le serveur Wazuh a été déployé à partir d’une image **OVA (Open Virtual Appliance)** sur **VMware Workstation** 🖥️. Cette approche a permis de disposer rapidement d’un environnement **préconfiguré, stable et optimisé**, facilitant le déploiement de la plateforme SIEM.

Les accès à la machine virtuelle OVA ont été définis comme suit :  
- **Username :** wazuh-user  
- **Password :** wazuh  

![Figure 1](/images/Installation_Wazuh.png)  
*Figure 1 : Installation du serveur Wazuh sur VMware Workstation*

---

## 🌐 Accès à l’interface web Wazuh

Après la phase d’installation et de configuration, nous avons procédé à l’accès à l’interface web de **Serveur Wazuh** afin de vérifier le bon fonctionnement du SIEM et d’activer la supervision des événements de sécurité.

Cette interface permet une **visualisation centralisée des alertes, événements et états de sécurité** du système.

Les accès à l’interface ont été configurés lors du déploiement de la solution.

![Figure 2](/images/Interface_graphique_wazuh.png)  
*Figure 2 : Interface web du dashboard Wazuh*

---

## ⚙️ 2. Installation de l’agent Wazuh

Afin d’étendre les capacités de supervision du SIEM, nous avons procédé à l’installation de l’agent **Wazuh** sur la machine **Ubuntu Server**.

Cette étape permet de générer les clés d’authentification pour établir une communication sécurisée entre l’agent et le serveur. La figure ci-dessous montre l’ajout de l’agent Ubuntu depuis l’interface d’administration.

![Figure 3](/images/Ajout_agent_ubuntu.png)  
*Figure 3 : Ajout de l’agent Ubuntu sur le serveur Wazuh*

Dans cette étape, nous avons procédé à l’installation et à la configuration de l’agent **Wazuh** sur le serveur **Ubuntu** comme montre la figure suivante.

![Figure 4](/images/Installation_agent.png)  
*Figure 4 : Installation de l’agent Wazuh sur le serveur Ubuntu*


Après avoir finalisé la phase de déploiement, nous avons vérifié l’état et l’activation de l’agent Wazuh afin de confirmer la bonne communication avec le serveur.

![Figure 5](/images/Etat_agent_ubuntu.png)  
*Figure 5 : État de l’agent Wazuh sur Ubuntu Server*

---

## 🔎 Vérification de l’ajout de l’agent Wazuh

Après l’installation de l’agent Wazuh sur Ubuntu 24.04, nous avons procédé à la vérification de son ajout et de son enregistrement sur le serveur Wazuh. Cette étape permet de confirmer que l’agent est correctement détecté et intégré dans la plateforme SIEM, assurant ainsi la remontée des événements de sécurité.

![Figure 6](/images/Verification_de_agent_Wazuh.png)  
*Figure 6 : Vérification de l’agent Wazuh*

## 📊 Visualisation des événements et du dashboard

Dans cette figure, nous présentons le **dashboard Wazuh** associé au serveur Ubuntu. Il permet de visualiser en temps réel les principaux indicateurs de sécurité, notamment le nombre d’authentifications réussies, le nombre d’échecs d’authentification, ainsi que le volume total des alertes générées, ainsi que d’autres informations relatives à l’état de sécurité du serveur Ubuntu.

Cette vue centralisée offre une meilleure visibilité sur l’activité du système et facilite l’analyse des événements de sécurité du serveur Ubuntu.

![Figure 7](/images/Dashboard_wazuh.png)  
*Figure 7 : Tableau de bord de sécurité du serveur Ubuntu sur Wazuh*

## 📥 Collecte et analyse des logs

Le serveur Wazuh intercepte les logs et alertes générés par l’agent Ubuntu. Cette centralisation permet d’assurer une visibilité complète sur les événements de sécurité du système.

La figure ci-dessous présente les journaux collectés depuis le serveur Ubuntu.

![Figure 8](/images/Logs_ubuntu.png)  
*Figure 8 : Journaux de sécurité collectés depuis le serveur Ubuntu via Wazuh*

## 🧠 Analyse MITRE ATT&CK

Les activités observées sur la machine Ubuntu sont également analysées selon MITRE ATT&CK.
La figure suivante montre cette analyse

![Figure 9](/images/MITRE_ATT&CK.png)  

*Figure 9 : Techniques MITRE ATT&CK pour Ubuntu Server*

---

## ⚙️ 3. Installation et configuration de Suricata (IDS/IPS)

Dans cette étape, nous avons procédé à l’installation et à la configuration de **Suricata**, un système de détection et de prévention d’intrusion (IDS/IPS). Cet outil permet d’analyser le trafic réseau en temps réel afin d’identifier les activités suspectes et les menaces potentielles.

Pour installer Suricata, nous avons commencé par mettre à jour les paquets du système, puis procéder à son installation via le gestionnaire de paquets APT.

```bash
sudo apt-get update
sudo apt-get install suricata
```
Après l’installation, nous avons démarré le service Suricata et activé son lancement automatique au démarrage du système afin d’assurer son fonctionnement continu.

```bash
systemctl start suricata
systemctl enable suricata
```

Après une installation réussie, nous avons vérifié l’état du service Suricata sur la machine Ubuntu afin de confirmer son bon fonctionnement et son exécution correcte. La figure suivante illustre l’état du service Suricata après son démarrage.

![Figure 10](/images/Etat_suricata.png)  
*Figure 10 : État du service Suricata sur la machine Ubuntu*

Une fois la configuration de Suricata effectuée, nous avons testé la surveillance de la machine Ubuntu en exploitant les journaux de détection, notamment le fichier **fast.log**, afin de vérifier la génération et la remontée des alertes réseau.

```bash
sudo cat /var/log/suricata/fast.log
```
![Figure 11](/images/Logs_suricata.png)  
*Figure 11 : Surveillance des événements réseau via le fichier fast.log de Suricata*

Nous avons intégré **Suricata avec Wazuh** afin de centraliser les alertes réseau dans l’interface du SIEM. Cette intégration permet la remontée automatique des événements générés par Suricata (intrusions, scans de ports, activités suspectes) vers Wazuh.

La configuration a été réalisée en adaptant le fichier **ossec.conf** afin de permettre à Wazuh de lire les logs **EVE JSON** produits par Suricata, comme illustré dans la figure suivante.

![Figure 12](/images/Wazuh_Suricata.png)  
*Figure 12 : Intégration de Suricata avec Wazuh via ossec.conf*

Comme illustré dans la figure ci-dessus, les alertes générées par Suricata sont désormais visibles directement dans l’interface Wazuh.

![Figure 13](/images/Log_suricata_Wazuh.png)  
*Figure 13 : Visualisation des alertes Suricata dans l’interface Wazuh*

---

## ⚙️ 4. Installation et configuration de TheHive, Cortex et MISP

Pour la mise en place des plateformes **TheHive, Cortex et MISP**, un fichier **Docker Compose** a été utilisé afin de déployer une architecture multi-services.

Les conteneurs ont été lancés via la commande `docker compose up`, permettant un déploiement en arrière-plan.

La figure suivante illustre l’interface graphique de la plateforme **TheHive**, accessible via le port **9000**.

![Figure 14](/images/Interface_graphique_TheHive.png)  
*Figure 14 : Interface graphique de la plateforme TheHive*

Cette figure montre l’interface graphique de la plateforme **Cortex**,accessible via le port **9001**.


![Figure 15](/images/Interface_graphique_cortex.png)  
*Figure 15 : Interface graphique de la plateforme Cortex*

La figure suivante montre l’interface graphique de la plateforme **MISP**.

![Figure 16](/images/Interface_graphique_MISP.png)  
*Figure 16 : Interface graphique de la plateforme MISP*


## 🔗 Intégration de Cortex et MISP

Dans cette étape, nous avons intégré **Cortex avec MISP** afin de permettre l’enrichissement automatique des observables et le partage des indicateurs de compromission (IOCs).

Cette intégration repose sur la configuration de l’**URL du serveur MISP** ainsi que sur l’utilisation de la **clé API (API Key) MISP** associée à un utilisateur dédié, permettant l’authentification sécurisée et la communication entre les deux plateformes.

![Figure 17](/images/Integration_MISP-Cortex.png)  
*Figure 17 : Intégration de Cortex avec MISP via API Key*

Après l’intégration, nous avons ajouté un analyseur **MISP** dans la plateforme **Cortex**..

![Figure 18](/images/Ajout_MISP_Cortex.png)  
*Figure 18 : Ajout de l’analyseur MISP dans Cortex*

## 🔗 Intégration de TheHive et Cortex

Dans cette étape, nous avons procédé à l’intégration de **TheHive avec Cortex** afin de permettre l’enrichissement automatique des observables et l’analyse des artefacts dans le cadre de la gestion des incidents de sécurité.

Cette intégration a été réalisée en utilisant l’**API Key Cortex** ainsi que l’**URL du serveur Cortex**, permettant une communication sécurisée et stable entre les deux plateformes, ainsi que l’exécution des analyzers directement depuis TheHive.

![Figure 19](/images/Integration_TheHive-Cortex.png)  
*Figure 19 : Intégration de TheHive avec Cortex*

Suite à l’intégration réussie entreWazuh et TheHive, la transmission fluide des alertes de sécurité a été rendue possible.

La figure suivante illustre des événements générés par Wazuh, automatiquement remontés dans TheHive pour analyse.

![Figure 20](/images/Alerte_TheHive.png)  
*Figure 20 : Alertes TheHive*


## 🔗 Intégration de Wazuh et TheHive

Dans cette phase, nous avons procédé à l’intégration de **Wazuh avec TheHive** afin d’automatiser le traitement et la gestion des alertes de sécurité.

Cette intégration a été réalisée via l’installation du module **thehive4py** sur le serveur Wazuh, permettant ainsi la communication et l’envoi automatique des alertes vers la plateforme TheHive.

La figure suivante illustre l’installation de ce module et la mise en place de cette intégration.

![Figure 21](/images/Installation_TheHive4py.png)  
*Figure 21 : Installation de TheHive4py sur Wazuh*

La configuration a été réalisée en ajoutant l’URL, le port et la clé API de TheHive dans le fichier /var/ossec/etc/ossec.conf.
La figure suivante illustre cette configuration. 

![Figure 22](/images/Integration_Wazuh_Thehive.png)  
*Figure 22 :  Intégration de Wazuh et TheHive*

## 🧪 5. Test de sécurité de la solution SOAR

Nous avons réalisé un test de sécurité afin de valider le bon fonctionnement de la solution **SOAR**.

Une attaque de type **brute force** a été simulée à l’aide de l’outil **Hydra** depuis une machine Kali Linux vers une machine endpoint, afin de générer des événements de sécurité et vérifier leur détection par la plateforme.

![Figure 23](/images/ip_kali.png)  
*Figure 23 : IP de la machine Kali Linux*

![Figure 24](/images/Attaque_Brute_Force.png)  
*Figure 24 : Simulation d’une attaque brute force*

Suite à la simulation de l’attaque par brute force, une alerte de sécurité a été automatiquement générée et reçue sur la plateforme **Wazuh**.

Cette alerte fournit des informations précises, notamment l’**adresse IP de la machine cible**, l’**adresse IP de la source de l’attaque**, ainsi que le**port réseau** impliqué, facilitant ainsi l’analyse et la traçabilité de l’incident.

Comme illustré dans la figure suivante :

![Figure 25](/images/Brute_force_detection_wazuh.png)  
*Figure 25 : Alerte Wazuh pour attaque par force brute*

Dès la détection de l’alerte par Wazuh, une alerte correspondante a été automatiquement créée dans TheHive.

![Figure 26](/images/Alerte_envoyées_à_TheHive.png)  
*Figure 26 : Alerte de sécurité envoyée à TheHive*
