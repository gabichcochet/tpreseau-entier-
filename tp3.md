### TP3 : 32°13'34"N 95°03'27"W ###

### ☀️ Avant de continuer...

Carte Ethernet Ethernet :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Killer E2600 Gigabit Ethernet Controller
   Adresse physique . . . . . . . . . . . : 08-97-98-E1-9D-06

### ☀️ Affichez votre table ARP :

PS C:\Users\fabdj> arp -a

Interface : 169.254.63.157 --- 0x8
  Adresse Internet      Adresse physique      Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 10.33.77.147 --- 0x18
  Adresse Internet      Adresse physique      Type
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

### ☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école :

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6 AX201 160MHz
   Adresse physique . . . . . . . . . . . : FC-B3-BC-C7-28-6A

### ☀️ Supprimez la ligne qui concerne la passerelle  :

PS C:\WINDOWS\system32> arp -d 10.33.79.254
PS C:\WINDOWS\system32> arp -a 
Interface : 169.254.63.157 --- 0x8
  Adresse Internet      Adresse physique      Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 10.33.77.147 --- 0x18
  Adresse Internet      Adresse physique      Type
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

### ☀️ Prouvez que vous avez supprimé la ligne dans la table ARP :

PS C:\WINDOWS\system32> arp -d 10.33.79.254
PS C:\WINDOWS\system32> arp -a

Interface : 169.254.63.157 --- 0x8
  Adresse Internet      Adresse physique      Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

### ☀️ Wireshark
  -arp1.pcapng


### ☀️ Déterminer

PS C:\WINDOWS\system32> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6 AX201 160MHz
   Adresse physique . . . . . . . . . . . : FC-B3-BC-C7-28-6A
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.180.196(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Bail obtenu. . . . . . . . . . . . . . : Tuesday, October 8, 2024 10:51:42 AM
   Bail expirant. . . . . . . . . . . . . : Tuesday, October 8, 2024 11:55:20 AM
   Passerelle par défaut. . . . . . . . . : 192.168.180.29
   Serveur DHCP . . . . . . . . . . . . . : 192.168.180.29
   Serveurs DNS. . .  . . . . . . . . . . : 192.168.180.29

### ☀️ DIY

PS C:\WINDOWS\system32> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6 AX201 160MHz
   Adresse physique . . . . . . . . . . . : FC-B3-BC-C7-28-6A
   DHCP activé. . . . . . . . . . . . . . : Non
   Configuration automatique activée. . . : Oui
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.180.197(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . : 192.168.180.29
   Serveurs DNS. . .  . . . . . . . . . . : 192.168.180.29
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé

### ☀️ Pingz !

PS C:\WINDOWS\system32> ping google.com

Envoi d’une requête 'ping' sur google.com [216.58.213.78] avec 32 octets de données :
Réponse de 216.58.213.78 : octets=32 temps=71 ms TTL=114
Réponse de 216.58.213.78 : octets=32 temps=53 ms TTL=114
Réponse de 216.58.213.78 : octets=32 temps=71 ms TTL=114
Réponse de 216.58.213.78 : octets=32 temps=47 ms TTL=114

Statistiques Ping pour 216.58.213.78:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 47ms, Maximum = 71ms, Moyenne = 60ms

### ☀️ Affichez votre table ARP !

PS C:\WINDOWS\system32> arp -a

Interface : 169.254.63.157 --- 0x8
  Adresse Internet      Adresse physique      Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

Interface : 192.168.180.197 --- 0x18
  Adresse Internet      Adresse physique      Type
  192.168.180.29        e2-b6-7a-88-24-14     dynamique
  192.168.180.255       ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique

### ☀️ Capture arp2.pcap

-arp2.pcapng