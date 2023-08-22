---
id: Modèle OSI
date: Jun 15, 2023 at 22:06
---

Ça fait partie de la [[Réseautique]].

Le modèle OSI est la norme TCP/IP qui documente comment tout les appareils connecté *doivent* communiqué. C'est exprimé en 7 couches:
![[OSI_Model_v1.svg.png]]

Chaque packet entrant passe par la couche 1 et monte jusqu'à la couche 7. Ils font ensuite le chemin inverse pour retourner à la couche 1.

La **couche 1** est le fils lui même. Il existe plusieurs type de fils, tel des fils coaxiale ou de la fibre. Cette couche est chargé de la conversion entre signaux analogique vers un train de bit, pouvant être utilisé par les appareils. 

La **couche 2** permet de lier plusieurs *hosts* ensemble. Entre-autre, grâce à la mac adresse de chacune des interfaces sur laquelle les fils sont connectés.

#networking 

# References
1. https://fr.wikipedia.org/wiki/Couche_physique
2. https://fr.wikipedia.org/wiki/Mod%C3%A8le_OSI
3. 