Pour cette fois, la commande
```find / -user flag01 2>/dev/null```
et 
```find / -user level01 2>/dev/null```
ne retournent rien on va devoir trouver autre chose

En cherchant le fichier /etc/shadow (fichier ou les user mdp sont en hash) je me suis rendu compte que je n'avais pas les droits pour lire le fichier
Alors je me suis rabattu sur /etc/passwd , fichier assez similaire mais sur lequel j'ai les droits. 
En le lisant je tombe sur une ligne 
```level01@SnowCrash:~$ cat /etc/passwd | grep flag01
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash```

On peut voir ici le mot de passe hash de flag01.
On peut donc le de-hash avec l'outil john 
```john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt```

hash.txt contenant
```flag01:42hDRfypTqqnw```

On affiche le resultat : 
```john --show hash.txt                                     
flag01:abcdefg```

Le mot de passe du compte flag est connu, on peut se connecter et recuperer le flag
