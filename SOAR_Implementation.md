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

## ⚙️ 2. Installation de l’agent Wazuh

Afin d’étendre les capacités de supervision du SIEM, nous avons procédé à l’installation de l’agent **Wazuh** sur la machine **Ubuntu Server**.

Cette étape permet de générer les clés d’authentification pour établir une communication sécurisée entre l’agent et le serveur. La figure ci-dessous montre l’ajout de l’agent Ubuntu depuis l’interface d’administration.

![Figure 3](/images/Ajout_agent_ubuntu.png)  
*Figure 3 : Ajout de l’agent Ubuntu sur le serveur Wazuh*

ns cette étape, nous avons procédé à l’installation et à la configuration de l’agent **Wazuh** sur le serveur **Ubuntu** comme montre la figure suivante.

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

Dans cette figure, nous présentons le **dashboard Wazuh** associé au serveur Ubuntu. Il permet de visualiser en temps réel les principaux indicateurs de sécurité, notamment le nombre d’authentifications réussies, le nombre d’échecs d’authentification, ainsi que le volume total des alertes générées, ainsi que d’autres informations relatives à l’état de sécurité du serveur Ubuntu.

Cette vue centralisée offre une meilleure visibilité sur l’activité du système et facilite l’analyse des événements de sécurité du serveur Ubuntu.

![Figure 7](/images/Dashboard_wazuh.png)  
*Figure 7 : Tableau de bord de sécurité du serveur Ubuntu sur Wazuh*

Le serveur Wazuh intercepte les logs et alertes générés par l’agent Ubuntu. Cette centralisation permet d’assurer une visibilité complète sur les événements de sécurité du système.

La figure ci-dessous présente les journaux collectés depuis le serveur Ubuntu.

![Figure 8](/images/Logs_ubuntu.png)  
*Figure 8 : Journaux de sécurité collectés depuis le serveur Ubuntu via Wazuh*

Les activités observées sur la machine Ubuntu sont également analysées selon MITRE ATT&CK.
La figure suivante montre cette analyse

![Figure 10](/images/MITRE_ATT&CK.png)  

*Figure 10 : Techniques MITRE ATT&CK pour Ubuntu Server*
