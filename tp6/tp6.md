# TP6 : Des bo services dans des bo LANs #

1) Le setup

### ☀️ Prouvez que...

# une machine du LAN1 peut joindre internet (ping un nom de domaine)

gabriel@client1:~$ ping google.com
PING google.com (172.217.19.142) 56(84) bytes of data.
64 bytes from mrs08s04-in-f14.1e100.net (172.217.19.142): icmp_seq=1 ttl=114 time=72.2 ms
64 bytes from mrs08s04-in-f14.1e100.net (172.217.19.142): icmp_seq=2 ttl=114 time=48.7 ms
64 bytes from mrs08s04-in-f14.1e100.net (172.217.19.142): icmp_seq=3 ttl=114 time=18.6 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 18.628/46.489/72.181/21.916 ms  

# une machine du LAN2 peut joindre internet (ping nom de domaine)

[gabriel@dns ~]$ ping google.com
PING google.com (142.251.37.238) 56(84) bytes of data.
64 bytes from mrs09s16-in-f14.1e100.net (142.251.37.238): icmp_seq=1 ttl=114 time=24.3 ms
64 bytes from mrs09s16-in-f14.1e100.net (142.251.37.238): icmp_seq=2 ttl=114 time=21.1 ms
^C
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 21.089/22.689/24.289/1.600 ms

# une machine du LAN1 peut joindre une machine du LAN2 (ping une adresse IP)

gabriel@clien1:~$ ping 10.6.2.11
PING 10.6.2.11 (10.6.2.11) 56(84) bytes of data.
64 bytes from 10.6.2.11: icmp_seq=1 ttl=64 time=0.475 ms
64 bytes from 10.6.2.11: icmp_seq=2 ttl=64 time=1.13 ms
^C
--- 10.6.2.11 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1049ms
rtt min/avg/max/mdev = 0.475/0.804/1.133/0.329 ms


2) client
   ## ☀️ Prouvez que...
   ### le client a bien récupéré une adresse IP en DHCP ###

gabriel@Client1:~$ ip a
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:81:19:a3 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.40/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s3
       valid_lft 42766sec preferred_lft 42766sec

   ### vous avez bien 1.1.1.1 en DNS

gabriel@Client1:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 1.1.1.1
       DNS Servers: 1.1.1.1

   ### vous avez bien la bonne passerelle indiquée

gabriel@Client1:~$ ip route show
default via 10.6.1.253 dev enp0s3 proto dhcp src 10.6.1.40 metric 100
1.1.1.1 via 10.6.1.253 dev enp0s3 proto dhcp src 10.6.1.40 metric 100
10.6.1.0/24 dev enp0s3 proto kernel scope link src 10.6.1.40 metric 100
10.6.1.253 dev enp0s3 proto dhcp scope link src 10.6.1.40 metric 100

   ### que ça ping un nom de domaine public sans problème magueule

gabriel@Client1:~$ ping -c 4 google.com
PING google.com (142.251.37.238) 56(84) bytes of data.
64 bytes from mrs09s16-in-f14.1e100.net (142.251.37.238): icmp_seq=2 ttl=114 time=20.6 ms
64 bytes from mrs09s16-in-f14.1e100.net (142.251.37.238): icmp_seq=4 ttl=114 time=42.8 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 2 received, 50% packet loss, time 3055ms
rtt min/avg/max/mdev = 20.599/31.721/42.844/11.122 ms


gabriel@Client1:~$ ping 10.6.2.11
PING 10.6.2.11 (10.6.2.11) 56(84) bytes of data.
64 bytes from 10.6.2.11: icmp_seq=2 ttl=63 time=1.14 ms
64 bytes from 10.6.2.11: icmp_seq=4 ttl=63 time=0.958 ms
64 bytes from 10.6.2.11: icmp_seq=6 ttl=63 time=0.744 ms
^C
--- 10.6.2.11 ping statistics ---
6 packets transmitted, 3 received, 50% packet loss, time 5134ms
rtt min/avg/max/mdev = 0.744/0.947/1.139/0.161 ms



[root@web ~]# ping -c 4 google.com
PING google.com (172.217.19.142) 56(84) bytes of data.
64 bytes from par03s12-in-f142.1e100.net (172.217.19.142): icmp_seq=1 ttl=114 time=25.2 ms
64 bytes from par03s12-in-f142.1e100.net (172.217.19.142): icmp_seq=2 ttl=114 time=22.4 ms
^C
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 22.382/23.806/25.231/1.424 ms


gabriel@Client1:~$ ping -c 4 google.com
PING google.com (172.217.19.142) 56(84) bytes of data.
64 bytes from par03s12-in-f142.1e100.net (172.217.19.142): icmp_seq=2 ttl=114 time=21.7 ms
64 bytes from par03s12-in-f142.1e100.net (172.217.19.142): icmp_seq=3 ttl=114 time=23.4 ms
64 bytes from par03s12-in-f142.1e100.net (172.217.19.142): icmp_seq=4 ttl=114 time=22.7 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 3 received, 25% packet loss, time 3018ms
rtt min/avg/max/mdev = 21.702/22.585/23.402/0.695 ms

### 1. Serveur Web

## ☀️ Déterminer sur quel port écoute le serveur NGINX

[root@web ~]# sudo ss -lnpt
State       Recv-Q      Send-Q           Local Address:Port            Peer Address:Port      Process
LISTEN      0           128                    0.0.0.0:22                   0.0.0.0:*          users:(("sshd",pid=720,fd=3))
LISTEN      0           511                    0.0.0.0:80                   0.0.0.0:*          users:(("nginx",pid=1680,fd=6),("nginx",pid=1679,fd=6))
LISTEN      0           128                       [::]:22                      [::]:*          users:(("sshd",pid=720,fd=4))
LISTEN      0           511                       [::]:80                      [::]:*          users:(("nginx",pid=1680,fd=7),("nginx",pid=1679,fd=7))


[root@web ~]#  sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1680,fd=6),("nginx",pid=1679,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1680,fd=7),("nginx",pid=1679,fd=7))

## ☀️ Ouvrir ce port dans le firewall

[root@web ~]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8 enp0s9
  sources:
  services: cockpit dhcpv6-client http https ssh
  ports:
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:


# ☀️ Visitez le site web !

gabriel@Client1:~$ curl http://10.6.2.11
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/

## 2.tp DNS
### ☀️ Déterminer sur quel(s) port(s) écoute le service BIND9
[root@dns ~]# sudo ss -lnpt
LISTEN    0         10                 127.0.0.1:53                0.0.0.0:*        users:(("named",pid=2100,fd=22))
LISTEN    0         10                 10.0.4.15:53                0.0.0.0:*        users:(("named",pid=2100,fd=27))
LISTEN    0         10                 10.6.2.12:53                0.0.0.0:*        users:(("named",pid=2100,fd=25))
LISTEN    0         10                     [::1]:53                   [::]:*        users:(("named",pid=2100,fd=29))


# ☀️ Ouvrir ce(s) port(s) dans le firewall
[root@dns ~]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8 enp0s9
  sources:
  services: cockpit dhcpv6-client dns ssh
  ports:
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:


# ☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps

[root@dns ~]# dig web.tp6.b1 @10.6.2.12
;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

[root@dns ~]# dig dns.tp6.b1 @10.6.2.12
;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.2.12

[root@dns ~]# dig ynov.com @10.6.2.12

;; ANSWER SECTION:
ynov.com.               300     IN      A       104.26.10.233
ynov.com.               300     IN      A       172.67.74.226
ynov.com.               300     IN      A       104.26.11.233


[root@dns ~]# dig -x 10.6.2.11 @10.6.2.12
;; ANSWER SECTION:
11.2.6.10.in-addr.arpa. 86400   IN      PTR     web.tp6.b1.



[root@dns ~]# dig -x 10.6.2.12 @10.6.2.12
;; ANSWER SECTION:
12.2.6.10.in-addr.arpa. 86400   IN      PTR     dns.tp6.b1.


### ☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1

root@Client1:~# nslookup web.tp.b1
^C
root@Client1:~# nslookup web.tp6.b1
Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
Name:   web.tp6.b1
Address: 10.6.2.11

## ☀️ Capturez une requête DNS et la réponse de votre serveur

-dns_capture.pcap(j'avais déjà effacé la vm client1 donc je l'ai fait avec la vm client2)

### 3. Serveur DHCP

## ☀️ Créez un nouveau client client2.tp6.b1 vitefé

root@Client2:~# ip a

```3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:cb:83:e8 brd ff:ff:ff:ff:ff:ff
    inet 10.6.2.37/24 brd 10.6.2.255 scope global dynamic noprefixroute enp0s8
       valid_lft 42528sec preferred_lft 42528sec
    inet6 fe80::a00:27ff:fecb:83e8/64 scope link
       valid_lft forever preferred_lft forever
root@Client2:~# resolvectl```

```
Link 3 (enp0s8)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS
                    DNSSEC=no/unsupported
Current DNS Server: 10.6.2.12
       DNS Servers: 10.6.2.12


root@Client2:~# curl http://web.tp6.b1
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/```