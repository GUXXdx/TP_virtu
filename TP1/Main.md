## Partie 1

🌞 **Déterminer l'adresse MAC de vos deux machines** | 🌞 **Définir une IP statique sur les deux machines** 
*(Je fais les 2 en même temps, juste trop efficace )*
`node1.tp1> ip 10.1.1.1/24
`node2.tp1> ip 10.1.1.2/24`

```
node1.tp1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node1.t10.1.1.1/24          0.0.0.0           00:50:79:66:68:00  20002  127.0.0.1:20003
       fe80::250:79ff:fe66:6800/64
```

```
node2.tp1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node2.t10.1.1.2/24          0.0.0.0           00:50:79:66:68:01  20004  127.0.0.1:20005
       fe80::250:79ff:fe66:6801/64
```

🌞 **Effectuer un `ping` d'une machine à l'autre**
```
node2.tp1> ping 10.1.1.1

84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=5.419 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=4.244 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=5.608 ms
84 bytes from 10.1.1.1 icmp_seq=4 ttl=64 time=3.856 ms
84 bytes from 10.1.1.1 icmp_seq=5 ttl=64 time=0.722 ms
```

🌞 **Wireshark !**
![[ping.pcapng]]

🌞 **ARP**
```
node1.tp1> arp

00:50:79:66:68:01  10.1.1.2 expires in 91 seconds
```

## Partie 2

🌞 **Déterminer l'adresse MAC de vos trois machines** | 🌞 **Définir une IP statique sur les trois machines**
```
node1.tp1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node1.t10.1.1.1/24          0.0.0.0           00:50:79:66:68:00  20002  127.0.0.1:20003
       fe80::250:79ff:fe66:6800/64
```

```
node2.tp1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node2.t10.1.1.2/24          0.0.0.0           00:50:79:66:68:01  20004  127.0.0.1:20005
       fe80::250:79ff:fe66:6801/64
```

```
node3.tp1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node3.t10.1.1.3/24          0.0.0.0           00:50:79:66:68:02  20010  127.0.0.1:20011
       fe80::250:79ff:fe66:6802/64
```

🌞 **Effectuer des `ping` d'une machine à l'autre**
```
node1.tp1> ping 10.1.1.2

84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=2.985 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=2.488 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=2.518 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=10.729 ms
84 bytes from 10.1.1.2 icmp_seq=5 ttl=64 time=0.768 ms
```

```
node2.tp1> ping 10.1.1.3

84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=4.191 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=1.727 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=10.169 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=1.248 ms
84 bytes from 10.1.1.3 icmp_seq=5 ttl=64 time=2.289 ms
```

```
node1.tp1> ping 10.1.1.3

84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=3.724 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=2.394 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=2.543 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=2.787 ms
84 bytes from 10.1.1.3 icmp_seq=5 ttl=64 time=3.444 ms
```

## Partie 3

🌞 **Donner un accès Internet à la machine `dhcp.tp1.efrei`**
```
[toto@localhost ~]$ ping 1.1.1.1

64 bytes from 1.1.1.1 icmp_seq=1 ttl=57 time=24.1 ms
64 bytes from 1.1.1.1 icmp_seq=2 ttl=57 time=24.1 ms
64 bytes from 1.1.1.1 icmp_seq=3 ttl=57 time=24.1 ms
64 bytes from 1.1.1.1 icmp_seq=4 ttl=57 time=23.5 ms
64 bytes from 1.1.1.1 icmp_seq=4 ttl=57 time=24.3 ms
```

🌞 **Installer et configurer un serveur DHC**
`dnf-y install dhcp-server`
```
vi /etc/dhcp/dhcpd.conf

authoritative;
subnet 10.1.1.0 netmask 255.255.255.0 {
	range 10.1.1.10 10.1.1.50;
	option broadcast-address 10.1.1.1;
	option routers 10.1.1.1;
}
```
`systemctl enable --now dhcpd`

🌞 **Récupérer une IP automatiquement depuis les 3 nodes**

🌞 **Wireshark !**