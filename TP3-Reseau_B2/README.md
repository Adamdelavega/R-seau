# TP3 : Progressons vers le réseau d'infrastructure
# 0. Prérequis
# I. (mini)Architecture réseau

**Vous me rendrez un 🗃️ tableau des réseaux 🗃️ qui rend compte des adresses choisies, sous la forme** :

| Nom du réseau | Adresse du réseau | Masque            | Nombre de clients possibles | Adresse passerelle | [Adresse broadcast|
|---------------|-------------------|-------------------|-----------------------------|--------------------|-------------------|
| `server1`     | `10.3.0.0/25`     | `255.255.255.128` | `128 - 3 = 125`             | `10.3.0.126`       | `10.3.0.127`      |
| `client1`     | `10.3.0.128/26`   | `255.255.255.192` | `64 - 3 = 61`               | `10.3.0.190`       | `10.3.0.191`      |
| `server2`     | `10.3.0.192/26`   | `255.255.255.192` | `64 - 3 = 61`               | `10.3.0.254`       | `10.3.3.255`      |

**Vous pouvez d'ores-et-déjà créer le routeur. Pour celui-ci, vous me prouverez que :**

- il a bien une IP dans les 3 réseaux, l'IP que vous avez choisie comme IP de passerelle
- il a un accès internet
- il a de la résolution de noms
- il porte le nom `router.tp3`*
- n'oubliez pas [d'activer le routage sur la machine](../../cours/memo/rocky_network.md#activation-du-routage)

# II. Services d'infra
## 1. Serveur DHCP

**VM `dhcp.client1.tp3`**

**Mettre en place une machine qui fera office de serveur DHCP** dans le réseau `client1`. Elle devra :

- porter le nom `dhcp.client1.tp3`
```
[adam@dhcp ~]$ hostname
dhcp.client1.tp3
```
- [📝**checklist**📝](#checklist)
- donner une IP aux machines clients qui le demande
```
# specify the range of lease IP address
  range dynamic-bootp 10.3.0.131 10.3.0.189;
```
- leur donner l'adresse de leur passerelle
```
 # specify gateway
    option routers 10.3.0.190;
```
- leur donner l'adresse d'un DNS utilisable
```
# specify DNS server's hostname or IP address
option domain-name-servers     1.1.1.1; 
```

📁 **Fichier `dhcpd.conf`**

