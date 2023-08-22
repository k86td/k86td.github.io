---
id: CRI
date: Jul 10, 2023 at 16:07
---

# Container Runtime Interface

>[!info]
>Cette page fais partie de ma recherche actuelle à propos de Kubernetes. Il est possible que certaine information soit mauvaise.

C'est une interface entre un [[Container Runtime]] et l'API de [[1. Kubernetes|Kubernetes]]. Sa permet de changer le comportement de Kubernetes sans re-compiler l'application au complet. Ça exprime l'API gRPC qui est utilisé entre Kubelet et le Container Runtime.

# References
1. https://kubernetes.io/docs/concepts/architecture/cri/