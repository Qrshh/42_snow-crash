Cette fois-ci, lorsque l'on fait ```ls -la```
On tombe sur le fichier level02.pcap, qu'on va telecharger sur notre ordinateur via cette commande:
```scp -P 4242 level02@<ip>:level02.pcap .```

On va donc l'ouvrir avec wireshark car c'est le seul outil dont nous disposons pour analyser un pcap.

En l'ouvrant, on clique sur n'importe quel flux et on fait :
Follow TCP stream
Ce qui nous donne une session de term ou un login et un mot de passe sont ecrits

Le mot de passe etant : 
ft_wandr...NDRel.L0L 

Les points retiennent mon attention donc, on va regarder la session de terminal en HEX dump au lieu de ASCII

Les points correspondent au nombre hexa 7f, qui correspond au caractere DEL ASCII
On en deduit donc que le mot de passe est :
ft_waNDReL0L

On peut donc se connecter a l'user flag02 et recuperer notre flag
