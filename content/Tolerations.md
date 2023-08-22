---
id: Tolerations
date: Aug 21, 2023 at 16:08
---

# Tolerations
C'est une façon de tolérer des [[20230717-10.07 - Taints|Teintes]] dans [[1. Kubernetes]]. Dans un [[1. Pods]], on peut définir des `tolerations` dans `spec`. Un exemple de configuration serait:
```yaml
tolerations:  
- key: "server"  
  operator: "Equal"  
  value: "ap-east"  
  effect: "NoExecute"  
  tolerationSeconds: 3600
```
Cela aurait pour résultat de permettre à un Pod de s'exécuter 3600 secondes après que la node sur lequel le Pod s'exécute ait la teinte `server=ap-east:NoExecute`.
# References
1. https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/