### TP7 : On dit chiffrer pas crypter



### I. Setup
## II. Serveur Web


# 🌞 Lister les ports en écoute sur la machine

```
[root@webb gabriel]#  sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=35488,fd=6),("nginx",pid=35487,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=35488,fd=7),("nginx",pid=35487,fd=7))
```

# 🌞 Ouvrir le port dans le firewall de la machine

```
[root@webb gabriel]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client http https ssh
  ports:
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```


# 🌞 Vérifier que ça a pris effet

```
[root@webb gabriel]# ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=0.394 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=0.046 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.046/0.220/0.394/0.174 ms
```


```
gabriel@clienttp7:~$ curl http://sitedefou.tp7.b1
meow !
```

# 🌞 Capture tcp_http.pcap

-tcp_http.pcap

# 🌞 Voir la connexion établie

```
gabriel@clienttp7:~$ ss -t -a
ESTAB       0           0                         10.7.1.101:58478                    10.7.1.11:http
```

# 🌞 Lister les ports en écoute sur la machine

```
[root@webb gabriel]# sudo ss -lnpt | grep 443
LISTEN 0      511        10.7.1.11:443       0.0.0.0:*    users:(("nginx",pid=1340,fd=6),("nginx",pid=1339,fd=6))
```

# 🌞 Gérer le firewall

```
[root@webb gabriel]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client http https ssh
  ports: 443/tcp
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

# 🌞 Capture tcp_https.pcap

-tcp_https.pcap

#  Test test test analyyyze

```
root@clienttp7:~# curl https://sitedefou.tp7.b1
curl: (60) SSL certificate problem: self-signed certificate
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
root@clienttp7:~# curl https://sitedefou.tp7.b1 -k
meow !
```

# 🌞 Capture tcp_https.pcap

-tcp_https.pcap

## III. Serveur VPN

# 🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0

```
[root@vpnserv gabriel]# ip a
4: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```

# 🌞 Déterminer sur quel port écoute Wireguard

```
[root@vpnserv gabriel]# sudo ss -lnpu
State          Recv-Q         Send-Q                 Local Address:Port                  Peer Address:Port        Process
UNCONN         0              0                            0.0.0.0:51820                      0.0.0.0:*
```

# 🌞 Ouvrez ce port dans le firewall

```
[root@vpnserv gabriel]# sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8 wg0
```

# 🌞 Ping ping ping !

```
  root@clienttp7:~# ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=4.68 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=1.41 ms
^C
--- 10.7.200.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 1.410/3.043/4.677/1.633 ms
```

# 🌞 Capture ping1_vpn.pcap

-ping-vpn.pcap

# 🌞 Capture ping2_vpn.pcap

-ping1_vpn.pcap


# 🌞 Prouvez que vous avez toujours un accès internet

```
root@clienttp7:~# traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
 1  _gateway (10.7.1.254)  13.145 ms  13.295 ms  12.795 ms
 2  10.0.2.2 (10.0.2.2)  14.715 ms  14.560 ms  14.263 ms
 3  10.0.2.2 (10.0.2.2)  18.031 ms  17.564 ms  17.220 ms
```

# 🌞 Visitez le service Web à travers le VPN

```
[root@webb gabriel]# curl https://sitedefou.tp7.b1
curl: (60) SSL certificate problem: self-signed certificate
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
[root@webb gabriel]# curl https://sitedefou.tp7.b1 -k
meow !
```