# Jarkom-Modul-5_IT05_2024

| Nama | NRP |
| ---- | :-: |
| Adlya Isriena Aftarisya | 5027231066 |
| Furqon Aryadana | 5027231024 |

## Topologi dan subnetting
<img width="763" alt="image" src="https://github.com/user-attachments/assets/8b17a371-00ab-41b1-adf8-e460142365b5">

## Pembagian IP
<img width="1056" alt="Screenshot 2024-11-30 at 18 36 21" src="https://github.com/user-attachments/assets/f0a4e124-7918-4ba1-a229-8f9590491e57">

## Konfigurasi
### New Eridu
```
auto eth0
iface eth0 inet dhcp

#A1
auto eth1
iface eth1 inet static
  address 10.66.0.1
  netmask 255.255.255.252
  
#A2
auto eth2
iface eth2 inet static
  address 10.66.0.5
  netmask 255.255.255.252
```
### SixStreet
```
#A1
auto eth0
iface eth0 inet static
  address 10.66.0.2
  netmask 255.255.255.252
  gateway 10.66.0.1

#A6
auto eth1
iface eth1 inet static
  address 10.66.2.1
  netmask 255.255.255.248

#A7
auto eth2
iface eth2 inet static
  address 10.66.2.9
  netmask 255.255.255.248

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
### HDD (DNS Server)
```
#A7
auto eth0
iface eth0 inet static
  address 10.66.2.10
  netmask 255.255.255.248
  gateway 10.66.2.9

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
### Fairy (DHCP Server)
```
#A7
auto eth0
iface eth0 inet static
  address 10.66.2.11
  netmask 255.255.255.248
  gateway 10.66.2.9

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
### OuterRing
```
#A6
auto eth0
iface eth0 inet static
  address 10.66.2.3
  netmask 255.255.255.248
  gateway 10.66.2.1

#A8
auto eth1
iface eth1 inet static
  address 10.66.2.65
  netmask 255.255.255.192

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
### ScootOutpost
```
#A6
auto eth0
iface eth0 inet static
  address 10.66.2.2
  netmask 255.255.255.248
  gateway 10.66.2.1

#A9
auto eth1
iface eth1 inet static
  address 10.66.2.129
  netmask 255.255.255.252
```
### HollowZero (Webserver)
```
#A9
auto eth0
iface eth0 inet static
  address 10.66.2.130
  netmask 255.255.255.252
  gateway 10.66.2.129

post-up route add -net 10.66.0.0 netmask 255.255.255.252 gw 10.66.2.129 #A1
```
### LuminaSquare
```
#A2
auto eth0
iface eth0 inet static
  address 10.66.0.6
  netmask 255.255.255.252
  gateway 10.66.0.5

#A3
auto eth1
iface eth1 inet static
  address 10.66.0.9
  netmask 255.255.255.248

#A5
auto eth2
iface eth2 inet static
  address 10.66.1.1
  netmask 255.255.255.0

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
### HIA
```
#A3
auto eth0
iface eth0 inet static
  address 10.66.0.10
  netmask 255.255.255.248
  gateway 10.66.0.9
```
### BalletTwins
```
#A3
auto eth0
iface eth0 inet static
  address 10.66.0.11
  netmask 255.255.255.248
  gateway 10.66.0.9

#A4
auto eth1
iface eth1 inet static
  address 10.66.0.129
  netmask 255.255.255.128

up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
### Burnice, Lycaon, Policeboo, Caesar, Ellen, dan Jane (Client)
```
auto eth0
iface eth0 inet dhcp
```

## Routing
### New Eridu
```
#KIRI
post-up route add -net 10.66.2.8 netmask 255.255.255.248 gw 10.66.0.2 #A7
post-up route add -net 10.66.2.0 netmask 255.255.255.248 gw 10.66.0.2 #A6
post-up route add -net 10.66.2.128 netmask 255.255.255.252 gw 10.66.0.2 #A9

#KANAN
post-up route add -net 10.66.0.8 netmask 255.255.255.248 gw 10.66.0.6 #A3
post-up route add -net 10.66.1.0 netmask 255.255.255.0 gw 10.66.0.6 #A5
post-up route add -net 10.66.0.128 netmask 255.255.255.128 gw 10.66.0.6 #A4
```
### SixStreet
```
post-up route add -net 10.66.2.128 netmask 255.255.255.252 gw 10.66.2.2 #A9
post-up route add -net 10.66.2.64 netmask 255.255.255.192 gw 10.66.2.3 #A8
```
### Fairy (DHCP Server)
```
post-up route add -net 10.66.2.64 netmask 255.255.255.192 gw 10.66.2.9 #A8
post-up route add -net 10.66.1.0 netmask 255.255.255.0 gw 10.66.2.9 #A5
post-up route add -net 10.66.0.128 netmask 255.255.255.128 gw 10.66.2.9 #A4
```
### HollowZero (Webserver)
```
post-up route add -net 10.66.0.0 netmask 255.255.255.252 gw 10.66.2.1 #A1
```
### LuminaSquare
```
post-up route add -net 10.66.0.128 netmask 255.255.255.128 gw 10.66.0.11 #A4
```
### HIA
```
post-up route add -net 10.66.0.4 netmask 255.255.255.252 gw 10.66.0.9 #A2
```
### BalletTwins
```
post-up route add -net 10.66.2.8 netmask 255.255.255.248 gw 10.66.0.9 #A7
```
