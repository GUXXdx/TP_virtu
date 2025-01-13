
## Partie 1 

🌞 **`ping` d'un client du `LAN1` vers un client du `LAN 2`**
```
PC3> show ip

NAME        : PC3[1]
IP/MASK     : 10.3.2.1/24
GATEWAY     : 10.3.2.254
DNS         :
MAC         : 00:50:79:66:68:02
LPORT       : 20002
RHOST:PORT  : 127.0.0.1:20031
MTU         : 1500

PC3> ping 10.3.1.1

84 bytes from 10.3.1.1 icmp_seq=1 ttl=62 time=64.512 ms
84 bytes from 10.3.1.1 icmp_seq=2 ttl=62 time=51.231 ms
84 bytes from 10.3.1.1 icmp_seq=3 ttl=62 time=56.454 ms
84 bytes from 10.3.1.1 icmp_seq=4 ttl=62 time=47.374 ms
84 bytes from 10.3.1.1 icmp_seq=5 ttl=62 time=57.501 ms
```

🌞 **Capture Wireshark `ping_par![[ping_dns.pcapng]]tie1`**
![[ping_partie1.pcapng]]

🌞 **Afficher les adresses MAC des routeurs**
```
R1#show arp
Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  10.3.12.1               -   c401.0527.0010  ARPA   FastEthernet1/0
Internet  10.3.12.2              19   c402.0545.0000  ARPA   FastEthernet1/0
Internet  10.3.1.1                5   0050.7966.6800  ARPA   FastEthernet0/1
Internet  10.3.1.254              -   c401.0527.0001  ARPA   FastEthernet0/1
```

🌞 **Prouvez que vous avez déjà un accès internet sur `r1`**
```
R1#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 80/97/124 ms
```

🌞 **Accès internet `LAN1`**
```
PC1> ping 1.1.1.1

1.1.1.1 icmp_seq=1 timeout
84 bytes from 1.1.1.1 icmp_seq=2 ttl=56 time=69.388 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=56 time=66.102 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=56 time=65.725 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=56 time=65.006 ms
```

🌞 **Accès internet `LAN2`** 
```
PC3> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=54 time=107.900 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=54 time=112.350 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=54 time=80.668 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=54 time=94.180 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=54 time=140.364 ms
```

## Partie 2

🌞 **VLAN - Tests de `ping`**
```
PC1> ping 10.3.1.2

84 bytes from 10.3.1.2 icmp_seq=1 ttl=64 time=14.804 ms
84 bytes from 10.3.1.2 icmp_seq=2 ttl=64 time=7.825 ms
84 bytes from 10.3.1.2 icmp_seq=3 ttl=64 time=6.592 ms
84 bytes from 10.3.1.2 icmp_seq=4 ttl=64 time=14.288 ms
84 bytes from 10.3.1.2 icmp_seq=5 ttl=64 time=19.199 ms
```

🌞 **Routeur - Tests de  `ping`**
```
R1#ping 10.3.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 32/44/64 ms
R1#ping 10.3.2.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.3.2.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 32/50/64 ms
```

```
show ip

NAME        : PC1[1]
IP/MASK     : 10.3.1.1/24
GATEWAY     : 10.3.1.254
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 20024
RHOST:PORT  : 127.0.0.1:20025
MTU         : 1500

PC1> ping 10.3.2.1

84 bytes from 10.3.2.1 icmp_seq=1 ttl=63 time=64.116 ms
84 bytes from 10.3.2.1 icmp_seq=2 ttl=63 time=19.786 ms
84 bytes from 10.3.2.1 icmp_seq=3 ttl=63 time=24.817 ms
84 bytes from 10.3.2.1 icmp_seq=4 ttl=63 time=19.753 ms
84 bytes from 10.3.2.1 icmp_seq=5 ttl=63 time=25.597 ms
```

🌞 **Tests de `ping`**
```
PC1> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=55 time=49.264 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=55 time=89.912 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=55 time=53.051 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=55 time=40.730 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=55 time=48.163 ms
```

## Partie 3

🌞 **DHCP - Prouvez avec un VPCS**
```

PC4> ip dhcp
DORA IP 10.3.2.10/24 GW 10.3.2.254

PC4> show ip

NAME        : PC4[1]
IP/MASK     : 10.3.2.10/24
GATEWAY     : 10.3.2.254
DNS         : 1.1.1.1
DHCP SERVER : 10.3.2.253
DHCP LEASE  : 710, 725/362/634
MAC         : 00:50:79:66:68:03
LPORT       : 20030
RHOST:PORT  : 127.0.0.1:20031
MTU         : 1500

PC4> ping 1.1.1.1

84 bytes from 51.255.68.208 icmp_seq=1 ttl=49 time=73.435 ms
84 bytes from 51.255.68.208 icmp_seq=2 ttl=49 time=75.782 ms
84 bytes from 51.255.68.208 icmp_seq=3 ttl=49 time=93.404 ms
84 bytes from 51.255.68.208 icmp_seq=4 ttl=49 time=76.892 ms
84 bytes from 51.255.68.208 icmp_seq=5 ttl=49 time=79.790 ms
```

🌞 **Tests résolutions DNS**
```
PC4> dhcp
DDORA IP 10.3.2.144/24 GW 10.3.2.254

PC4> show ip

NAME        : PC4[1]
IP/MASK     : 10.3.2.144/24
GATEWAY     : 10.3.2.254
DNS         : 10.3.3.2
DHCP SERVER : 10.3.2.253
DHCP LEASE  : 879, 900/450/787
MAC         : 00:50:79:66:68:03
LPORT       : 20026
RHOST:PORT  : 127.0.0.1:20027
MTU         : 1500

PC4> ping efrei.fr
efrei.fr resolved to 51.255.68.208

84 bytes from 51.255.68.208 icmp_seq=1 ttl=51 time=35.010 ms
84 bytes from 51.255.68.208 icmp_seq=2 ttl=51 time=31.204 ms
84 bytes from 51.255.68.208 icmp_seq=3 ttl=51 time=43.429 ms
84 bytes from 51.255.68.208 icmp_seq=4 ttl=51 time=40.276 ms
84 bytes from 51.255.68.208 icmp_seq=5 ttl=51 time=29.624 ms

PC4> ping dns.tp3.b2
dns.tp3.b2 resolved to 10.3.3.3

84 bytes from 10.3.3.3 icmp_seq=1 ttl=63 time=41.150 ms
84 bytes from 10.3.3.3 icmp_seq=2 ttl=63 time=33.872 ms
84 bytes from 10.3.3.3 icmp_seq=3 ttl=63 time=117.969 ms
84 bytes from 10.3.3.3 icmp_seq=4 ttl=63 time=22.565 ms
84 bytes from 10.3.3.3 icmp_seq=5 ttl=63 time=43.001 ms
```


🌞 **Capture Wireshark** ![[ping_dns.pcapng]]
🌞 **HTTP - Preuve avec un client**
```
[toto@dns ~]$ curl supersite.tp3.b2 | head 

<!doctype html>
	<head>
		<meta charset='utf-8'>
		<meta name='viewport" content='width=device-width, initial-scale=1'>
		<title>HTTP Server Test Page powered by: Rocky Linux</title>


[toto@dns ~]$ curl web.tp3.b2 | head

<!doctype html>
	<head>
		<meta charset='utf-8'>
		<meta name='viewport" content='width=device-width, initial-scale=1'>
		<title>HTTP Server Test Page powered by: Rocky Linux</title>
```

## Partie 4