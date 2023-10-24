# ReplicaSet
C'est une resource [[1. Kubernetes]]. Elle crée un ou plusieurs Pod et s'assure qu'il y a toujours le bon nombre de réplique actif. C'est utile pour créer des application et assurer sa disponibilité en routant les requêtes vers d'autre réplique. Sa documentation est [ici](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

## Scaling & Rolling Update
Il est possible de scale un ReplicaSet afin d'augmenter sa quantité de réplique. On n'a qu'à exécuter `kubectl scale replicaset/name --replicas=<new number of replicas>`. Après on peut voir le ReplicaSet possède le nouveau nombre de réplique.
Pour faire une rolling update, on peut faire `kubectl edit replicaset <deployment name>`. Le ReplicaSet sera mis à jour, il est possible de voir les nouveaux pods qui se sont fais créer.