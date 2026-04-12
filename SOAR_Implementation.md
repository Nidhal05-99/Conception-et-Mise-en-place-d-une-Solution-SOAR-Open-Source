# 🔹 Mise en place du SIEM

Dans le cadre de ce projet SOAR, la première étape a consisté à déployer la brique **SIEM (Security Information and Event Management)**.

Le SIEM assure la centralisation, l’analyse et la corrélation des événements de sécurité afin de permettre la détection des activités suspectes en temps réel. La solution open source **Wazuh** a été retenue pour cette implémentation.

---

## ⚙️ 1. Installation et configuration du serveur Wazuh

Le serveur Wazuh a été déployé à partir d’une image **OVA (Open Virtual Appliance)** sur **VMware Workstation** 🖥️. Cette approche a permis de disposer d’un environnement préconfiguré, facilitant un déploiement rapide, stable et optimisé de la plateforme SIEM.

Les identifiants par défaut de la machine virtuelle OVA sont les suivants :  
- **Username :** wazuh-user  
- **Password :** wazuh
  
![Figure 1](/images/Installation_Wazuh.png)  
*Figure 1 : Installation du serveur Wazuh*

Après avoir terminé l’installation et les configurations nécessaires, nous avons procédé à l’accès à l’interface web de **Wazuh** afin de vérifier le bon fonctionnement du SIEM et de commencer la supervision des événements de sécurité.

Les identifiants utilisés pour l’accès à l’interface sont les suivants :  
- **Username :** admin  
- **Password :** admin  

---

![Figure 2](/images/Dashboard_wazuh.png)  
*Figure 2 : Interface web de Wazuh*
