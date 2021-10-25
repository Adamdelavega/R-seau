# TP4 : Vers un réseau d'entreprise

# I. Dumb switch

## 1. Topologie 1

## 2. Adressage topologie 1

| Node  | IP            |
|-------|---------------|
| `pc1` | `10.1.1.1/24` |
| `pc2` | `10.1.1.2/24` |


**Commençons simple**

- définissez les IPs statiques sur les deux VPCS
```
PC1> ip 10.1.1.1/24
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0
PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.1.1.1/24
GATEWAY     : 255.255.255.0
DNS         : 
MAC         : 00:50:79:66:68:00
LPORT       : 20004
RHOST:PORT  : 127.0.0.1:20005
MTU         : 1500


PC2> ip 10.1.1.2/24
Checking for duplicate address...
PC2 : 10.1.1.2 255.255.255.0
PC2> show ip

NAME        : PC2[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 255.255.255.0
DNS         : 
MAC         : 00:50:79:66:68:01
LPORT       : 20006
RHOST:PORT  : 127.0.0.1:20007
MTU         : 1500
```
- `ping` un VPCS depuis l'autre
```
PC1> ping 10.1.1.2

84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=6.629 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=1.945 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=4.602 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=13.538 ms

PC2> ping 10.1.1.1

84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=10.992 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=9.769 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=11.719 ms
84 bytes from 10.1.1.1 icmp_seq=4 ttl=64 time=10.297 ms
```

# II. VLAN

## 1. Topologie 2

## 2. Adressage topologie 2

| Node  | IP            | VLAN |
|-------|---------------|------|
| `pc1` | `10.1.1.1/24` | 10   |
| `pc2` | `10.1.1.2/24` | 10   |
| `pc3` | `10.1.1.3/24` | 20   |

### 3. Setup topologie 2

**Adressage**

- définissez les IPs statiques sur tous les VPCS
```
PC3> ip 10.1.1.3/24
Checking for duplicate address...
PC3 : 10.1.1.3 255.255.255.0
PC3> show ip

NAME        : PC3[1]
IP/MASK     : 10.1.1.3/24
GATEWAY     : 0.0.0.0
DNS         : 
MAC         : 00:50:79:66:68:02
LPORT       : 20042
RHOST:PORT  : 127.0.0.1:20043
MTU         : 1500

PC2> show ip

NAME        : PC2[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 0.0.0.0
DNS         : 
MAC         : 00:50:79:66:68:01
LPORT       : 20006
RHOST:PORT  : 127.0.0.1:20007
MTU         : 1500

PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.1.1.1/24
GATEWAY     : 0.0.0.0
DNS         : 
MAC         : 00:50:79:66:68:00
LPORT       : 20004
RHOST:PORT  : 127.0.0.1:20005
MTU         : 1500
```
- vérifiez avec des `ping` que tout le monde se ping

**PC1**
```
PC1> ping 10.1.1.2

84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=7.468 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=4.034 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=2.992 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=4.266 ms
PC1> ping 10.1.1.3

84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=6.620 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=3.913 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=5.464 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=3.100 ms
```
**PC2**
```
PC2> ping 10.1.1.1

84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=10.092 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=12.701 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=10.425 ms
84 bytes from 10.1.1.1 icmp_seq=4 ttl=64 time=9.074 ms
PC2> ping 10.1.1.3

84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=6.260 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=5.757 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=3.182 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=3.233 ms
```
**PC3**
```
PC3> ping 10.1.1.1

84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=8.961 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=10.973 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=7.154 ms
84 bytes from 10.1.1.1 icmp_seq=4 ttl=64 time=9.724 ms
PC3> ping 10.1.1.2

84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=8.711 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=8.435 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=7.487 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=8.736 ms
```

**Configuration des VLANs**

- référez-vous [à la section VLAN du mémo Cisco](../../cours/memo/memo_cisco.md#8-vlan)
- déclaration des VLANs sur le switch `sw1`
- ajout des ports du switches dans le bon VLAN (voir [le tableau d'adressage de la topo 2 juste au dessus](#2-adressage-topologie-2))
  - ici, tous les ports sont en mode *access* : ils pointent vers des clients du réseau

**Déclaration des Vlans**
```
Switch>en
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#vlan 10
Switch(config-vlan)#name admins
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name guests
Switch(config-vlan)#exit
```
**Vlans pour PC1 et PC2**
```
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#interface GigabitEthernet0/0
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#exit
Switch(config)#interface GigabitEthernet0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#exit
```
**Vlan pour PC3**
```
Switch(config)#interface GigabitEthernet0/2
Switch(config-if)#switchport mode access      
Switch(config-if)#switchport access vlan 20   
Switch(config-if)#exit
```

**Vérif**

- `pc1` et `pc2` doivent toujours pouvoir se ping
- `pc3` ne ping plus personne
**PC1 et PC2**
```
PC1> ping 10.1.1.2

84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=6.037 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=2.958 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=4.162 ms
PC1> ping 10.1.1.3

host (10.1.1.3) not reachable


PC2> ping 10.1.1.1

84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=12.244 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=8.299 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=9.636 ms
PC2> ping 10.1.1.3

host (10.1.1.3) not reachable
```
**PC3**
```
PC3> ping 10.1.1.1

host (10.1.1.1) not reachable

PC3> ping 10.1.1.2

host (10.1.1.2) not reachable
```

# III. Routing

## 1. Topologie 3

## 2. Adressage topologie 3

Les réseaux et leurs VLANs associés :

| Réseau    | Adresse       | VLAN associé |
|-----------|---------------|--------------|
| `clients` | `10.1.1.0/24` | 11           |
| `admins`  | `10.2.2.0/24` | 12           |
| `servers` | `10.3.3.0/24` | 13           |

L'adresse des machines au sein de ces réseaux :

| Node               | `clients`       | `admins`        | `servers`       |
|--------------------|-----------------|-----------------|-----------------|
| `pc1.clients.tp4`  | `10.1.1.1/24`   | x               | x               |
| `pc2.clients.tp4`  | `10.1.1.2/24`   | x               | x               |
| `adm1.admins.tp4`  | x               | `10.2.2.1/24`   | x               |
| `web1.servers.tp4` | x               | x               | `10.3.3.1/24`   |
| `r1`               | `10.1.1.254/24` | `10.2.2.254/24` | `10.3.3.254/24` |

## 3. Setup topologie 3

**Adressage**

- définissez les IPs statiques sur toutes les machines **sauf le *routeur***

**pc1**
```
PC1> show ip                  

NAME        : PC1[1]
IP/MASK     : 10.1.1.1/24
GATEWAY     : 0.0.0.0
DNS         : 
DOMAIN NAME : pc1.clients.tp4
MAC         : 00:50:79:66:68:00
LPORT       : 20006
RHOST:PORT  : 127.0.0.1:20007
MTU         : 1500
```
**pc2**
```
PC2> show ip                  

NAME        : PC2[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 0.0.0.0
DNS         : 
DOMAIN NAME : pc2.clients.tp4
MAC         : 00:50:79:66:68:01
LPORT       : 20004
RHOST:PORT  : 127.0.0.1:20005
MTU         : 1500
```

**adm1**
```
PC3> show ip

NAME        : PC3[1]
IP/MASK     : 10.2.2.1/24
GATEWAY     : 0.0.0.0
DNS         : 
DOMAIN NAME : adm1.admins.tp4
MAC         : 00:50:79:66:68:02
LPORT       : 20042
RHOST:PORT  : 127.0.0.1:20043
MTU         : 1500
```

**web1**
```
[adam@web1 ~]$ ip a
[...]
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:ba:e0:e7 brd ff:ff:ff:ff:ff:ff
    inet 10.3.3.1/24 brd 10.3.3.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:feba:e0e7/64 scope link 
[...]
[adam@web1 ~]$ cat /etc/hostname 
web1.server.tp4
[adam@web1 ~]$ 
```
**test ping**
```
PC1> ping 10.1.1.2

84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=6.703 ms

PC2> ping 10.1.1.1

84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=7.912 ms

adm1> ping 10.1.1.1

No gateway found
```
(adm1 ne ping pas, c'est normal pour l'instant)
```
[adam@web1 ~]$ ping 10.1.1.1
connect: Network is unreachable
[adam@web1 ~]$ 
```
(web1 ne ping pas c'est normal)

**Configuration des VLANs**

- référez-vous au [mémo Cisco](../../cours/memo/memo_cisco.md#8-vlan)
- déclaration des VLANs sur le switch `sw1`
- ajout des ports du switches dans le bon VLAN (voir [le tableau d'adressage de la topo 2 juste au dessus](#2-adressage-topologie-2))
- il faudra ajouter le port qui pointe vers le *routeur* comme un *trunk* : c'est un port entre deux équipements réseau (un *switch* et un *routeur*)

**Déclaration des Vlans**
```
Switch(config)#no vlan 10
Switch(config)#no vlan 20
Switch(config)#vlan 11
Switch(config-vlan)#name clients
Switch(config-vlan)#exit        
Switch(config)#vlan 12     
Switch(config-vlan)#name admins 
Switch(config-vlan)#exit
Switch(config)#vlan 13    
Switch(config-vlan)#name servers
Switch(config-vlan)#exit
```

**Assignation des Vlans**

**Vlan clients**

```
Switch(config)#interface GigabitEthernet0/0
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 11
Switch(config-if)#exit
Switch(config)#interface GigabitEthernet0/1
Switch(config-if)#switchport mode access      
Switch(config-if)#switchport access vlan 11   
Switch(config-if)#exit                                              
```
**Vlan admins**

```
Switch(config)#interface GigabitEthernet0/2
Switch(config-if)#switchport mode access      
Switch(config-if)#switchport access vlan 12   
Switch(config-if)#exit                        
```

**Vlan server**

```
Switch(config)#interface GigabitEthernet0/3
Switch(config-if)#switchport mode access      
Switch(config-if)#switchport access vlan 13   
Switch(config-if)#exit                        
```

**Mode trunk**

```
Switch(config)#interface GigabitEthernet1/0
Switch(config-if)#switchport trunk encapsulation dot1q
Switch(config-if)#switchport mode trunk
Switch(config-if)#switchport trunk allowed vlan add 11
Switch(config-if)#switchport trunk allowed vlan add 12
Switch(config-if)#switchport trunk allowed vlan add 13
Switch(config-if)#exit
Switch(config)#exit
Switch#show interface trunk

Port        Mode             Encapsulation  Status        Native vlan
Gi1/0       on               802.1q         trunking      1

Port        Vlans allowed on trunk
Gi1/0       1-4094

Port        Vlans allowed and active in management domain
Gi1/0       1,11-13

Port        Vlans in spanning tree forwarding state and not pruned
Gi1/0       1,11-13
Switch#
```

**Config du *routeur***

- attribuez ses IPs au *routeur*
  - 3 sous-interfaces, chacune avec son IP et un VLAN associé

```
R1(config)#interface FastEthernet0/0.11
R1(config-subif)#encapsulation dot1Q 11      
R1(config-subif)#ip addr 10.1.1.254 255.255.255.0
R1(config-subif)#exit
```
```
R1(config)#interface FastEthernet0/0.12
R1(config-subif)#encapsulation dot1Q 12        
R1(config-subif)#ip addr 10.2.2.254 255.255.255.0
R1(config-subif)#exit
```
```
R1(config)#interface FastEthernet0/0.13  
R1(config-subif)#encapsulation dot1Q 13        
R1(config-subif)#ip addr 10.3.3.254 255.255.255.0
R1(config-subif)#exit
```
```
R1(config)#interface fastEthernet 0/0       
R1(config-if)#no shut
R1(config-if)#
*Mar  1 00:11:00.343: %LINK-3-UPDOWN: Interface FastEthernet0/0, changed state to up
*Mar  1 00:11:01.343: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up
```

**Vérif**

- tout le monde doit pouvoir ping le routeur sur l'IP qui est dans son réseau
- en ajoutant une route vers les réseaux, ils peuvent se ping entre eux
  - ajoutez une route par défaut sur les VPCS
  - ajoutez une route par défaut sur la machine virtuelle
  - testez des `ping` entre les réseaux

**Ping**
```
PC1> ping 10.1.1.254

84 bytes from 10.1.1.254 icmp_seq=1 ttl=255 time=10.237 ms
84 bytes from 10.1.1.254 icmp_seq=2 ttl=255 time=11.027 ms

PC2> ping 10.1.1.254

84 bytes from 10.1.1.254 icmp_seq=1 ttl=255 time=16.775 ms
84 bytes from 10.1.1.254 icmp_seq=2 ttl=255 time=10.294 ms

adm1> ping 10.2.2.254

84 bytes from 10.2.2.254 icmp_seq=1 ttl=255 time=22.680 ms
84 bytes from 10.2.2.254 icmp_seq=2 ttl=255 time=16.718 ms

[adam@web1 ~]$ ping 10.3.3.254
PING 10.3.3.254 (10.3.3.254) 56(84) bytes of data.
64 bytes from 10.3.3.254: icmp_seq=1 ttl=255 time=29.7 ms
64 bytes from 10.3.3.254: icmp_seq=2 ttl=255 time=11.4 ms
```

**Ajout des routes**
```
PC1> ip 10.1.1.1/24 10.1.1.254
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0 gateway 10.1.1.254
PC1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC1    10.1.1.1/24          10.1.1.254        00:50:79:66:68:00  20006  127.0.0.1:20007
       fe80::250:79ff:fe66:6800/64

PC2> ip 10.1.1.2/24 10.1.1.254
Checking for duplicate address...
PC2 : 10.1.1.2 255.255.255.0 gateway 10.1.1.254

PC2> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC2    10.1.1.2/24          10.1.1.254        00:50:79:66:68:01  20004  127.0.0.1:20005
       fe80::250:79ff:fe66:6801/64

PC3> ip 10.2.2.1/24 10.2.2.254
Checking for duplicate address...
PC3 : 10.2.2.1 255.255.255.0 gateway 10.2.2.254

PC3> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
PC3    10.2.2.1/24          10.2.2.254        00:50:79:66:68:02  20042  127.0.0.1:20043
       fe80::250:79ff:fe66:6802/64

[adam@web1 ~]$ sudo cat /etc/sysconfig/network-scripts/ifcfg-enp0s3
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
NAME=enp0s3
UUID=38ad34d6-6f1e-417c-b804-25ccdd9deff3
DEVICE=enp0s3
ONBOOT=yes
IPADDR=10.3.3.1
NETMASK=255.255.255.0
GATEWAY=10.3.3.254
```

**Ping**
```
PC1> ping 10.2.2.1

84 bytes from 10.2.2.1 icmp_seq=1 ttl=63 time=27.191 ms
84 bytes from 10.2.2.1 icmp_seq=2 ttl=63 time=22.526 ms
^C

PC1> ping 10.3.3.1

84 bytes from 10.3.3.1 icmp_seq=1 ttl=63 time=26.413 ms
84 bytes from 10.3.3.1 icmp_seq=2 ttl=63 time=19.317 ms
^C
```
```
PC2> ping 10.2.2.1

84 bytes from 10.2.2.1 icmp_seq=1 ttl=63 time=29.859 ms
84 bytes from 10.2.2.1 icmp_seq=2 ttl=63 time=26.430 ms

PC2> ping 10.3.3.1

84 bytes from 10.3.3.1 icmp_seq=1 ttl=63 time=44.806 ms
84 bytes from 10.3.3.1 icmp_seq=2 ttl=63 time=17.911 ms
```
```
PC3> ping 10.1.1.1

84 bytes from 10.1.1.1 icmp_seq=1 ttl=63 time=31.047 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=63 time=20.791 ms
^C
PC3> ping 10.1.1.2

84 bytes from 10.1.1.2 icmp_seq=1 ttl=63 time=21.329 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=63 time=39.033 ms
^C
PC3> ping 10.3.3.1  

84 bytes from 10.3.3.1 icmp_seq=1 ttl=63 time=20.682 ms
84 bytes from 10.3.3.1 icmp_seq=2 ttl=63 time=35.316 ms
^C
```
```
[adam@web1 ~]$ ping 10.1.1.1
PING 10.1.1.1 (10.1.1.1) 56(84) bytes of data.
64 bytes from 10.1.1.1: icmp_seq=1 ttl=63 time=41.6 ms
64 bytes from 10.1.1.1: icmp_seq=2 ttl=63 time=22.5 ms
^C
--- 10.1.1.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 22.494/32.051/41.609/9.559 ms
[adam@web1 ~]$ ping 10.1.1.2
PING 10.1.1.2 (10.1.1.2) 56(84) bytes of data.
64 bytes from 10.1.1.2: icmp_seq=1 ttl=63 time=41.10 ms
64 bytes from 10.1.1.2: icmp_seq=2 ttl=63 time=24.7 ms
^C
--- 10.1.1.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1000ms
rtt min/avg/max/mdev = 24.700/33.331/41.963/8.633 ms
[adam@web1 ~]$ ping 10.2.2.1
PING 10.2.2.1 (10.2.2.1) 56(84) bytes of data.
64 bytes from 10.2.2.1: icmp_seq=1 ttl=63 time=34.1 ms
64 bytes from 10.2.2.1: icmp_seq=2 ttl=63 time=19.2 ms
^C
--- 10.2.2.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 19.197/26.643/34.089/7.446 ms
```

# IV. NAT

## 1. Topologie 4

## 2. Adressage topologie 4

Les réseaux et leurs VLANs associés :

| Réseau    | Adresse       | VLAN associé |
|-----------|---------------|--------------|
| `clients` | `10.1.1.0/24` | 11           |
| `admins`  | `10.2.2.0/24` | 12           |
| `servers` | `10.3.3.0/24` | 13           |

L'adresse des machines au sein de ces réseaux :

| Node               | `clients`       | `admins`        | `servers`       |
|--------------------|-----------------|-----------------|-----------------|
| `pc1.clients.tp4`  | `10.1.1.1/24`   | x               | x               |
| `pc2.clients.tp4`  | `10.1.1.2/24`   | x               | x               |
| `adm1.admins.tp4`  | x               | `10.2.2.1/24`   | x               |
| `web1.servers.tp4` | x               | x               | `10.3.3.1/24`   |
| `r1`               | `10.1.1.254/24` | `10.2.2.254/24` | `10.3.3.254/24` |

## 3. Setup topologie 4

**Ajoutez le noeud Cloud à la topo**

- branchez à `eth1` côté Cloud
- côté routeur, il faudra récupérer un IP en DHCP (voir [le mémo Cisco](../../cours/memo/memo_cisco.md))
- vous devriez pouvoir `ping 1.1.1.1`
```
R1(config)#interface FastEthernet1/0       
R1(config-if)#ip address dhcp
R1(config-if)#no shut
R1(config-if)#exit

R1#show ip int br
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            unassigned      YES unset  up                    up      
FastEthernet0/0.11         10.1.1.254      YES manual up                    up      
FastEthernet0/0.12         10.2.2.254      YES manual up                    up      
FastEthernet0/0.13         10.3.3.254      YES manual up                    up      
FastEthernet1/0            10.0.3.16       YES DHCP   up                    up      
FastEthernet2/0            unassigned      YES unset  administratively down down    
FastEthernet3/0            unassigned      YES unset  administratively down down 
```
```
PC1> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=61 time=33.378 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=61 time=36.992 ms

PC2> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=61 time=30.518 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=61 time=29.168 ms

PC3> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=61 time=33.710 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=61 time=29.804 ms

[adam@web1 ~]$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=61 time=33.8 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=61 time=28.1 ms
```

**Configurez le NAT**

- référez-vous [à la section NAT du mémo Cisco](../../cours/memo/memo_cisco.md#7-configuration-dun-nat-simple)
```
R1(config)#interface fastEthernet 0/0
R1(config-if)#ip nat inside

*Mar  1 00:53:35.159: %LINEPROTO-5-UPDOWN: Line protocol on Interface NVI0, changed state to up
R1(config-if)#exit
R1(config)#interface fastEthernet 1/0
R1(config-if)#ip nat outside            
R1(config-if)#exit
```

**Test**

- ajoutez une route par défaut (si c'est pas déjà fait)
  - sur les VPCS
  - sur la machine Linux
- configurez l'utilisation d'un DNS
  - sur les VPCS
  - sur la machine Linux
- vérifiez un `ping` vers un nom de domaine

**web1**
```
[adam@web1 ~]$ sudo cat /etc/sysconfig/network-scripts/ifcfg-enp0s3
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
NAME=enp0s3
UUID=38ad34d6-6f1e-417c-b804-25ccdd9deff3
DEVICE=enp0s3
ONBOOT=yes
IPADDR=10.3.3.1
NETMASK=255.255.255.0
GATEWAY=10.3.3.254
DNS1=1.1.1.1

[adam@web1 ~]$ ping google.com
PING google.com (142.250.201.174) 56(84) bytes of data.
64 bytes from par21s23-in-f14.1e100.net (142.250.201.174): icmp_seq=1 ttl=61 time=37.4 ms
64 bytes from par21s23-in-f14.1e100.net (142.250.201.174): icmp_seq=2 ttl=61 time=26.6 ms
```

**pc1 et pc2**
```
PC1> ping google.com
google.com resolved to 172.217.19.238

84 bytes from 172.217.19.238 icmp_seq=1 ttl=61 time=28.924 ms
84 bytes from 172.217.19.238 icmp_seq=2 ttl=61 time=31.487 ms

PC2> ip dns 1.1.1.1

PC2> ping google.com
google.com resolved to 172.217.19.238

84 bytes from 172.217.19.238 icmp_seq=1 ttl=61 time=32.635 ms
84 bytes from 172.217.19.238 icmp_seq=2 ttl=61 time=39.774 ms
```

**adm1**
```
PC3> ip dns 1.1.1.1

PC3> ping google.com
google.com resolved to 172.217.19.238

84 bytes from 172.217.19.238 icmp_seq=1 ttl=61 time=29.099 ms
84 bytes from 172.217.19.238 icmp_seq=2 ttl=61 time=36.558 ms
```

# V. Add a building

## 1. Topologie 5

## 2. Adressage topologie 5

Les réseaux et leurs VLANs associés :

| Réseau    | Adresse       | VLAN associé |
|-----------|---------------|--------------|
| `clients` | `10.1.1.0/24` | 11           |
| `admins`  | `10.2.2.0/24` | 12           |
| `servers` | `10.3.3.0/24` | 13           |

L'adresse des machines au sein de ces réseaux :

| Node                | `clients`       | `admins`        | `servers`       |
|---------------------|-----------------|-----------------|-----------------|
| `pc1.clients.tp4`   | `10.1.1.1/24`   | x               | x               |
| `pc2.clients.tp4`   | `10.1.1.2/24`   | x               | x               |
| `pc3.clients.tp4`   | DHCP            | x               | x               |
| `pc4.clients.tp4`   | DHCP            | x               | x               |
| `pc5.clients.tp4`   | DHCP            | x               | x               |
| `dhcp1.clients.tp4` | `10.1.1.253/24` | x               | x               |
| `adm1.admins.tp4`   | x               | `10.2.2.1/24`   | x               |
| `web1.servers.tp4`  | x               | x               | `10.3.3.1/24`   |
| `r1`                | `10.1.1.254/24` | `10.2.2.254/24` | `10.3.3.254/24` |


**Vous devez me rendre le `show running-config` de tous les équipements**

- de tous les équipements réseau
  - le routeur
```
R1#show running-config
Building configuration...

Current configuration : 1268 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
!
boot-start-marker
boot-end-marker
!
!
no aaa new-model
memory-size iomem 5
no ip icmp rate-limit unreachable
!
!
ip cef
no ip domain lookup
!
!
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
ip tcp synwait-time 5
!         
!         
!         
interface FastEthernet0/0
 no ip address
 ip nat inside
 ip virtual-reassembly
 duplex auto
 speed auto
!         
interface FastEthernet0/0.11
 encapsulation dot1Q 11
 ip address 10.1.1.254 255.255.255.0
!         
interface FastEthernet0/0.12
 encapsulation dot1Q 12
 ip address 10.2.2.254 255.255.255.0
!         
interface FastEthernet0/0.13
 encapsulation dot1Q 13
 ip address 10.3.3.254 255.255.255.0
!         
interface FastEthernet1/0
 ip address dhcp
 ip nat outside
 ip virtual-reassembly
 duplex auto
 speed auto
!         
interface FastEthernet2/0
 no ip address
 shutdown 
 duplex auto
 speed auto
!         
interface FastEthernet3/0
 no ip address
 shutdown 
 duplex auto
 speed auto
!         
!         
no ip http server
ip forward-protocol nd
!         
!         
!         
no cdp log mismatch duplex
!         
!         
!         
control-plane
!         
!         
!         
!         
!         
!         
!         
!         
!         
line con 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line aux 0
 exec-timeout 0 0
 privilege level 15
 logging synchronous
line vty 0 4
 login    
!         
!         
end  
```

  - les 3 switches

**sw1**
```
Switch#show run
Building configuration...

Current configuration : 3685 bytes
!
! Last configuration change at 22:15:10 UTC Mon Oct 25 2021
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname Switch
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
!
!
!
!
!         
!         
!         
!         
ip cef    
no ipv6 cef
!         
!         
!         
spanning-tree mode pvst
spanning-tree extend system-id
!         
vlan internal allocation policy ascending
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
interface GigabitEthernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/3
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/0
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/3
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/0
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/3
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/0
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/3
 media-type rj45
 negotiation auto
!         
ip forward-protocol nd
!         
no ip http server
no ip http secure-server
!         
!         
!         
!         
!         
!         
control-plane
!         
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
!         
line con 0
line aux 0
line vty 0 4
!         
!         
end
```

**sw2**
```
Switch#show ru
Building configuration...

Current configuration : 3767 bytes
!
! Last configuration change at 22:12:30 UTC Mon Oct 25 2021
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname Switch
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
!
!
!
!
!         
!         
!         
!         
ip cef    
no ipv6 cef
!         
!         
!         
spanning-tree mode pvst
spanning-tree extend system-id
!         
vlan internal allocation policy ascending
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
interface GigabitEthernet0/0
 switchport access vlan 11
 switchport mode access
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/1
 switchport access vlan 11
 switchport mode access
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/2
 switchport access vlan 12
 switchport mode access
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/3
 switchport access vlan 13
 switchport mode access
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/3
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/0
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/3
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/0
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/3
 media-type rj45
 negotiation auto
!         
ip forward-protocol nd
!         
no ip http server
no ip http secure-server
!         
!         
!         
!         
!         
!         
control-plane
!         
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
!         
line con 0
line aux 0
line vty 0 4
!         
!         
end 
```

**sw3**
```
Switch#show run
Building configuration...

Current configuration : 3767 bytes
!
! Last configuration change at 22:19:03 UTC Mon Oct 25 2021
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname Switch
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
!
!
!
!
!         
!         
!         
!         
ip cef    
no ipv6 cef
!         
!         
!         
spanning-tree mode pvst
spanning-tree extend system-id
!         
vlan internal allocation policy ascending
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
!         
interface GigabitEthernet0/0
 switchport access vlan 11
 switchport mode access
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/1
 switchport access vlan 11
 switchport mode access
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/2
 switchport access vlan 11
 switchport mode access
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet0/3
 switchport access vlan 11
 switchport mode access
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet1/3
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/0
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet2/3
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/0
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/1
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/2
 media-type rj45
 negotiation auto
!         
interface GigabitEthernet3/3
 media-type rj45
 negotiation auto
!         
ip forward-protocol nd
!         
no ip http server
no ip http secure-server
!         
!         
!         
!         
!         
!         
control-plane
!         
banner exec ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner incoming ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
banner login ^C
**************************************************************************
* IOSv is strictly limited to use for evaluation, demonstration and IOS  *
* education. IOSv is provided as-is and is not supported by Cisco's      *
* Technical Advisory Center. Any use or disclosure, in whole or in part, *
* of the IOSv Software or Documentation to any third party for any       *
* purposes is expressly prohibited except as otherwise authorized by     *
* Cisco in writing.                                                      *
**************************************************************************^C
!         
line con 0
line aux 0
line vty 0 4
!         
!         
end   
```
```
PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.1.1.1/24
GATEWAY     : 10.1.1.254
DNS         : 1.1.1.1  
DOMAIN NAME : pc1.clients.tp4
MAC         : 00:50:79:66:68:00
LPORT       : 20028
RHOST:PORT  : 127.0.0.1:20029
MTU         : 1500

PC2> show ip

NAME        : PC2[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 10.1.1.254
DNS         : 1.1.1.1  
DOMAIN NAME : pc1.clients.tp4
MAC         : 00:50:79:66:68:01
LPORT       : 20030
RHOST:PORT  : 127.0.0.1:20031
MTU         : 1500

adm1> show ip

NAME        : adm1[1]
IP/MASK     : 10.2.2.1/24
GATEWAY     : 10.2.2.254
DNS         : 1.1.1.1  
DOMAIN NAME : adm1.admins.tp4
MAC         : 00:50:79:66:68:05
LPORT       : 20036
RHOST:PORT  : 127.0.0.1:20037
MTU         : 1500
```

**Mettre en place un serveur DHCP dans le nouveau bâtiment**

- il doit distribuer des IPs aux clients dans le réseau `clients` qui sont branchés au même switch que lui
- sans aucune action manuelle, les clients doivent...
  - avoir une IP dans le réseau `clients`
  - avoir un accès au réseau `servers`
  - avoir un accès WAN
  - avoir de la résolution DNS

Suite à cette erreur je n'ai pas pu continuer le tp
```
[adam@dhcp1 ~]$ sudo dnf install -y dhcp-server
Failed to set locale, defaulting to C.UTF-8
^CRocky Linux 8 - AppStream                                                           0% [                                                                                 ] 3.0 kB/s |   0  B     51:37 ETRocky Linux 8 - AppStream                                                                                                                                                  0.0  B/s |   0  B     07:03    
Errors during downloading metadata for repository 'appstream':
  - Curl error (28): Timeout was reached for http://nlrtm1-edge2.cdn.i3d.net/o1/k9999/pub/rockylinux/8.4/AppStream/x86_64/os/repodata/0c2535842701846572abbf971e6cc382192bbc3d82737d8fd93faada940c2bb4-primary.xml.gz?nonce=MTYzNTIwMTY3MA%3D%3D [Operation too slow. Less than 1000 bytes/sec transferred the last 30 seconds]
  - Curl error (28): Timeout was reached for http://nlrtm1-edge2.cdn.i3d.net/o1/k9999/pub/rockylinux/8.4/AppStream/x86_64/os/repodata/5f4a28e9384e321682fea107ea30e5984c7a25ce1da45629dfd97b7d6b00ce50-filelists.xml.gz?nonce=MTYzNTIwMTcwNg%3D%3D [Operation too slow. Less than 1000 bytes/sec transferred the last 30 seconds]
  [...]
  ```

  mais voicic comment je comptais procéder.
  je modifie le fichier de conf comme ci-dessous.
```
[root@dlp ~]# dnf -y install dhcp-server
[root@dlp ~]# vi /etc/dhcp/dhcpd.conf
# create new

# specify domain name

option domain-name     "clients.tp4";
# specify DNS server's hostname or IP address

option domain-name-servers     1.1.1.1;
# default lease time

default-lease-time 600;
# max lease time

max-lease-time 7200;
# this DHCP server to be declared valid

authoritative;
# specify network address and subnetmask

subnet 10.1.1.0 netmask 255.255.255.0 {
    # specify the range of lease IP address
    range dynamic-bootp 10.1.1.3 10.1.1.252;
    # specify broadcast address
    option broadcast-address 10.0.0.255;
    # specify gateway
    option routers 10.1.1.254;
}
```
j'active le service et j'autorise le trafique sur le firewall pour le service dhcpd
[root@dlp ~]# systemctl enable --now dhcpd
firewall-cmd --add-service=dhcp 

je n'ai plus qu'a demander une nouvelle IP avec la commande dhclient -v (-v pour demander et -r pour lacher)
















