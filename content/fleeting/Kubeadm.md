---
id: Kubeadm
date: Jul 11, 2023 at 10:07
---


# Kubeadm

C'est l'utilitaire [[1. Kubernetes|Kubernetes]] pour configurer l'accès au cluster, initialiser un cluster, et d'autre chose. C'est une couche par dessus Kubernetes qui permet d'automatiser des étapes répétitives.

## Initialisation

Lors de la création d'un cluster, il y a certaine étapes qui doivent être accomplis avant qu'il soit fonctionnelle. Pour comprendre en détail ces étapes, il existe un guide [Kubernetes The Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way) qui montre *toutes* les étapes manuellement comment un cluster est mis en place.

Avec Kubeadm, il est possible de créer un cluster très simplement. Sa se résume à deux commandes:
1. `kubeadm init`
2. `kubeadm join`

Certain paramètre existe pour modifier le fonctionnement de chaque commande.

## Upgrade

Pour mettre à jour un cluster, il peut être utile d'utiliser `kubeadm upgrade plan` pour planifier la mise à jour.

## Certificats

>[!question]
>À quoi chacun des certificats sert? Et comment l'authentification fonctionne?

Kubernetes nécessite des certificats [[PKI]] pour s'authentifié via [[TLS]]. Les certificats sont enregistrés dans `/etc/kubernetes/pki`. La documentation montre chaque certificat et à quoi ils servent [Ici](https://kubernetes.io/docs/setup/best-practices/certificates/).  

## Kubeadm Init

`--upload-certs`: cette commande mentionne à Kubeadm de mettre les certificats du cluster dans un [[Secret]] nommé `kubeadm-certs`. 

`--config=<path>`: permet de définir le ficher de configuration qu'on veut utiliser pour configurer notre cluster.

## Kubeadm Join

Il est possible de rejoindre un cluster avec un Discovery Token CA Cert Hash et un token. Pour prendre ce hash, il faut exécuter cette commande:
```
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
```
Ce hash sert à valider que le CA est valide sur la node qu'on essaie de rejoindre est valide. Le hash devrait être le même tant que le certificat (`ca.crt`) ne change pas.

`--token`: le token avec lequel on veut rejoindre.

`--discovery-token-ca-cert-hash`: le hash du CA valide.

## Kubeadm Config

Permet d'intéragir avec la configuration du cluster.

### Print

Ça permet d'afficher la configuration par défaut de certaine section du cluster.

# References
1. https://github.com/kelseyhightower/kubernetes-the-hard-way
2. https://kubernetes.io/docs/setup/best-practices/certificates/
3. https://computingforgeeks.com/join-new-kubernetes-worker-node-to-existing-cluster/