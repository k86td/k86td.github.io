---
id: Kube-Controller-Manager
date: Jul 19, 2023 at 15:07
---

# Kube-Controller-Manager
C'est un agent qui fais partie de [[1. Kubernetes|Kubernetes]].

C'est un processus critique qui gère le *Control Loop* en demandant le status actuelle du cluster à [[Kube-Apiserver]]. Si le status n'est pas celui demander, il contactera les *Controllers* nécessaire. Il y a en pratique plusieurs *Operators*, tel `Endpoints`, `Namespace` et `Replication`.
# References
1. 