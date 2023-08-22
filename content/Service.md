---
id: Service
date: Aug 16, 2023 at 12:08
tags: draft, kubernetes
---

C'est une ressource [[1. Kubernetes]].
# Service
C'est l'opérateur qui permet la communication entre des [[1. Pods]]. Il s'exécute dans le [[Kube-Controller-Manager]]. Il interagit avec l'API server pour configurer le [[20230710-15.07 - CNI|CNI]] et [[Kube-Proxy]]. Un service crée également un opérateur [[20230719-13.07 - Kubernetes Endpoints|Endpoint]] qui permet de collecter un (ou des) IP éphémère de Pods qui on des [[20230815-12.08 - Labels|Labels]] qui match le sélecteur du service.
## Fonctionnement
Chaque requête à l'API seront envoyé au [[20230710-15.07 - CNI|CNI]]. Celui-ci communique avec l'agent sur chaque node (ça peut être des [[20230815-11.08 - DaemonSet|DaemonSet]]). Dans le cas de calico, ce serait `calico-node`. En plus des requêtes vers le CNI, des requêtes vers [[Kube-Proxy]] sont envoyé afin qu'il puisse configurer son firewall correctement.
Voici une image qui exprime le fonctionnement d'un service:
![[g7mn32prjgih-ServicesDiagramProxy.png]]
Dans cette image, on voit deux worker nodes et le control plane constitué d'une seule node. Les deux worker possède un [[1. Pods]] nommé `MyApp`. Ces deux Pods ont un IP éphémère. Un endpoint est crée par le service avec IP `10.128.0.44`. L'[[20230719-13.07 - Kubernetes Endpoints|Endpoint]] dirige vers l'IP éphémère des Pod `MyApp`. Un port d'écoute est crée, et chaque node commence la lecture de ce port, dans ce cas `35001`. Dans les règles de firewall de Kube-Proxy, n'importe quel node devrait envoyé les requête vers l'Endpoint. Donc un utilisateur est en mesure d'accéder à `MyApp` en accédant au port `35001` de *n'importe quel node*.

> [!question]
> Dans un endpoint, quel IP éphémère aura priorité? Dans l'exemple plus haut, est-ce qu'on attendrait toujours `MyApp` sur worker-2, ou ce serait balancer entre les 2 workers?

Un autre exemple de déploiement complexe dans un environnement multi-container:
![[k9384xxsvbjw-Service_Network.png]]
## Types
Il existe plusieurs types de service. Certain sont dépendant de d'autre service et doivent les créer avant.
### ClusterIP
C'est le type le plus simple. Un IP est associé au service dans le range qui est définie au démarrage de l'API server dans `service-cluster-ip-range`. Il associe sont IP avec les Pods qui match sont sélecteur avec les [[20230815-12.08 - Labels|Labels]] définit. 
### NodePort
Pour ce type de service, l'opérateur crée d'abord un ClusterIP. Après il assigne un port dans le range définie au démarrage de l'API server dans `node-port-range`. Ce port sera écouter sur chaque node et le traffic sera envoyé à l'Endpoint du service (soit le ClusterIP). Donc tous utilisateurs externe sera en mesure d'accéder au service en accédant à l'IP d'une node et le port qui à été attribuer à ce service.
### LoadBalancer
Ce type ne crée pas réellement de LoadBalancer. Il crée plutôt un NodePort et fait une requête asynchrone pour utilisé un LoadBalancer. Si un listener reçoit la requête, il pourra créer les resources nécessaire et envoyé le status. Dans le cas qu'il n'y a pas de listeners, la requête restera `Pending` et aucun IP accessible par l'externe ne sera disponible.
## Labels
Les labels servent comme sélecteur pour définir où le traffic d'un service doit se rendre. 
## Proxy
Si on fait `kubectl proxy`, nous sommes en mesure de tester un service en faisant des appels à l'API de Kubernetes. Par exemple, un service nommé `peenuts` dans le namespace `default` peut se faire appelé ainsi: `http://127.0.0.1:8001/api/v1/namespaces/default/peenuts[:<port-name>]`. 
# References
1. 