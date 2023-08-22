---
id: 20230622-14.06
date: Jun 22, 2023 at 14:06
name: IP to Reversed-Domain from an HTML Table
tags: bash
---

On à reçu une liste d'IP qui montrait des signes de vulnérabilités SSLv3 (SSL Poodle). Afin de déterminer l'origine de ces IPs, je voulais trouver le reverse de chacun de ces IPs.

En Bash, il est facile de faire ça. Premièrement, il faut prendre le code source de la page avec la liste des IPs vulnérables. Une fois la page télécharger, il faut l'analyser pour en retirer uniquement les addresses. Ça ressemble à sa:
```bash
cat page.html | \
	htmlq --text ".eventRow td:nth-child(2)" > output.txt
```

Le sélecteur dépend de la page elle même, mais c'est facile à adapter pour sélectionner d'autres sections. Une fois la liste compléter et mise dans un fichier, on peut itérer dans celui-ci:
```bash
while read -r line; \
	do [[ ! -z "$line" ]] && \
	echo "L:$line"; done < output.txt
```

La section `[[ ! -z "$line"]]` s'assure que la variable n'est pas vide, donc que la ligne n'est pas vide. Toutefois, on ne veut pas uniquement écrire la ligne à l'écran, on veut faire un *[[Reverse DNS Lookup]]* sur cet IP. On adapte notre script comme ceci:
```bash
while read -r line; \
	do [[ ! -z "$line" ]] && \
	dig +noall +answer +short -x $line >> reversed.txt; \
	done < output.txt
```

Ici, on utilise la commande *[[Dig]]* et on va chercher le reverse de l'IP. On prend le résultat et on l'ajoute au fichier `reversed.txt`. Il est possible de retirer les doublons en faisant `uniq -u reversed.txt > reversed-unique.txt`. 
# References
1. https://github.com/mgdm/htmlq
2. https://www.w3schools.com/cssref/css_selectors.php
3. https://linuxhint.com/while_read_line_bash/
4. https://serverfault.com/questions/431080/dig-show-only-answer
5. https://www.cyberciti.biz/faq/unix-linux-shell-removing-duplicate-lines/