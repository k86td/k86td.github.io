# Deployment
C'est une resource [[1. Kubernetes]]. C'est une resource par dessus un [[ReplicaSet]]. Un déploiement gère le status également du déploiement et permet de modifier ce status avec les commandes dans `kubectl rollout`. Lorsqu'une nouvelle version est créer, le Déploiement crée un nouveau [[ReplicaSet]] jusqu'à ce que tout les nouveau Pods soit créer. Une fois créer, il supprime l'ancien [[ReplicaSet]]. La documentation de cette ressource ce trouve [ici](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment).

## Rollout
Cette ressource supporte les [[Kubernetes Rollout]].