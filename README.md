## 1. .

Pour rappel : le tableau d'adressage.

|      Machines       | IP correspondate |
|:-------------------:|:----------------:|
|  `node1.tp1.efrei`  |  `10.1.1.1/24`   |
|  `node2.tp1.efrei`  |  `10.1.1.2/24`   |

---

### 1.1. Les adresses MAC.

> Machine 1:

```
PC1> show ip

NAME        : PC1[1]
IP/MASK     : 0.0.0.0/0
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 10000
RHOST:PORT  : 127.0.0.1:10001
MTU:        : 1500
```

> Machine 2:

```
PC2> show ip

NAME        : PC2[1]
IP/MASK     : 0.0.0.0/0
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 10008
RHOST:PORT  : 127.0.0.1:10009
MTU:        : 1500

PC2>
```

### 1.2. Les adresses IP.

> PC1:

```
PC1> ip 10.1.1.1/24
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0

PC1> show ip

NAME        : PC1[1]
IP/MASK     : 10.1.1.1/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 10000
RHOST:PORT  : 127.0.0
```

> PC2:

```
PC2> ip 10.1.1.2/24
Checking for duplicate address...
PC1 : 10.1.1.2 255.255.255.0

PC2> show ip

NAME        : PC2[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 10008
RHOST:PORT  : 127.0.0.1:10009
MTU:        : 1500
```

### 1.3. Ping.

> De PC1 à PC2:
```
PC1> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=0.177 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=0.475 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=0.355 ms
```

> De PC2 à PC1:
```
PC2> ping 10.1.1.1
84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=0.369 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=0.370 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=0.367 ms
... (311lignes restantes
