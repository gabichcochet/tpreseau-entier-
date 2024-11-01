### TP 2 RESEAU ###
### Simplest LAN ###
1) 🌞 Prouvez que votre configuration est effective

```
PS C:\Users\fabdj> ipconfig
Carte Ethernet Ethernet :
   Suffixe DNS propre à la connexion. . . :
   Adresse IPv4. . . . . . . . . . . . . .: 10.10.13.15
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :
```

1) 🌞 Tester que votre LAN + votre adressage IP est fonctionnel

```
PS C:\Users\fabdj> ping 10.10.13.20

Envoi d’une requête 'Ping'  10.10.13.20 avec 32 octets de données :
Réponse de 10.10.13.20 : octets=32 temps=2 ms TTL=128
Réponse de 10.10.13.20 : octets=32 temps=3 ms TTL=128
Réponse de 10.10.13.20 : octets=32 temps=2 ms TTL=128
Réponse de 10.10.13.20 : octets=32 temps=2 ms TTL=128

Statistiques Ping pour 10.10.13.20:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 2ms, Maximum = 3ms, Moyenne = 2ms
```

1) 🌞 Capture de ping

-ping2.pcapng

### Utilisation des ports ###
1) 🌞 Sur le PC serveur

```
PS C:\Users\fabdj\netcat-win32-1.11\netcat-1.11> ./nc.exe -l -p 1234
```

1) 🌞 Sur le PC client

```
   PS C:\Users\fabdj\netcat-win32-1.11\netcat-1.11> ./nc.exe 10.10.13.15 1234
```

2) 🌞 Echangez-vous des messages

```
PS C:\Users\fabdj\netcat-win32-1.11\netcat-1.11> ./nc.exe -l -p 1234
yo
quoi

feur
ça marche
```

1) 🌞 Utilisez une commande qui permet de voir la connexion en cours

```
PS C:\WINDOWS\system32> netstat -a -b -n
 TCP    10.10.13.15:1234       10.10.13.15:39962      ESTABLISHED
 [nc.exe]
```

1) 🌞 Faites une capture Wireshark complète d'un échange
   -netcat1.pcapng
2) 🌞 Inversez les rôles
   -netcat2.pcapng
### Analyse de vos applications usuelles ###
1) 🌞 Utilisez Wireshark pour capturer du trafic HTTP
   -http.pcapng
2) 🌞 Pour les 5 applications
   -service1(minecraftlauncher).pcapng
   -service2(spotify).pcapng
   -service3(dropbox).pcapng
   -service4(microsoftteams).pcapng
   -service5(grammarly).pcapng
