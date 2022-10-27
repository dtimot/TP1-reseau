## I. First steps
Faites-vous un petit top 5 des applications que vous utilisez sur votre PC souvent, des applications qui utilisent le réseau : un site que vous visitez souvent, un jeu en ligne, Spotify, j'sais po moi, n'importe.

🌞 **Déterminez, pour ces 5 applications, si c'est du TCP ou de l'UDP**
>Spotify
```
-35.186.224.25
-443
-54703
netstat- TCP    10.33.18.163:54703     35.186.224.25:443      ESTABLISHED     5232
```
>Discord
```
-162.159.136.234
-443
-63407
netstat-  TCP    10.33.18.163:59979     162.159.134.232:443    ESTABLISHED     16560
 [Discord.exe]
```
>EpicGamesLauncher
```
-3.218.135.115
-443
-60116
netstat-  TCP    10.33.18.163:60116     3.218.135.115:443      ESTABLISHED     10304
 [EpicGamesLauncher.exe]
```
>TwitchStudio
```
-44.240.230.124
-443
-60318
netstat-  TCP    10.33.18.163:60357     44.240.230.124:443     ESTABLISHED     2156
 [TwitchStudioUI.exe]
```
>Battle net
```
-24.105.29.76
-443
-63234
netstat-  TCP    10.33.18.163:63234     24.105.29.76:443       ESTABLISHED     9828
 [Battle.net.exe]
```

avec Wireshark, on va faire les chirurgiens réseau
déterminez, pour chaque application :

IP et port du serveur auquel vous vous connectez
le port local que vous ouvrez pour vous connecter




Dès qu'on se connecte à un serveur, notre PC ouvre un port random. Une fois la connexion TCP ou UDP établie, entre le port de notre PC et le port du serveur qui est en écoute, on parle de tunnel TCP ou de tunnel UDP.


Aussi, TCP ou UDP ? Comment le client sait ? Il sait parce que le serveur a décidé ce qui était le mieux pour tel ou tel type de trafic (un jeu, une page web, etc.) et que le logiciel client est codé pour utiliser TCP ou UDP en conséquence.

🌞 Demandez l'avis à votre OS

votre OS est responsable de l'ouverture des ports, et de placer un programme en "écoute" sur un port
il est aussi responsable de l'ouverture d'un port quand une application demande à se connecter à distance vers un serveur
bref il voit tout quoi
utilisez la commande adaptée à votre OS pour repérer, dans la liste de toutes les connexions réseau établies, la connexion que vous voyez dans Wireshark, pour chacune des 5 applications

Il faudra ajouter des options adaptées aux commandes pour y voir clair. Pour rappel, vous cherchez des connexions TCP ou UDP.

### MacOS
$ netstat

### GNU/Linux
$ ss

### Windows
$ netstat


🦈🦈🦈🦈🦈 Bah ouais, captures Wireshark à l'appui évidemment. Une capture pour chaque application, qui met bien en évidence le trafic en question.

## II. Mise en place

1. SSH
🖥️ Machine node1.tp4.b1

n'oubliez pas de dérouler la checklist (voir les prérequis du TP)
donnez lui l'adresse IP 10.4.1.11/24


Connectez-vous en SSH à votre VM.
🌞 **Examinez le trafic dans Wireshark**


déterminez si SSH utilise TCP ou UDP

pareil réfléchissez-y deux minutes, logique qu'on utilise pas UDP non ?



repérez le 3-Way Handshake à l'établissement de la connexion

c'est le SYN SYNACK ACK



repérez du trafic SSH
repérez le FIN ACK à la fin d'une connexion
entre le 3-way handshake et l'échange FIN, c'est juste une bouillie de caca chiffré, dans un tunnel TCP

🌞 Demandez aux OS

repérez, avec une commande adaptée (netstat ou ss), la connexion SSH depuis votre machine
ET repérez la connexion SSH depuis votre VM
>tcp        ESTAB      0           0                                  10.4.1.11:ssh                  10.4.1.1:52439

🦈 Je veux une capture clean avec le 3-way handshake, un peu de trafic au milieu et une fin de connexion

2. Routage
Ouais, un peu de répétition, ça fait jamais de mal. On va créer une machine qui sera notre routeur, et permettra à toutes les autres machines du réseau d'avoir Internet.
🖥️ Machine router.tp4.b1

n'oubliez pas de dérouler la checklist (voir les prérequis du TP)
donnez lui l'adresse IP 10.4.1.254/24 sur sa carte host-only
ajoutez-lui une carte NAT, qui permettra de donner Internet aux autres machines du réseau
référez-vous au TP précédent


Rien à remettre dans le compte-rendu pour cette partie.