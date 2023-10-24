# Hein?
C'est l'outil principale pour utiliser [[1. Kubernetes]]. Il permet de créer, modifier, supprimer des resources sur le cluster. Ça ne sert à rien d'expliquer tout ce que l'outil peut faire. La documentation se trouve [ici](https://kubernetes.io/docs/reference/kubectl/).
## Modification d'objet

Il est courant de modifier un objet pour le mettre à jour avec de nouvelle information. Pour appliquer une modification, plusieurs options s'offrent à l'utilisateur.

1. `Apply`, 3-way diff (compare configuration ancienne, configuration courante et la configuration que l'utilisateur tente d'appliquer)
2. `Edit` (performe un get, ouvre un éditeur de texte, puis fais un `apply`)
3. `Patch`
## Logs
Ça permet de voir les logs d'un container. Il est possible de voir les logs de différent container d'un [[1. Pods]].
## Debug
Il est possible d'attacher un container éphémère à un Pod afin de debug un problème. Pour ce faire, il est possible d'exécuter `kubectl debug [-i] [-t] --image=<image> --attach
## Rollout
Les informations concernant le rollout de ressource ce trouve [[Kubernetes Rollout|ici]].
## Obtenir le YAML d'une Ressource

Lorsqu'on utilise le verbe `Get`, il est possible de définir le format d'affichage, et ce format peut être directement du [[Yaml]]. Il est donc possible de sauvegarder une ressources en faisant: `kubectl get <resource> <resource_name> -o yaml > output.yaml`.

Pour générer le Yaml d'un objet, il est possible de mettre le flag `--dry-run` pour uniquement générer les resources (Yaml) sans l'appliquer/créer sur le cluster, donc `kubectl get <resource> <name> --dry-run=client -o yaml`.
