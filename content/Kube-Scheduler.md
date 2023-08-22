---
id: Kube-Scheduler
date: Jul 19, 2023 at 15:07
tags: draft
---
# Kube-Scheduler
C'est lui qui détermine quels node vas recevoir un Pod dans un cluster [[1. Kubernetes]].

Ils prend en compte la disponibilité des resources. Un utilisateur à la possibilité de définir la priorité d'un [[1. Pods]]. Créer des [[20230815-12.08 - Labels|Labels]], [[PodAffinity]], [[Tolerations]]. Pour configurer ce fonctionnement, il est possible de créer des profiles pour le `Scheduler`. Ces profiles sont appliqué sur un [[Kube-Scheduler#Extension Point]].
## Profiles
Il est possible d'avoir plusieurs profiles en même temps. Voici un exemple:
```yaml
apiVersion: kubescheduler.config.k8s.io/v1  
kind: KubeSchedulerConfiguration  
profiles:  
  - schedulerName: default-scheduler  
  - schedulerName: custom-scheduler  
    plugins:  
      preFilter:  
        disabled:  
	        - name: '*'  
      filter:  
        disabled:  
	        - name: '*'  
      postFilter:  
        disabled:
	        - name: '*'
```
## Étapes
Le scheduler suit certaines étapes afin de planifier le déploiement de ressource correctement. Les véritables étapes sont des [[Kube-Scheduler#Extension Point]].
### Filtering
C'est le stage qui détermine l'ensemble de node qui sont *capable* d'héberger un Pod. Par exemple, le filtre `PodFitsResources` qui permet de voir qu'une node possède assez de ressource pour avoir un Pod.
### Scoring
Cette étape crée des scores pour chacune des nodes selon des critères spécifique. La node avec le score le plus haut sera celui sur lequel le Pod sera assigné.
## Extension Point
C'est les étapes dans le pipeline du scheduler pour assigné une ressource dans le cluster. Une liste complète des plugins de scheduling se trouve [ici](https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins).
### QueueSort
C'est le plugin qui vas ordonnée la liste des Pods qui ne sont pas encore assigné. Il peut avoir ***uniquement un plugin*** de ce type actif à la fois.
### PreFilter
Permet d'analyser certaine information d'un Pod/Cluster avant l'étape de filtrage. Peut définir un Pod comme unschedulable.
### Filter
Permet d'exclure des nodes qui ne peuvent pas exécuter le Pod. Ils peuvent avoir plusieurs filtres et ils sont exécuter en ordres. Si aucun filtre n'est valide pour le Pod, il est marquer comme unschedulable.
### PostFilter
Ces de la logiques additionnelles qui permet de configurer quel node peuvent héberger la ressource. Il peut y en avoir plusieurs. Si ce plugin marque un Pod comme schedulable, les plugins PostFilter suivant ne seront pas appelé.
### Score
C'est l'Extension Point qui score chaque node pour déterminer celle qui est la plus probable pour héberger la ressource.
# References
1. https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/
2. https://kubernetes.io/docs/reference/scheduling/config/
3. https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins
4. https://www.linkedin.com/pulse/prefilter-vs-filter-postfilter-concepts-k8s-framework-kirill-kazakov