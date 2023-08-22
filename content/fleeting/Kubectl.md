---
id: Kubectl
date: Jul 11, 2023 at 10:07
---

# Kubectl

C'est l'outil pour contrôler les ressources [[1. Kubernetes|Kubernetes]]. 

## Keywords

Kubectl utilise des verbes pour contrôler ces ressources. Une liste complète peut être afficher avec `--help`. Voici quelque exemple:

1. Get
2. Run
3. Create
4. Delete
5. Describe
6. Replace
7. Scale

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

Certaine resources gardent un index de modification afin de *revert* un changement si jamais un problème survenait. Ce n'est pas toutes les resources qui supportent cette commande. Ceux qui la supportent sont:
- [[20230717-11.07 - Deployments]]
- [[20230815-11.08 - DaemonSet]]
- [[20230815-14.08 - StatefulSet]]

Les commands disponible sont:
1. `history`
2. `pause`
3. `restart`
4. `resume`
5. `status`
6. `undo`

Voir dans les références afin de trouver les paramètres possible pour chacune d'entre-elles.
## Tips

Lorsqu'on utilise le verbe `Get`, il est possible de définir le format d'affichage, et ce format peut être directement du [[Yaml|Yaml]]. Il est donc possible de sauvegarder une ressources en faisant: `kubectl get <resource> <resource_name> -o yaml > output.yaml`.

Pour générer le Yaml d'un objet, il est possible de mettre le flag `--dry-run` pour uniquement générer les resources (Yaml) sans l'appliquer/créer sur le cluster

# References
1. https://kubernetes.io/docs/reference/kubectl/
2. https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout
3. https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/