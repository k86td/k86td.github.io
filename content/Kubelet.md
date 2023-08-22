---
id: Kubelet
date: Jul 19, 2023 at 16:07
---

# Kubelet

C'est en lien avec [[1. Kubernetes|Kubernetes]]

C'est un processus qui peut être gérer avec [[Systemd]]. 

C'est le processus qui gère les changements de configuration sur les nodes. Il reçoit une spécification de pod (`PodSpec`, JSON/Yaml qui décrit un pod) et tente de configurer la node actuelle jusqu'à ce quel atteigne le status désiré. 

Si un Pod nécessite des ressources additionnels, comme un accès au storage, Secret/ConfigMap, Kubelet vas s'assurer l'accessibilité des ressources, et les créer si besoin et possible.

Kubelet retourne le status à [[Kube-Apiserver]] pour de la persistance éventuelle. 

## En Gros

Kubelet fais les tâches suivantes:

1. Applique des `PodSpec`
2. *Mount* des volumes sur des Pod
3. Télécharge des `Secrets`
4. Envoie les requête au [[Container Runtime]] locale
5. Envoie le status à [[Kube-Apiserver]]

## Autres

- Topology Manager (en Alpha)

# References
1. 