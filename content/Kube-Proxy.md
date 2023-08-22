---
id: Kube-Proxy
date: Jul 19, 2023 at 15:07
tags: kubernetes, draft
---

# Kube-Proxy

C'est un composant de [[1. Kubernetes|Kubernetes]].

Permet de créer des streams de connexion entre chacune des nodes pour forwarder des requêtes. Il est possible d'utiliser TCP, UDP ou SCTP (avec ou sans round-robin).

## Working-Mode
Le proxy peut changer sont comportement selon les paramètres de configuration à sa disposition.
### Iptables
Dans ce mode de fonctionnement, le proxy reçoit toujours des updates de l'API server pour des changements dans un Service ou Endpoint. Si il y a des changements, il doit modifier ces règles.
# References
1. https://kubernetes.io/docs/reference/command-line-tools-reference/kube-proxy/