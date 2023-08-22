---
id: Kube-Apiserver
date: Jul 19, 2023 at 15:07
---

# Kube-Apiserver

C'est un agent [[1. Kubernetes|Kubernetes]].

C'est l'élément centrale d'un cluster Kubernetes. Tout appel à l'API est gérer par cet agent.

C'est lui qui gère les instances [[Etcd]] pour que le status du cluster reste valide. Toutes informations persistantes (status du cluster, information réseaux, etc.) sont garder dans les instances Etcd.

#draft 

# References
1. 