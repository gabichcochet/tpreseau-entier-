### TP5 : Un ptit LAN à nous

### I. Setup
☀️ Uniquement avec des commandes, prouvez-que :
## vous avez bien configuré les adresses IP demandées
## vous avez bien configuré les hostnames demandés

# sur le pc
PS C:\Users\fabdj> ipconfig

Carte Ethernet Ethernet 10 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv4. . . . . . . . . . . . . .: 10.5.1.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

# client1.tp5.b1
gabriel@gabriel-VirtualBox:~$ sudo hostnamectl set-hostname Gabthehostt
[sudo] password for gabriel: 
gabriel@gabriel-VirtualBox:~$ sudo -s
root@Gabthehostt:/home/gabriel# ip a

2: enp0s10: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:49:f4:4b brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global enp0s10
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe49:f44b/64 scope link 
       valid_lft forever preferred_lft forever

# client2.tp5.b1
gabriel@gabriel-VirtualBox:~$ sudo hostnamectl set-hostname Gabthehosttt
[sudo] password for gabriel: 
gabriel@gabriel-VirtualBox:~$ sudo -s
root@Gabthehosttt:/home/gabriel# ip a

2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:08:b5:2d brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.12/24 brd 10.1.1.255 scope global enp0s3
       valid_lft forever preferred_lft forever
    inet 192.168.56.109/24 metric 100 brd 192.168.56.255 scope global dynamic enp0s3
       valid_lft 417sec preferred_lft 417sec
    inet6 fe80::a00:27ff:fe08:b52d/64 scope link 
       valid_lft forever preferred_lft forever

# routeur.tp5.b1
[root@localhost ~]# sudo hostnamectl set-hostname Gabthehost

[root@Gabthehost ~]# ip a
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER,UP> mtu 1500 qdisc fq_codel state UP group deafult qlen 1000 
link/ether 08:00:27:bf:63:e5 brd ff:ff:ff:ff:ff:ff
inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute emp0s3 
valid_lft forever preferred_lft forever 
inet6 fe80::a00:27ff:febf:63e5/64 scope link
valid_lft forever preferred_lft forever


## tout le monde peut se ping au sein du réseau 10.5.1.0/24

# client 1
gabriel@Gabthehostt:~$ ping 10.5.1.254

PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.018 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=0.027 ms
64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=0.033 ms
64 bytes from 10.5.1.254: icmp_seq=4 ttl=64 time=0.042 ms
^C
--- 10.5.1.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3085ms
rtt min/avg/max/mdev = 0.018/0.030/0.042/0.008 ms

# client 2
gabriel@Gabthehosttt:~$ ping 10.5.1.254

PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.019 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=0.064 ms
64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=0.041 ms
64 bytes from 10.5.1.254: icmp_seq=4 ttl=64 time=0.51 ms
^C
--- 10.5.1.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3092ms
rtt min/avg/max/mdev = 0.019/0.043/0.064/0.016 ms


# Routeur à client1
[root@Gabthehost ~]#
PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.014 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64 time=0.035 ms
64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=0.018 ms
^C
--- 10.5.1.254 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2065ms
rtt min/avg/max/mdev = 0.014/0.022/0.035/0.009 ms

# PC à routeur


PS C:\Users\fabdj> ping 10.5.1.254

Envoi d’une requête 'Ping'  10.5.1.254 avec 32 octets de données :
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.5.1.254:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

### Accès internet pour tous

1) Accès internet routeur
### ☀️ Déjà, prouvez que le routeur a un accès internet

[root@Gabthehost ~]# ping google.com
PING ynov.com (172.217.19.142) 56(84) bytes of data.
64 bytes from 172.217.19.142 : icmp_seq=1 time=32 ms ttl=115
64 bytes from 172.217.19.142 : icmp_seq=2 time=34 ms ttl=115
64 bytes from 172.217.19.142 : icmp_seq=3 time=36 ms ttl=115
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2004ms
rtt min/avg/max/mdev = 32.444/34.283/36.320 ms

2) Accès internet clients
### Prouvez que les clients ont un accès internet

gabriel@Gabthehostt-VirtualBox:~$ ping www.ynov.com
PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=51 time=15.5 ms
64 bytes from 104.26.10.233: icmp_seq=2 ttl=51 time=16.7 ms
64 bytes from 104.26.10.233: icmp_seq=4 ttl=51 time=18.9 ms
64 bytes from 104.26.10.233: icmp_seq=5 ttl=51 time=14.9 ms
^C
--- www.ynov.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4072ms
rtt min/avg/max/mdev = 15.548/16.712/18.928/14.922 ms

### ☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau

sur le client 1:

gabriel@Gabthehostt-VirtualBox:~$ cat /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s10:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
      nameservers:
        adresses: [1.1.1.1]

### III. Serveur SSH

### ☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH

[root@Gabthehost ~]# sudo ss -lnpt| grep 22
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=707,fd=3))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=707,fd=4))

### ☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert

[root@Gabthehost ]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s10 enp0s12
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 22/tcp
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

### IV. Serveur DHCP

##  Installation et configuration du serveur DHCP

# ☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1

[root@Gabthehost ]# dnf -y install dhcp-server
[root@Gabthehost dhcp]# sudo nano dhcpd.conf

## Contenu du fichier "dhcpd.conf

# specify DNS server's hostname or IP address
option domain-name-servers  1.1.1.1;
# specify network address and subnetmask
subnet 10.5.1.0 netmask 255.255.255.0 {
    # specify the range of lease IP address
    range dynamic-bootp 10.5.1.137 10.5.1.237;
    # specify broadcast address
    option broadcast-address 10.5.1.255;
    # specify gateway
    option routers 10.5.1.254;
}


[root@Gabthehost dhcp]# systemctl enable --now dhcpd
[root@Gabthehost dhcp]# firewall-cmd --add-service=dhcp
[root@Gabthehost dhcp]# firewall-cmd --runtime-to-permanent

# B. Test avec un nouveau client

# ☀️ Créez une nouvelle machine client client3.tp5.b1
gabriel@client3:~$ sudo hostnamectl
Static hostname: client3.tp5.b1

gabriel@client3:~$ ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:dc:88:db brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s10

gabriel@client3:~$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=51 time=18.6 ms
64 bytes from 104.26.11.233: icmp_seq=2 ttl=51 time=14.4 ms
64 bytes from 104.26.11.233: icmp_seq=3 ttl=51 time=17.5 ms
^C
--- ynov.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
rtt min/avg/max/mdev = 12.134/14.849/16.594/1.030 ms


##### C. Consulter le bail DHCP

[root@Gabthehost dhcpd]# cat /var/lib/dhcpd/dhcpd.leases
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

server-duid "\000\001\000\001.\241\002\361\010\000'\302`\011";

lease 10.5.1.137 {
  starts 2 2024/10/15 20:14:03;
  ends 3 2024/10/16 08:17:29;
  cltt 2 2024/10/15 20:14:03;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:dc:88:db;
  uid "\001\010\000'\361\024\000";
  client-hostname "gabriel-VirtualBox";
}

## ☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC


[root@Gabthehost dhcpd]# cat /var/lib/dhcpd/dhcpd.leases
lease 10.5.1.137 {
  hardware ethernet 08:00:27:dc:88:db;
}

gabriel@client3:~$ ip a
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:dc:88:db brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s8