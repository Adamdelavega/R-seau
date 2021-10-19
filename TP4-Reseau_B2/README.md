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
PC1> ip 10.1.1.1 255.255.255.0
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


PC2> ip 10.1.1.2 255.255.255.0
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
Switch(config)#interface GigabitEthernet0/3
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






