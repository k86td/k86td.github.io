---
id: Persistant Volume
date: Aug 16, 2023 at 09:08
tags: kubernetes
---

C'est une ressource [[1. Kubernetes]] qui permet la [[20230815-15.08 - Kubernetes Persistance|Persistance]] des données.
# PersistentVolume
Ce sont des volumes qui définissent un accès à des ressources dans un cluster. Ils peuvent définir cet accès selon plusieurs backend de storage. Un PV doit définir une capacité de storage, un backend, un niveau d'accès et optionnellement une politique de retention des données.

## AccessModes
C'est ce champs qui permet de définir les permissions d'accès au storage par le PV. Il y a:
- ReadWriteOnce
- ReadOnlyMany
- ReadWriteMany

Si la permission est `Many`, c'est qu'il est possible d'attacher le volume sur plus d'un Pod.
## Backend de Storage
Il en existe beaucoup. Certain deprecated. C'est eux qui permette réellement l'accès au donnée.
## Politique de Retention des Données
Dans le lifetime des volumes persistants, il y a une étape qui s'appelle le reclaiming. Ça survient après qu'un Pod ait utilisé le PV et sert à le garder dans un état valide. Il existe trois strategy actuellement pour reclaim les données d'un PV. Le champs `persistentVolumeReclaimPolicy` permet de configurer ce fonctionnement. Les valeurs possibles sont expliqué dans le [[20230815-15.08 - Kubernetes Persistance#Lifetime|Lifetime]] des volumes persistants.
### NFS
Ce backend de storage permet de connecter un PV à un dossier NFS. Voici un exemple d'une configuration:
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
name: pv-test
spec:
	capacity:
		storage: 5Gi
	accessModes:
		- ReadWriteMany
	persistentVolumeReclaimPolicy: Retain
	nfs:
		path: /opt/sfw
		server: my-server
		readOnly: false
```
# References
1. 