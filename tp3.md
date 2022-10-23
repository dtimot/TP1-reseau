### 1. Echange ARP
🌞**Générer des requêtes ARP**

>   [timothee@localhost ~]$ ping 10.3.1.12
```
PING 10.3.1.12 (10.3.1.12) 56(84) bytes of data.
    64 bytes from 10.3.1.12: icmp_seq=1 ttl=64 time=0.333 ms
    --- 10.3.1.12 ping statistics ---
    1 packets transmitted, 1 received, 0% packet loss, time 0ms
    rtt min/avg/max/mdev = 0.333/0.333/0.333/0.000 ms
```
>[timothee@localhost ~]$ ip neigh show
```
10.3.1.1 dev enp0s8 lladdr 0a:00:27:00:00:08 DELAY
10.3.1.12 dev enp0s8 lladdr 08:00:27:1f:eb:d9 STALE
```
```
10.3.1.1 dev enp0s8 lladdr 0a:00:27:00:00:08 DELAY
10.3.1.11 dev enp0s8 lladdr 08:00:27:53:26:77 STALE
```
prouvez que l'info est correcte (que l'adresse MAC que vous voyez dans la table est bien celle de la machine correspondante)

une commande pour voir la MAC de marcel dans la table ARP de john

et une commande pour afficher la MAC de marcel, depuis marcel

### 2. Analyse de trames
🌞**Analyse de trames**

utilisez la commande tcpdump pour réaliser une capture de trame
videz vos tables ARP, sur les deux machines, puis effectuez un ping


🦈 Capture réseau tp2_arp.pcapng qui contient un ARP request et un ARP reply

Si vous ne savez pas comment récupérer votre fichier .pcapng sur votre hôte afin de l'ouvrir dans Wireshark, et me le livrer en rendu, demandez-moi.

## 1. Mise en place du routage
🌞**Activer le routage sur le noeud router**

Cette étape est nécessaire car Rocky Linux c'est pas un OS dédié au routage par défaut. Ce n'est bien évidemment une opération qui n'est pas nécessaire sur un équipement routeur dédié comme du matériel Cisco.

🌞Ajouter les routes statiques nécessaires pour que john et marcel puissent se ping

il faut taper une commande ip route add pour cela, voir mémo
il faut ajouter une seule route des deux côtés
une fois les routes en place, vérifiez avec un ping que les deux machines peuvent se joindre
> sudo ip route add 10.3.1.0/24 via 10.3.2.254 dev enp0s8 (marcel)

>sudo ip route add 10.3.2.0/24 via 10.3.1.254 dev enp0s8 (john)

```
[timothee@localhost ~]$ ping 10.3.2.12
PING 10.3.2.12 (10.3.2.12) 56(84) bytes of data.
64 bytes from 10.3.2.12: icmp_seq=1 ttl=63 time=1.47 ms
64 bytes from 10.3.2.12: icmp_seq=2 ttl=63 time=1.56 ms
^C
--- 10.3.2.12 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 1.470/1.513/1.557/0.043 ms
```

```
[timothee@localhost ~]$ ping 10.3.1.11
PING 10.3.1.11 (10.3.1.11) 56(84) bytes of data.
64 bytes from 10.3.1.11: icmp_seq=1 ttl=63 time=0.797 ms
64 bytes from 10.3.1.11: icmp_seq=2 ttl=63 time=1.70 ms
^C
--- 10.3.1.11 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1037ms
rtt min/avg/max/mdev = 0.797/1.246/1.695/0.449 ms
```

## 2. Analyse de trames
🌞**Analyse des échanges ARP**

videz les tables ARP des trois noeuds
>ipneigh show

effectuez un ping de john vers marcel
>ping 10.3.2.12 (john)

regardez les tables ARP des trois noeuds
essayez de déduire un peu les échanges ARP qui ont eu lieu
```
Pour aller a marcel john est bien passé par le routeur 
```
répétez l'opération précédente (vider les tables, puis ping), en lançant tcpdump sur marcel
>sudo tcpdump -i enp0s8 -c 10 -w mon_fichier.pcap not port 22

écrivez, dans l'ordre, les échanges ARP qui ont eu lieu, puis le ping et le pong, je veux TOUTES les trames utiles pour l'échange


| ordre | type trame  | IP source | MAC source                   | IP destination | MAC destination            |
|-------|-------------|-----------|------------------------------|----------------|----------------------------|
| 1     | Requête ARP | x         |`marcel` `(08:00:27:34:e5:ad)`| x              |Broadcast `08:00:27:1f:eb:d9`|
| 2     | Réponse ARP | x         |Broadcast `08:00:27:1f:eb:d9` | x              |`marcel` `(08:00:27:34:e5:ad)`|
| ...   | ...         | ...       | ...                          |                |                            |
| ?     | Ping        | ?         | 08:00:27:34:e5:ad            | ?              | 08:00:27:1f:eb:d9          |
| ?     | Pong        | ?         |  08:00:27:1f:eb:d9           | ?              | 08:00:27:34:e5:ad          |
