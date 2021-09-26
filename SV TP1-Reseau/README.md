# 1.Affichage d'informations sur la pile TCP/IP locale
### En ligne de commandes
#### Afficher les infos des cartes réseau de votre pc
*nom, adresse Mac et adresse IP de l'interface Wifi*
```
ifconfig
wlp4s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.33.3.133  netmask 255.255.252.0  broadcast 10.33.3.255
        inet6 fe80::e79:2809:6f7b:d670  prefixlen 64  scopeid 0x20<link>
        ether f8:94:c2:2e:59:00  txqueuelen 1000  (Ethernet)
        RX packets 40725  bytes 33838606 (33.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 26184  bytes 5205032 (5.2 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


```
*nom, adresse Mac et adresse IP de l'interface Ethernet*
```
ifconfig
enp0s31f6: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 54:e1:ad:d4:c4:62  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 16  memory 0xec200000-ec220000  
```
*Affichez votre Gateway*
```
ip route show
default via 10.33.3.253 dev wlp4s0 proto dhcp metric 600 
10.33.0.0/22 dev wlp4s0 proto kernel scope link src 10.33.3.133 metric 600 
169.254.0.0/16 dev wlp4s0 scope link metric 1000 

```
### En graphique (GUI : Graphical User Interface)
#### Trouvez comment afficher les informations sur une carte IP (change selon l'OS)
*trouvez l'IP, la MAC et la gateway pour l'interface WiFi de votre PC*

![](/img/Screen1.png)

* à quoi sert la gateway dans le réseau d'YNOV ?*
```
La gateway ou passerelle sert à communiquer avec d'autre machines dans un réseau distant
```
# 2.Modifications des informations
### A.Modification d'adresse IP (part 1)

![](/img/Screen2.png)

```
Il est possible de perdre son acces à internet car  il peux avoir plusieurs machine avec la même IP donc un souci de compatibilité
```
### B.Table ARP
*depuis la ligne de commande, afficher la table ARP*
``` 
arp
Address                  HWtype  HWaddress           Flags Mask            Iface
10.33.2.97               ether   d8:12:65:b5:11:77   C                     wlp4s0
10.33.0.208              ether   70:66:55:c5:4e:29   C                     wlp4s0
10.33.0.24               ether   d8:12:65:b5:11:77   C                     wlp4s0
10.33.2.93               ether   d8:12:65:b5:11:77   C                     wlp4s0
_gateway                 ether   00:12:00:40:4c:bf   C                     wlp4s0
10.33.3.254              ether   00:0e:c4:cd:74:f5   C                     wlp4s0
10.33.3.17               ether   80:32:53:e2:78:04   C                     wlp4s0
```
*identifier l'adresse MAC de la passerelle de votre réseau, et expliquer comment vous avez repéré cette adresse MAC spécifiquement*
```
Les adresses MAC sont dans la colone HWadress (Hard Ware adresse) 
pour adresse physique je les distingue grace au nom de la 
colone mais aussi grace a leur formes de suite de nombres
séparés par un ":" deux nombre ou chiffre par deux
```
*envoyez des ping vers des IP du même réseau que vous. Lesquelles ? menfou, random. Envoyez des ping vers au moins 3-4 machines*
```
ATTENTION CETTE PARTIE DU TP EST FAITE CHEZ MOI
DONC LES ADRESSES CHANGES ET LA TABLE AUSSI.

ping 192.168.1.94
PING 192.168.1.94 (192.168.1.94) 56(84) bytes of data.
64 bytes from 192.168.1.94: icmp_seq=1 ttl=64 time=495 ms

ping 192.168.1.91
PING 192.168.1.91 (192.168.1.91) 56(84) bytes of data.
64 bytes from 192.168.1.91: icmp_seq=1 ttl=64 time=458 ms
64 bytes from 192.168.1.91: icmp_seq=2 ttl=64 time=4.54 ms
```
*Affichez votre table ARP*
```
arp
Address                  HWtype  HWaddress           Flags Mask            Iface
STB                      ether   e4:5d:51:a2:f3:44   C                     wlp4s0
box                      ether   cc:2d:1b:70:61:58   C                     wlp4s0
RedmiNote8Pro-RedmiN     ether   1c:cc:d6:f8:12:c6   C                     wlp4s0
POCOPHONEF1-POCOPHON     ether   62:25:6f:bf:5b:a8   C                     wlp4s0
```
*listez les adresses MAC associées aux adresses IP que vous avez pinglistez les adresses MAC associées aux adresses IP que vous avez pinglistez les adresses MAC associées aux adresses IP que vous avez ping*
```
L'adresse Mac liée à l'IP 192.168.1.91 (Redmi) est 1c:cc:d6:f8:12:c6 
L'adresse Mac liée à l'IP 192.168.1.94 (Pocophone) est 62:25:6f:bf:5b:a8 
```
### C.nmap
*Utilisez nmap pour scanner le réseau de votre carte WiFi et trouver une adresse IP libre*
```
nmap -sP 192.168.1.0/24
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-13 19:48 CEST
Nmap scan report for box (192.168.1.1)
Host is up (0.0032s latency).
Nmap scan report for X1-Carbon (192.168.1.65)
Host is up (0.000040s latency).
Nmap scan report for POCOPHONEF1-POCOPHON (192.168.1.94)
Host is up (0.031s latency).
Nmap done: 256 IP addresses (3 hosts up) scanned in 2.82 seconds
```
```
arp
Address                  HWtype  HWaddress           Flags Mask            Iface
STB                      ether   e4:5d:51:a2:f3:44   C                     wlp4s0
box                      ether   cc:2d:1b:70:61:58   C                     wlp4s0
POCOPHONEF1-POCOPHON     ether   62:25:6f:bf:5b:a8   C                     wlp4s0
```
### D.Modification de l'adresse IP PART 2
##### Modifiez de nouveau votre adresse IP vers une adresse IP que vous savez libre grâce à nmap
###### utilisez un ping scan sur le réseau YNOV
###### montrez moi la commande nmap et son résultat
```
ATTENTION CETTE PARTIE A ETE REPRISE A YNOV !

nmap -sP 10.33.0.0/22
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-16 14:22 CEST
[...]
Nmap scan report for 10.33.3.133
Host is up (0.00022s latency).
Nmap scan report for 10.33.3.160
Host is up (0.27s latency).
Nmap scan report for 10.33.3.161
Host is up (0.012s latency).
Nmap scan report for 10.33.3.187
Host is up (0.11s latency).
Nmap scan report for 10.33.3.219

[...]


```
``` 
Je choisi l'adresse 10.33.3.134 car elle est libre
```
###### configurez correctement votre gateway pour avoir accès à d'autres réseaux (utilisez toujours la gateway d'YNOV)

![](/img/Screen3.png)

###### prouvez en une suite de commande que vous avez bien l'IP choisie, que votre passerelle est bien définie, et que vous avez un accès internet
```
 ip a
[...]
wlp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether f8:94:c2:2e:59:00 brd ff:ff:ff:ff:ff:ff
    inet 10.33.3.134/22 brd 10.33.3.255 scope global noprefixroute wlp4s0
       valid_lft forever preferred_lft forever
    inet6 fe80::e850:4748:36fc:4b65/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```
```
ping google.com
PING google.com (216.58.214.174) 56(84) bytes of data.
64 bytes from mad01s26-in-f14.1e100.net (216.58.214.174): icmp_seq=1 ttl=114 time=29.7 ms
64 bytes from mad01s26-in-f14.1e100.net (216.58.214.174): icmp_seq=2 ttl=114 time=19.5 ms
64 bytes from mad01s26-in-f14.1e100.net (216.58.214.174): icmp_seq=3 ttl=114 time=21.5 ms
^C
--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 19.498/23.572/29.703/4.412 ms
```
```
ping 10.33.0.31
PING 10.33.0.31 (10.33.0.31) 56(84) bytes of data.
64 bytes from 10.33.0.31: icmp_seq=1 ttl=64 time=1022 ms
64 bytes from 10.33.0.31: icmp_seq=2 ttl=64 time=17.6 ms
64 bytes from 10.33.0.31: icmp_seq=3 ttl=64 time=821 ms
^C
--- 10.33.0.31 ping statistics ---
4 packets transmitted, 3 received, 25% packet loss, time 3007ms
rtt min/avg/max/mdev = 17.642/620.263/1021.937/433.925 ms, pipe 2
```
## II. Exploration locale en duo
### 1. Prérequis
###### deux PCs avec ports RJ45
###### un câble RJ45
###### firewalls désactivés sur les deux PCs
### 2. Câblage
### Création du réseau (oupa)
### 3. Modification d'adresse IP
#### Si vos PCs ont un port RJ45 alors y'a une carte réseau Ethernet associée :
##### modifiez l'IP des deux machines pour qu'elles soient dans le même réseau
###### choisissez une IP qui commence par "192.168"
###### utilisez un /30 (que deux IP disponibles)
```
Nous allons prendre les IP 192.168.0.1 et 192.168.0.2(moi) avec un mask 255.255.252.0
```
![](/img/Screen4.png)

##### vérifiez à l'aide de commandes que vos changements ont pris effet
```
ip a
[...]
4: enx000ec6eee95e: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0e:c6:ee:e9:5e brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.2/22 brd 192.168.3.255 scope global noprefixroute enx000ec6eee95e
       valid_lft forever preferred_lft forever
    inet6 fe80::bbb0:6332:936d:13e5/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever

```
##### utilisez ping pour tester la connectivité entre les deux machines
```
ping 192.168.0.1
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=0.544 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=0.666 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=64 time=0.689 ms
^C
--- 192.168.0.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2030ms
rtt min/avg/max/mdev = 0.544/0.633/0.689/0.063 ms

```
##### affichez et consultez votre table ARP
```
ping 192.168.0.1
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=0.544 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=0.666 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=64 time=0.689 ms
^C
--- 192.168.0.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2030ms
rtt min/avg/max/mdev = 0.544/0.633/0.689/0.063 ms
```
### 4. Utilisation d'un des deux comme gateway
##### vos PCs ont deux cartes avec des adresses IP actuellement
##### la carte WiFi, elle permet notamment d'aller sur internet, grâce au réseau YNOV
##### la carte Ethernet, qui permet actuellement de joindre votre coéquipier, grâce au réseau que vous avez créé :)
##### Vous allez désactiver Internet sur une des deux machines, et vous servir de l'autre machine pour accéder à internet.
##### pour ce faiiiiiire :
###### désactivez l'interface WiFi sur l'un des deux postes
```
ip a
[...]
2: enp0s31f6: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 54:e1:ad:d4:c4:62 brd ff:ff:ff:ff:ff:ff
3: wlp4s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noqueue state DOWN group default qlen 1000
    link/ether f8:94:c2:2e:59:00 brd ff:ff:ff:ff:ff:ff
4: enx000ec6eee95e: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0e:c6:ee:e9:5e brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.2/22 brd 192.168.3.255 scope global noprefixroute enx000ec6eee95e
       valid_lft forever preferred_lft forever
    inet6 fe80::bbb0:6332:936d:13e5/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever

```
###### s'assurer de la bonne connectivité entre les deux PCs à travers le câble RJ45
```
 ping 192.168.0.1
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=0.622 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=0.556 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=64 time=0.500 ms
^C
--- 192.168.0.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2052ms
rtt min/avg/max/mdev = 0.500/0.559/0.622/0.049 ms
```
##### sur le PC qui n'a plus internet
###### sur la carte Ethernet, définir comme passerelle l'adresse IP de l'autre PC

![](/img/Screen5.png)

##### sur le PC qui a toujours internet
###### our tester la connectivité à internet on fait souvent des requêtes simples vers un serveur internet connu encore une fois, un ping vers un DNS connu comme 1.1.1.1 ou 8.8.8.8 c'est parfait
```
 ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=57 time=17.1 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=57 time=18.4 ms
^C
--- 1.1.1.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 17.102/17.734/18.367/0.632 ms
```
######  utiliser un traceroute ou tracert pour bien voir que les requêtes passent par la passerelle choisie (l'autre le PC)
```
Etant le pc qui recois internet voici mon traceroute
traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
 1  josephdev (192.168.0.1)  0.471 ms  0.432 ms  0.416 ms
 2  _gateway (10.33.3.253)  16.758 ms  16.977 ms  17.375 ms
 3  10.33.10.254 (10.33.10.254)  8.347 ms  8.331 ms  8.569 ms
 4  reverse.completel.net (92.103.174.137)  8.810 ms  8.795 ms  9.636 ms
 5  92.103.120.182 (92.103.120.182)  10.268 ms  10.546 ms  10.534 ms
 6  172.19.130.117 (172.19.130.117)  20.537 ms  17.016 ms  20.538 ms
 7  46.218.128.74 (46.218.128.74)  17.041 ms  17.121 ms  16.602 ms
 8  equinix-paris.cloudflare.com (195.42.144.143)  17.559 ms  17.033 ms  20.712 ms
 9  one.one.one.one (1.1.1.1)  18.764 ms  19.472 ms  18.659 ms
```
### 5. Petit chat privé
#####  sur le PC serveur avec par exemple l'IP 192.168.1.1
```
adam@X1-Carbon:~$ nc -l -p 8888
```
```adam@X1-Carbon:~$ nc -l -p 8888
test1
test
PC Joseph : Bonjour
pc Adam : Bonjour
```
##### pour aller un peu plus loin
###### le serveur peut préciser sur quelle IP écouter, et ne pas répondre sur les autres
###### par exemple, on écoute sur l'interface Ethernet, mais pas sur la WiFI
```
nc -p 9999 -s 192.168.0.2 -l
test
PC Joseph sur co privée
```
###### on peut aussi accepter uniquement les connexions internes à la machine en écoutant sur 127.0.0.1
```
nc -p 9999 -s 127.0.0.1 -l
ddd
```
### 6. Firewall
###### Toujours par 2.
##### Le but est de configurer votre firewall plutôt que de le désactiver
```
ATTENTION CETTE PARTIE A ETE FAITE CHEZ MOI AVEC MON DEUXIEME PC !
J'ai du refaire la partie partage de connection via un calbe eternet.
```
###### Activez votre firewall
```
sudo ufw enable
Firewall is active and enabled on system startup
```
![](/img/Screen6.png)

#####  Autoriser les ping
###### configurer le firewall de votre OS pour accepter le ping
###### aidez vous d'internet
###### on rentrera dans l'explication dans un prochain cours mais sachez que ping envoie un message ICMP de type 8 (demande d'ECHO) et reçoit un message ICMP de type 0 (réponse d'écho) en retour
```
sudo cat /etc/ufw/before.rules
# ok icmp codes for INPUT
-A ufw-before-input -p icmp --icmp-type destination-unreachable -j ACCEPT
-A ufw-before-input -p icmp --icmp-type time-exceeded -j ACCEPT
-A ufw-before-input -p icmp --icmp-type parameter-problem -j ACCEPT
-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT
```
```
POUR LE PC 2
netsh advfirewall firewall add rule name="ICMP Allow incoming V4 echo request" protocol=icmpv4:8,any dir=in action=allow
```
*PREUVE QUE LE PING FONCTIONNE PC 1*
```
ping 192.168.0.1
PING 192.168.0.1 (192.168.0.1) 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=64 time=0.846 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=64 time=1.30 ms
^C
--- 192.168.0.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1028ms
rtt min/avg/max/mdev = 0.846/1.071/1.297/0.225 ms
```

![](/img/Screen7.png)

#####  Autoriser le traffic sur le port qu'utilise nc
###### on parle bien d'ouverture de port TCP et/ou UDP
###### on ne parle PAS d'autoriser le programme nc
###### choisissez arbitrairement un port entre 1024 et 20000
###### vous utiliserez ce port pour communiquer avec netcat par groupe de 2 toujours
###### le firewall du PC serveur devra avoir un firewall activé et un netcat qui fonctionne
```
sudo ufw allow 10000/udp
[sudo] password for adam: 
Rule added
Rule added (v6)
```
![](/img/Screen8.png)
![](/img/Screen9.png)

```
 nc 192.168.0.1 10000
coucou

```
![](/img/Screen10.png)

### III. Manipulations d'autres outils/protocoles côté client
#### 1. DHCP
##### Exploration du DHCP, depuis votre PC
###### afficher l'adresse IP du serveur DHCP du réseau WiFi YNOV
```
sudo nmap --script broadcast-dhcp-discover -e wlp4s0
[sudo] password for adam: 
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-19 22:19 CEST
Pre-scan script results:
| broadcast-dhcp-discover: 
|   Response 1 of 1: 
|     IP Offered: 192.168.1.93
|     DHCP Message Type: DHCPOFFER
|     Server Identifier: 192.168.1.1
|     IP Address Lease Time: 2m00s
|     Renewal Time Value: 1m00s
|     Rebinding Time Value: 1m45s
|     Broadcast Address: 192.168.1.255
|     NTP Servers: 192.168.1.1
|     Domain Name Server: 192.168.1.1
|     Router: 192.168.1.1
|_    Subnet Mask: 255.255.255.0
WARNING: No targets were specified, so 0 hosts scanned.
Nmap done: 0 IP addresses (0 hosts up) scanned in 2.74 seconds
```
###### cette adresse a une durée de vie limitée. C'est le principe du bail DHCP (ou DHCP lease). Trouver la date d'expiration de votre bail DHCP
###### vous pouvez vous renseigner un peu sur le fonctionnement de DHCP dans les grandes lignes. On aura sûrement un cours là dessus :)
```
sudo nmap --script broadcast-dhcp-discover -e wlp4s0
[sudo] password for adam: 
Sorry, try again.
[sudo] password for adam: 
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-19 22:54 CEST
Pre-scan script results:
| broadcast-dhcp-discover: 
|   Response 1 of 1: 
|     IP Offered: 192.168.1.93
|     DHCP Message Type: DHCPOFFER
|     Server Identifier: 192.168.1.1
|     IP Address Lease Time: 2m00s
|     Renewal Time Value: 1m00s
|     Rebinding Time Value: 1m45s
|     Broadcast Address: 192.168.1.255
|     NTP Servers: 192.168.1.1
|     Domain Name Server: 192.168.1.1
|     Router: 192.168.1.1
|_    Subnet Mask: 255.255.255.0
WARNING: No targets were specified, so 0 hosts scanned.
Nmap done: 0 IP addresses (0 hosts up) scanned in 2.57 seconds
```
### 2. DNS
#### trouver l'adresse IP du serveur DNS que connaît votre ordinateur
```
dig ynov.com

; <<>> DiG 9.16.1-Ubuntu <<>> ynov.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5603
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;ynov.com.			IN	A

;; ANSWER SECTION:
ynov.com.		10800	IN	A	92.243.16.143

;; Query time: 20 msec
;; SERVER: 127.0.0.53#53(127.0.0.53)
;; WHEN: dim. sept. 19 23:01:35 CEST 2021
;; MSG SIZE  rcvd: 53
```
#### utiliser, en ligne de commande l'outil nslookup (Windows, MacOS) ou dig (GNU/Linux, MacOS) pour faire des requêtes DNS à la main
##### faites un lookup (lookup = "dis moi à quelle IP se trouve tel nom de domaine")
###### pour google.com
```
nslookup google.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	google.com
Address: 216.58.215.46
Name:	google.com
Address: 2a00:1450:4007:80d::200e
```
```
pour ynov.com
nslookup ynov.com
Server:		127.0.0.53
Address:	127.0.0.53#53

Non-authoritative answer:
Name:	ynov.com
Address: 92.243.16.143
```
###### interpréter les résultats de ces commandes
```
On peux voir sur les deux premières lignes l'adresse dur serveur DNS.
Sur la ligne Name: on peux voir le nom de domaine qui est recherché
et en dessous son adresse IP (il y a une IPV6 en plus pour google.com)
```
###### déterminer l'adresse IP du serveur à qui vous venez d'effectuer ces requêtes
```
L'adresse IP du serveur avec laquel j'ai fait des requettes est 127.0.0.53
```
###### faites un reverse lookup (= "dis moi si tu connais un nom de domaine pour telle IP")
```
pour l'adresse 78.74.21.21
nslookup 78.74.21.21
21.21.74.78.in-addr.arpa	name = host-78-74-21-21.homerun.telia.com.

Authoritative answers can be found from:
```
```
pour l'adresse 92.146.54.88
nslookup 92.146.54.88
88.54.146.92.in-addr.arpa	
name =apoitiers654-1-167-88.w92-146.abo.wanadoo.fr.

Authoritative answers can be found from:

```
###### interpréter les résultats
```
On peux voir les noms de domaines qui sont reliés aux adresses IP
```
### IV. Wireshark
#####  utilisez le pour observer les trames qui circulent entre vos deux carte Ethernet. Mettez en évidence :
###### un ping entre vous et la passerelle
```
On peux voir que c'est un ping grace au protocol ICMP
```
![](/img/Screen11.png)

###### un netcat entre vous et votre mate, branché en RJ45
```
voici copment j'ai voulu faire la minupaltion.
J'ai pris soins de capturer sur la bonne carte réseau et de mettre un filtre
```
![](/img/Screen12.png)
###### une requête DNS. Identifiez dans la capture le serveur DNS à qui vous posez la question.
```
On peux voir les requettes DNS grace au filtre DNS
```
![](/img/Screen13.png)