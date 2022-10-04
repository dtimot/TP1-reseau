# I. Exploration locale en solo

## 1 Affichage d'informations sur la pile TCP/IP locale

En ligne de commande
En utilisant la ligne de commande (CLI) de votre OS :

🌞 **Affichez les infos des cartes réseau de votre PC**

>ipconfig /all
```
Carte réseau sans fil Wi-Fi :

Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6 AX200 160MHz
Adresse physique . . . . . . . . . . . : 4C-79-6E-9C-8B-73
Adresse IPv4. . . . . . . . . . . . . .: 10.33.16.148(préféré)
```
### Je n'ai pas de carte ethernet

🌞 **Affichez votre gateway**
```
  Passerelle par défaut. . . . . . . . . : 10.33.19.254
```

🌞 **Déterminer la MAC de la passerelle**
```
  10.33.19.254          00-c0-e7-e0-04-4e     dynamique
```
## En graphique (GUI : Graphical User Interface)
#### En utilisant l'interface graphique de votre OS :
🌞 **Trouvez comment afficher les informations sur une carte IP (change selon l'OS)**
```
Carte réseau sans fil Wi-Fi :

   Adresse physique . . . . . . . . . . . : 4C-79-6E-9C-8B-73
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.16.148(préféré)
   Passerelle par défaut. . . . . . . . . : 10.33.19.254
```
🌞 **Utilisez l'interface graphique de votre OS pour changer d'adresse IP :**

changez l'adresse IP de votre carte WiFi pour une autre
ne changez que le dernier octet
```
-> panneau de configuration
-> Réseau et internet 
-> Centre reseau et partage 
-> Modifier les parametres de partage avancé
-> ipv4
-> changer l'adresse
```
🌞 **Il est possible que vous perdiez l'accès internet. Que ce soit le cas ou non, expliquez pourquoi c'est possible de perdre son accès internet en faisant cette opération.**
```
apres avoir changé l'adresse ip, ça ne reconait pas
```
🌞 **Modifiez l'IP des deux machines pour qu'elles soient dans le même réseau**

>Panneau de configuration -> Réseaux et internet -> Centre réseaux et partage -> Modifier les paramètres de la carte-> Clique droit Réseaux Ynov -> Propriétés -> Protocole Internet version 4 (TCP/IPv4)

```
Adresse IP: 10.10.10.155
Masque de sous-réseau: 255.255.255.0
```

🌞 **Vérifier à l'aide d'une commande que votre IP a bien été changée**

>ipconfig

```
Carte Ethernet Ethernet :

   Adresse IPv4. . . . . . . . . . . . . .: 10.10.10.155
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
```

🌞 **Vérifier que les deux machines se joignent**

- utilisez la commande `ping` pour tester la connectivité entre les deux machines

> ping 10.10.10.252

```
Envoi d’une requête 'Ping'  10.10.10.252 avec 32 octets de données :
Réponse de 10.10.10.252 : octets=32 temps=6 ms TTL=128
Réponse de 10.10.10.252 : octets=32 temps=3 ms TTL=128
Réponse de 10.10.10.252 : octets=32 temps=3 ms TTL=128
Réponse de 10.10.10.252 : octets=32 temps=3 ms TTL=128

Statistiques Ping pour 10.10.10.252:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 3ms, Maximum = 6ms, Moyenne = 3ms
```

🌞 **Déterminer l'adresse MAC de votre correspondant**

> arp -a

Interface : 10.10.10.155 --- 0xb
  Adresse Internet      Adresse physique      Type
  10.10.10.252          b4-45-06-bf-f7-76     dynamique

## 4. Utilisation d'un des deux comme gateway

🌞**Tester l'accès internet**

>ping 8.8.8.8

```
Envoi d’une requête 'Ping'  8.8.8.8 avec 32 octets de données :
Réponse de 8.8.8.8 : octets=32 temps=23 ms TTL=113
Réponse de 8.8.8.8 : octets=32 temps=24 ms TTL=113
Réponse de 8.8.8.8 : octets=32 temps=23 ms TTL=113
Réponse de 8.8.8.8 : octets=32 temps=24 ms TTL=113
```

🌞 **Prouver que la connexion Internet passe bien par l'autre PC**

>tracert 192.168.137.1

```
Détermination de l’itinéraire vers DESKTOP-URQ404I [192.168.137.1]
avec un maximum de 30 sauts :

  1     1 ms     1 ms    <1 ms  DESKTOP-URQ404I [192.168.137.1]

Itinéraire déterminé.
```

🌞 **Activez et configurez votre firewall**
>autoriser les ping
```
-> pare-feu 
-> parametre avancés
-> nouvelle regle 
-> presonaliser 
-> icpmv4
-> adresses ip respectives
```
>autoriser le traffic sur le port qu'utilise nc
```
flem
```
🌞 **Exploration du DHCP, depuis votre PC**
```
```