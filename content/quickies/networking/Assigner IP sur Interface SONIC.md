---
id: 20230628-12.06
date: Jun 28, 2023 at 11:06
---

Assigner un IP sur l'interface d'une switch permet d'agir comme un routeur. 

Première chose à faire est de voir les interfaces disponible. On a qu'a faire `show interfaces status`, et sa montrera les interfaces disponibles sur la switch. Un exemple d'output ressemble à:
```
  Interface            Lanes    Speed
-----------  ---------------  -------
  Ethernet0               49      25G
  Ethernet1               50      25G
  Ethernet2               51      25G
  Ethernet3               52      25G
  Ethernet4               57      25G
  Ethernet5               58      25G
  Ethernet6               59      25G
  Ethernet7               60      25G
  Ethernet8               61      25G
  Ethernet9               62      25G
 Ethernet10               63      25G
 Ethernet11               64      25G
 Ethernet12               77      25G
 Ethernet13               78      25G
 Ethernet14               79      25G
 Ethernet15               80      25G
```

On peut mettre l'interface en ligne en faisant `sudo config interface startup <interface_name>`. Il faut ensuite configurer l'IP sur l'interface. On peut faire ça avec `config interface ip add <nom_interface> <ip>/<cidr_mask>`. Par exemple:
```
sudo config interface ip add Ethernet0 10.0.0.1/24
```

Il est possible par la suite de regarder l'interface que l'on vient de configurer en faisant `show ip interfaces`. Finalement, il est necessaire d'enregistrer la configuration sur le disque. Il est possible de le faire en entrant `sudo config save -y`.

#networking 

# References
1. https://support.edge-core.com/hc/en-us/articles/900000208686--Enterprise-SONiC-Management-and-front-port-IPv4-IPv6-Address