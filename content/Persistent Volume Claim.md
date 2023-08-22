---
id: Persistant Volume Claim
date: Aug 16, 2023 at 09:08
tags: kubernetes
---

C'est une ressource [[1. Kubernetes]] qui permet la [[20230815-15.08 - Kubernetes Persistance|Persistance]] des données.
# PersistentVolumeClaim
C'est une demande d'accéder au ressource d'un [[Persistent Volume]]. Un PVC n'a pas besoin de pointer directement vers un PV, puisqu'il vas prendre le premier PV valide et disponible.

Un exemple d'un manifest d'un PVC:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: pvc-one
spec:
	accessModes:
		- ReadWriteMany
	resources:
		requests:
			storage: 200Mi
```
# References
1. 