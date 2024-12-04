# Jarkom-Modul-5-IT05-2024

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

up echo nameserver 192.168.122.1 > /etc/resolv.conf
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
### HIA (Webserver)
```
#A3
auto eth0
iface eth0 inet static
  address 10.66.0.10
  netmask 255.255.255.248
  gateway 10.66.0.9

up echo nameserver 192.168.122.1 > /etc/resolv.conf
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
post-up route add -net 10.66.2.64 netmask 255.255.255.192 gw 10.66.0.2 #A9

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

## Penyelesaian
### Prerequesite
tambahkan konfigurasi berikut di `/root/.bashrc` di New Eridu untuk forward IP agar semua nodes terhubung ke internet
```
echo net.ipv4.ip_forward=1 >/etc/sysctl.conf
sysctl -p

ETH0_IP=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $ETH0_IP
```
### Konfigurasi DHCP Server
```
apt-get update
apt-get install isc-dhcp-server netcat -y
service isc-dhcp-server start

echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server

# A4
echo 'subnet 10.66.0.128 netmask 255.255.255.128 {
        range 10.66.0.129 10.66.0.254;
        option routers 10.66.0.129;
        option broadcast-address 10.66.0.255;
        option domain-name-servers 10.66.2.10; #IP DNS Server
}
# A5
subnet 10.66.1.0 netmask 255.255.255.0 {
        range 10.66.1.1 10.66.1.254;
        option routers 10.66.1.1;
        option broadcast-address 10.66.1.255;
        option domain-name-servers 10.66.2.10; #IP DNS Server
}
# A8
subnet 10.66.2.64 netmask 255.255.255.192 {
        range 10.66.2.65 10.66.2.126;
        option routers 10.66.2.65;
        option broadcast-address 10.66.2.127;
        option domain-name-servers 10.66.2.10; #IP DNS Server
}
#A7
subnet 10.66.2.8 netmask 255.255.255.248 {}'>/etc/dhcp/dhcpd.conf
```
### Konfigurasi DHCP Relay
```
apt-get update
apt-get install isc-dhcp-relay netcat -y
service isc-dhcp-relay start

echo 'SERVERS="10.66.2.11" # IP DHCP Server
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf
sysctl -p

service isc-dhcp-relay restart
service rsyslog start
```
## Misi 2 No 2
> Tidak ada perangkat lain yang bisa melakukan ping ke Fairy. Tapi Fairy tetap dapat mengakses semua perangkat
### Penyelesaian
jalankan command beerikut di console Fairy
```
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```
### Testing
Fairy dapat ping HIA

<img width="554" alt="Screenshot 2024-12-01 at 12 36 09" src="https://github.com/user-attachments/assets/bda798af-19b7-4d1d-9056-b21c36e42ebc">

HIA tidak dapat ping Fairy

<img width="520" alt="Screenshot 2024-12-01 at 12 37 04" src="https://github.com/user-attachments/assets/d89d7148-cd4c-47fd-a071-cb697e50bf2e">

## Misi 2 No 3 
> HDD hanya bisa diakses oleh Fairy

1. Tambahkan config berikut ke `/root/.bashrc`
```
export DEBIAN_FRONTEND=noninteractive
apt update
apt install bind9 netcat -y

echo 'options {
        directory "/var/cache/bind";

         forwarders {
                192.168.122.1;
         };

        allow-query { any; };
        auth-nxdomain no;

        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```
2. kemudian jalankan command berikut pada console HDD
```
iptables -P INPUT DROP
iptables -A INPUT -s 10.66.2.11 -j ACCEPT
```
### Testing
Fairy bisa mengakses HDD

<img width="574" alt="image" src="https://github.com/user-attachments/assets/99a279d5-6cac-4ad1-b3f6-4bc3a82bdf73">

LuminaSquare tidak bisa mengakses HDD

<img width="502" alt="image" src="https://github.com/user-attachments/assets/223b1a31-fff5-4e0e-9f65-0aba93a9aeec">

testing dengan netcat, sebelumnya pastikan telah membuka port yang akan digunakan di HDD. Disini saya menggunakan port 8888
```
nc -l -p 8888
```
lalu coba test dari Fairy dan nodes bebas lainnya

<img width="547" alt="image" src="https://github.com/user-attachments/assets/1a4e0ba1-ea5e-4be3-8b59-59c564e61164">

<img width="682" alt="image" src="https://github.com/user-attachments/assets/b2676e72-8d9f-45df-89d0-5af634bfa706">

bisa dilihat dari gambar berikut, pesan dari Fairy sampai di HDD sedangkan dari LuminaSquare tidak sampai

<img width="546" alt="image" src="https://github.com/user-attachments/assets/5f5d4ad9-cb40-4073-b2e4-28c7030b2814">

## Misi 2 No 4
> HollowZero hanya bisa diakses oleh Caesar, Burnice, PoliceBoo, Jane pada hari Senin-Jumat

lakukan config berikut di HollowZero
```
export DEBIAN_FRONTEND=noninteractive
apt update
apt install apache2 -y

echo 'Welcome to HollowZero' > /var/www/html/index.html

echo '<VirtualHost *:80>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf

service apache2 restart
```
kemudian jalankan command berikut di HollowZero
```
iptables -P INPUT DROP
iptables -A INPUT -s 10.66.2.64/26 -m time --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s 10.66.1.0/24 -m time --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
```

### Testing

<img width="720" alt="image" src="https://github.com/user-attachments/assets/8412ce48-7dc1-473d-9dd6-010501117850">

<img width="696" alt="image" src="https://github.com/user-attachments/assets/2ddbe921-5ca0-4e2b-ae2a-1adf029a8441">

Dapat dilihat dari gambar di atas, Caesar tidak dapat ngeping dan ngecurl HollowZero karena ini hari Minggu. 

Untuk memastikan, tambahin hari minggu ke iptables punya A8 tadi agar dapat mengakses HollowZero. Namun sebelumnya pastikan telah menjalankan command `iptables -D INPUT 1` untuk menghapus iptables sebelumnya

<img width="719" alt="image" src="https://github.com/user-attachments/assets/8c4c315f-680d-4a08-b00a-f723f5db4c75">

#### Caesar
<img width="548" alt="image" src="https://github.com/user-attachments/assets/7205f7e1-04ef-4548-94a3-8cfb0cad4967">

bisa ngeping dan ngecurl HollowZero

#### Policeboo
<img width="568" alt="image" src="https://github.com/user-attachments/assets/be55ed10-f0ee-43a4-b7ee-10e19e8c4e46">

Policeboo tidak bisa ngeping dan ngecurl HollowZero karena hanya bisa mengakses di hari senin-jumat saja

#### Lycaon
<img width="605" alt="image" src="https://github.com/user-attachments/assets/aa754aa4-9ccc-49e3-8d41-e01d74fad2a3">

Lycaon tidak bisa ngeping dan ngecurl HollowZero karena tidak memiliki akses sama sekali ke HollowZero

## Misi 2 No 5
> HIA hanya bisa diakses oleh Ellen dan Lycaon pada pukul 08:00 - 21:00 dan bisa diakses oleh Jane serta Policeboo hanya pada pukul 03:00 - 23:00

lakukan config berikut di HIA
```
export DEBIAN_FRONTEND=noninteractive
apt update
apt install apache2 -y

echo 'Welcome to HollowZero' > /var/www/html/index.html

echo '<VirtualHost *:80>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf

service apache2 restart
```
Jalankan command berikut di HIA
```
iptables -P INPUT DROP
iptables -A INPUT -s 10.66.0.128/25 -m time --timestart 08:00 --timestop 21:00 -j ACCEPT
iptables -A INPUT -s 10.66.1.0/24 -m time --timestart 03:00 --timestop 23:00 -j ACCEPT
```

### Testing
untuk test yang pertama, coba begini:

<img width="720" alt="image" src="https://github.com/user-attachments/assets/635b6800-3dd9-4829-8639-8018c97459cc">

#### PoliceBoo

<img width="560" alt="image" src="https://github.com/user-attachments/assets/cf4a19ec-0206-4dc4-893e-ef664fe13a1e">

#### Lycaon

<img width="552" alt="image" src="https://github.com/user-attachments/assets/e979d70d-35cb-40d8-aa77-98154c27e282">

dari kedua gambar tersebut, bisa kita lihat bahwa keduanya masih dapat mengakses HIA karena jamnya masih sesuai dengan yang di iptables

untuk test yang kedua, kita ubah salah satu iptables biar tidak bisa akses HIA

<img width="720" alt="image" src="https://github.com/user-attachments/assets/595e70d5-e397-4522-9fa3-ad6e1b62df19">

#### PoliceBoo

<img width="579" alt="image" src="https://github.com/user-attachments/assets/9ce16325-5e61-4d4a-bbd5-8acdae67f768">

PoliceBoo gabisa akses karena cuma bisa sampe jam 17.00 saja sedangkan sekarang jam 18.00an

#### Lycaon

<img width="544" alt="image" src="https://github.com/user-attachments/assets/c721523a-c49d-4203-83d6-4f21875eece2">

Lycaon masih bisa akses karena jam nya masih sesuai

## Misi 2 No 6
> HIA harus memblokir aktivitas port scanning yang melebihi 25 port dalam rentang 10 detik, penyerang yang diblokir tidak bisa ping, nc, atau curl ke HIA, log dari iptables akan tercatat untuk analisis.

jalankan command bereikut di HIA
```
# Atur rate limit untuk port scanning (maksimum 25 koneksi per 10 detik)
iptables -N PORTSCAN
iptables -A INPUT -p tcp --dport 1:100 -m state --state NEW -m recent --set --name portscan
iptables -A INPUT -p tcp --dport 1:100 -m state --state NEW -m recent --update --seconds 10 --hitcount 25 --name portscan -j PORTSCAN

# Blokir IP yang terdeteksi melakukan port scanning tidak wajar
iptables -A PORTSCAN -m recent --set --name blacklist
iptables -A PORTSCAN -j DROP

# Blokir semua aktivitas dari IP yang ada di daftar blacklist
iptables -A INPUT -m recent --name blacklist --rcheck -j REJECT
iptables -A OUTPUT -m recent --name blacklist --rcheck -j REJECT

# Logging untuk port scanning
iptables -A PORTSCAN -j LOG --log-prefix='PORT SCAN DETECTED' --log-level 4
```

### Testing
Sebelum Nmap masih bisa nc, ping, curl HIA

#### nc

<img width="583" alt="image" src="https://github.com/user-attachments/assets/4b452512-1c4e-40a1-a2d8-6d43d6a88931">

<img width="251" alt="image" src="https://github.com/user-attachments/assets/76dbf491-3311-4826-9f75-1a16bfb668b2">

#### ping dan curl

<img width="546" alt="image" src="https://github.com/user-attachments/assets/e8cb1cfa-e399-444f-b581-89dce4faaae5">

Sesudah nmap, dah gak bisa nc, ping, curl HIA
```
nmap -p 1-100 10.66.0.10
```
#### nc

<img width="582" alt="image" src="https://github.com/user-attachments/assets/569ff2e2-184d-4772-9d24-e2d6d904f1ea">

#### ping dan curl

<img width="660" alt="image" src="https://github.com/user-attachments/assets/139f2a13-55d8-41a7-99fd-f76908111057">

Hasil Analisis
https://drive.google.com/file/d/1bUIxeWZVaNQJRAic0sr0dP4Omk-S3MJp/view?usp=sharing

## Misi 2 No 7
> Untuk HollowZero hanya ada 2 koneksi aktif dari 2 IP berbeda dalam waktu bersamaan yang diperbolehkan

Jalankan command berikut di HollowZero
```
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -m recent --set
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW -m recent --update --seconds 1 --hitcount 3 -j REJECT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```
### Testing
sebelum testing pastikan sudah menginstal parallel
```
apt-get update
apt-get install parallel -y
```
lakukan testing dengan command berikut:
```
parallel curl -s http://IP-HollowZero ::: IP-Caesar IP-Burnice IP-Jane IP-Policeboo
```
<img width="745" alt="image" src="https://github.com/user-attachments/assets/2b2c423f-d638-495e-9430-08ba4bbee91a">


## Misi 2 No 8
> Agar setiap paket yang dikirimkan ke Burnice dapat dialihkan ke HollowZero

Jalankan command berikut di Burnice
```
iptables -t nat -A PREROUTING -p tcp --dport 8888 -j DNAT --to-destination 10.66.2.130
iptables -t nat -A POSTROUTING -p tcp --dport 8888 -j MASQUERADE
```

### Testing
#### Jalanin ini di HollowZero

<img width="411" alt="image" src="https://github.com/user-attachments/assets/1c637982-1bbb-4728-be4a-f8eaeba6176b">

#### dari fairy kita netcat ke burnice

<img width="632" alt="image" src="https://github.com/user-attachments/assets/4a2d2c73-40af-40be-8f05-b23b09ffedd5">

#### hasilnya muncul di Hollow

<img width="395" alt="image" src="https://github.com/user-attachments/assets/db00721e-2b1b-4a44-b15c-b5b0e739f253">

## Misi 3
> memblokir semua transmisi masuk maupun keluar dari Burnice bisa memanipulasi policy iptables. Sebelum Burnice sepenuhnya terisolasi, Fairy mengirimkan pesan moral:
“Kepercayaan adalah dasar dari jaringan yang aman. Jangan pernah mengkhianatinya.”

Lakukan command berikut di console Burnice
```
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
```
### Testing
coba ini di Fairy
```
 echo “Kepercayaan adalah dasar dari jaringan yang aman. Jangan pernah mengkhianatinya.” | nc 10.66.2.67 8888
```
Hasilnya bakal begini:

<img width="722" alt="image" src="https://github.com/user-attachments/assets/3ba5c72d-70df-4f19-907e-e5f7fc563467">

sekarang waktunya kita isolasi Burnice, pake command yang sudah saya sebut di atas tadi

<img width="549" alt="image" src="https://github.com/user-attachments/assets/923ca214-1e32-4c28-b14a-d706a24a7b85">

sudah ga bisa ping burnice

<img width="639" alt="image" src="https://github.com/user-attachments/assets/117f5c78-5181-428b-8072-0e578526844a">

burnice sudah tidak bisa ping kemanapun juga, rasakan itu burnice... 

BERESSS bye jarkom 😋
