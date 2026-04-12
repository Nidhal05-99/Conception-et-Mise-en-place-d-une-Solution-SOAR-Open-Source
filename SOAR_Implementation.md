# 🔹 Mise en place du SIEM

Dans le cadre de ce projet SOAR, la première étape a consisté à déployer la brique **SIEM (Security Information and Event Management)**.

Le SIEM assure la centralisation, l’analyse et la corrélation des événements de sécurité afin de permettre la détection des activités suspectes en temps réel. La solution open source **Wazuh** a été retenue pour cette implémentation.

---

## ⚙️ 1. Installation et configuration du serveur Wazuh

Le serveur Wazuh a été déployé à partir d’une image **OVA (Open Virtual Appliance)** sur **VMware Workstation** 🖥️. Cette approche a permis de disposer d’un environnement préconfiguré, facilitant un déploiement rapide, stable et optimisé de la plateforme SIEM.

![Figure 1](../images/Installation_Wazuh.png)  
*Figure 1 : Installation du serveur Wazuh*
