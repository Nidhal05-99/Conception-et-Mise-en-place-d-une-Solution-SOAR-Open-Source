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

Après la phase d’installation et de configuration, nous avons procédé à l’accès à l’interface web de **Wazuh Dashboard** afin de vérifier le bon fonctionnement du SIEM et d’activer la supervision des événements de sécurité.

Cette interface permet une **visualisation centralisée des alertes, événements et états de sécurité** du système.

Les accès à l’interface ont été configurés lors du déploiement de la solution.

![Figure 2](/images/Dashboard_wazuh.png)  
*Figure 2 : Interface web du dashboard Wazuh*

## ⚙️ 2. Installation de l’agent Wazuh

Afin d’étendre les capacités de supervision du SIEM, nous avons procédé à l’installation de l’agent **Wazuh** sur la machine **Ubuntu Server**.

Cette étape permet de générer les clés d’authentification pour établir une communication sécurisée entre l’agent et le serveur. La figure ci-dessous montre l’ajout de l’agent Ubuntu depuis l’interface d’administration.

![Figure 3](/images/Ajout_agent_ubuntu.png)  
*Figure 3 : Ajout de l’agent Ubuntu sur le serveur Wazuh



