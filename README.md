# Jarkom-Modul-5-B23-2023
# **Praktikum Modul 5 Jaringan Komputer**
Berikut adalah Repository dari Kelompok B23 untuk pengerjaan Praktikum Modul 5. Dalam Repository ini terdapat daftar anggota kelompok, dokumentasi dan Penjelasan tiap soal, _Screenshot_, dan Kendala yang Dialami. 

# **Anggota Kelompok**
| Nama                      | NRP        | Kelas               |
| ------------------------- | ---------- | ------------------- |
| Armadya Hermawan Sarwono  | 5025211243 | Jaringan Komputer B |
| Dian Lies Seviona Dabukke | 5025211080 | Jaringan Komputer B |

# **Dokumentasi dan Penjelasan Soal**
Berikut adalah dokumentasi yang tiap soal dan penjelasan terkait perintah yang digunakan :

# **VLSM dengan GNS3**
Teknik ini pengefisiensian pembagian IP(subnetting) dengan menyesuaikan besar netmask sesuai banyaknya host/komputer yang membutuhkannya. 
Langkah pertama tandai subnet pada gambar topologi anda 
![Screenshot 2023-12-19 171627](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/ed9f6613-5bd2-46a7-8026-08922c5edbce)
<br>                            
2. Setelah itu, tentukan jumlah alamat IP yang dibutuhkan seperti tabel dibawah : 
|  Subnet |  Jumlah IP  |  Netmask  |
| ------  | ----- | ------- |
|   A1    |   2   |   /30   |
|   A2    |   2   |   /30   |
|   A3    |   66  |   /25   |
|   A4    |  256  |   /23   |
|   A5    |   2   |   /30   |
|   A6    |   2   |   /30   |
|   A7    |   2   |   /30   |
|   A8    |   2   |   /30   |
|   A9    | 1023  |   /21   |
|   A10   |  514  |   /22   |
|  **TOTAL**  |  **1871** |   **/21**   |

<br>
3. Sehingga akan dihasilkan sebuah tree yang dimana IP-nya akan diatur tiap interface sesuai dengan aturan subnetting yang darinya didapatkan Network ID, Broadcast Address, dan Available Hosts. 
<img width="3175" alt="Untitled (Copy)" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/d66d12ae-8c62-410e-82e6-8a17d408852f">
<br>
Sebelum melakukan konfigurasi dan routing : <br>

* SIMPAN ROUTING DALAM : _/root/rute.sh_ 
* BUKA : _/etc/sysctl.conf_ -> UNCOMMENT : _net.ipv4.ip_forward=1_ (PADA SEMUA ROUTER) DAN SIMPAN DI _/root/sysctl.conf_  
* PADA _root/.bashrc_ di AURA TAMBAHKAN : _iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.20.0.0/16_ 
dan PADA _root/.bashrc_ di tiap node TAMBAHKAN : _echo nameserver 192.168.122.1 > /etc/resolv.conf_
* untuk testing, lakukan pada server-client :
```bash
apt-get update
apt-get install netcat
```
Server: ```bash nc -l -p [port] ```
Client: ```bash nc [ip server] [port] ```
<br>

**Aura (ROUTER)**
<br>
Configurasi : 
```bash
Aura -> NAT
auto eth0
iface eth0 inet dhcp

Aura -> Heiter
auto eth1
iface eth1 inet static
        address 10.20.0.21
        netmask 255.255.255.252

Aura -> Frieren
auto eth2
iface eth2 inet static
         address 10.20.0.17
         netmask 255.255.255.252
```
Routing :
```bash
 route add -net 10.20.8.0 netmask 255.255.248.0 gw 10.20.0.22
 route add -net 10.20.4.0 netmask 255.255.252.0 gw 10.20.0.22
 route add -net 10.20.0.0 netmask 255.255.255.252 gw 10.20.0.18
 route add -net 10.20.0.4 netmask 255.255.255.252 gw 10.20.0.18
 route add -net 10.20.0.128 netmask 255.255.255.128 gw 10.20.0.18
 route add -net 10.20.2.0 netmask 255.255.254.0 gw 10.20.0.18
 route add -net 10.20.0.8 netmask 255.255.255.252 gw 10.20.0.18
 route add -net 10.20.0.12 netmask 255.255.255.252 gw 10.20.0.18
```
**Heiter (ROUTER)**
<br>
Config :
```bash
Heiter -> Aura
auto eth0
iface eth0 inet static
        address 10.20.0.22
        netmask 255.255.255.252
   gateway 10.20.0.21


Heiter -> TurkRegion
auto eth1
iface eth1 inet static
        address 10.20.8.1
        netmask 255.255.248.0

Heiter -> Switch 3
auto eth2
iface eth2 inet static
        address 10.20.4.1
        netmask 255.255.252.0
``` 
Routing :
```bash
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.20.0.21
 ```

**TurkRegion  (CLIENT)**
<br>
Config :
```bash
TurkRegion -> Heiter
auto eth0
iface eth0 inet static
          address 10.20.8.2
          netmask 255.255.248.0
          gateway 10.20.8.1
 ```
 
**Sein (SERVER)**
<br>
Config :
```bash
Sein -> Heiter
auto eth0
iface eth0 inet static
          address 10.20.4.2
          netmask 255.255.252.0
          gateway 10.20.4.1
```
 
**GrabForest (CLIENT)**
<br>
Config :
```bash
GrabForest -> Heiter
auto eth0
iface eth0 inet static
          address 10.20.4.3
          netmask 255.255.252.0
          gateway 10.20.4.1
```
 
**Frieren (ROUTER)**
<br>
Config :
```bash
Frieren -> Aura
auto eth0
iface eth0 inet static
        address 10.20.0.18
        netmask 255.255.255.252
   gateway 10.20.0.17


Frieren -> Stark
auto eth1
iface eth1 inet static
        address 10.20.0.13
        netmask 255.255.255.252

Frieren -> Himmel
auto eth2
iface eth2 inet static
        address 10.20.0.9
        netmask 255.255.255.252
 ```
Routing :
```bash
route add -net 10.20.0.0 netmask 255.255.255.252 gw 10.20.0.10
route add -net 10.20.0.4 netmask 255.255.255.252 gw 10.20.0.10
route add -net 10.20.0.128 netmask 255.255.255.128 gw 10.20.0.10
route add -net 10.20.2.0 netmask 255.255.254.0 gw 10.20.0.10
 ```

**Stark (SERVER)**
<br>
Config :
```bash
Stark -> Frieren
auto eth0
iface eth0 inet static
          address 10.20.0.14
          netmask 255.255.255.252
          gateway 10.20.0.13
```
 
**Himmel (ROUTER)**
<br>
Config :
```bash
Himmel -> Frieren
auto eth0
iface eth0 inet static
        address 10.20.0.10
        netmask 255.255.255.252
   gateway 10.20.0.9


Himmel -> LaubHills
auto eth1
iface eth1 inet static
        address 10.20.2.1
        netmask 255.255.254.0

Himmel -> Switch 1
auto eth2
iface eth2 inet static
        address 10.20.0.129
        netmask 255.255.255.128
```
Routing :
```bash
route add -net 10.20.0.0 netmask 255.255.255.252 gw 10.20.0.131
route add -net 10.20.0.4 netmask 255.255.255.252 gw 10.20.0.131
 ```

**LaubHills (CLIENT)**
<br>
Config :
```bash
LaubHills -> Himmel
auto eth0
iface eth0 inet static
          address 10.20.2.2
          netmask 255.255.254.0
          gateway 10.20.2.1
```

**SchwerMountain (CLIENT)**
<br>
Config :
```bash
SchwerMountain -> Himmel
auto eth0
iface eth0 inet static
          address 10.20.0.130
          netmask 255.255.255.128
          gateway 10.20.0.129
``` 

**Fern (ROUTER)**
<br>
Config :
```bash
Fern -> Himmel
auto eth0
iface eth0 inet static
        address 10.20.0.131
        netmask 255.255.255.128
   gateway 10.20.0.129

Fern -> Richter
auto eth2
iface eth2 inet static
        address 10.20.0.5
        netmask 255.255.255.252

Fern -> Switch 2
auto eth1
iface eth1 inet static
        address 10.20.0.1
        netmask 255.255.255.252
 ```
Routing :
```bash
 route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.20.0.129
```

**Richter (SERVER)**
<br>
Config :
```bash
Richter -> Fern
auto eth0
iface eth0 inet static
          address 10.20.0.6
          netmask 255.255.255.252
          gateway 10.20.0.5
```

**Revolte (SERVER)**
<br>
Config :
```bash
Revolte -> Fern
auto eth0
iface eth0 inet static
          address 10.20.0.2
          netmask 255.255.255.252
          gateway 10.20.0.1
 ```

# **DHCP Server : Revolte**
<br>

```bash
apt-get update
apt-get install isc-dhcp-server
nano /etc/default/isc-dhcp-server 
#karena revolte menuju ke switch melalui eth0
interfaces = “eth0”
service isc-dhcp-server start
<br>
nano /etc/dhcp/dhcpd.conf
``` 
tambahkan script berikut :
- SchwerMountain
```bash
subnet 10.20.0.128 netmask 255.255.255.128  {
    range 10.20.0.130 10.20.0.254;
    option routers 10.20.0.129;
    option broadcast-address 10.20.0.255;
    option domain-name-servers 10.20.0.6;
    default-lease-time 600;
    max-lease-time 7200;
}
```
- LaubHills
```bash
subnet 10.20.2.0 netmask 255.255.254.0 {
    range 10.20.2.2 10.20.3.254;
    option routers 10.20.2.1;
    option broadcast-address 10.20.3.255;
    option domain-name-servers 10.20.0.6;
    default-lease-time 600;
    max-lease-time 7200;
}
```
- TurkRegion
```bash
subnet 10.20.8.0 netmask 255.255.248.0 {
    range 10.20.8.2 10.20.15.254;
    option routers 10.20.8.1;
    option broadcast-address 10.20.15.255;
    option domain-name-servers 10.20.0.6;
    default-lease-time 600;
    max-lease-time 7200;
}
```
- GrobeForest
```bash
subnet 10.20.4.0 netmask 255.255.252.0 {
    range 10.20.4.2 10.20.7.254;
    option routers 10.20.4.1;
    option broadcast-address 10.20.7.255;
    option domain-name-servers 10.20.0.6;
    default-lease-time 600;
    max-lease-time 7200;
}
```
- Revolte -> Fern
```bash
subnet 10.20.0.0 netmask 255.255.255.252 {
    option routers 10.20.0.1;
}
```
```bash
service isc-dhcp-server restart
service isc-dhcp-server status
```
lalu pada router Himmel, Fern, dan Heiter, lakukan :
```bash
SERVERS="10.20.0.2"  
INTERFACES=" eth0 eth1 eth2"
OPTIONS=
```
service isc-dhcp-relay restart

# **DHCP Client :** 
pada : <br>
- SchwerMountain
- LaubHills
- TurkRegion
- GrobeForest <br>
Isi pada ```bash nano /etc/network/interfaces``` :
```bash
auto eth0
iface eth0 inet dhcp
```
lalu hapus konfigurasi statis yang ada address, netmask, gateway yang lama. <br>
Hasilnya akan terlihat seperti ini :
|      TurkRegion     |   SchwerMountain   |
| ------------------- | ------------------ |
|![Turk](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/cccf65cb-73cd-4f34-96c3-49aabec9cb2c)   | ![Schwer](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/192363eb-af4a-458e-94b8-370692a094d5) | 

|     LaubHills     |    GrobeForest    |
| ----------------- | ----------------- |
|![Laub](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/a7d14d31-0723-4f0e-b557-b57811900737)   | ![Grobe](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/a73864d7-3a83-4151-a8d1-73e2ba4875de) | 

# **DNS SERVER : Richter** 
```bash
apt-get clean
apt-get update
apt-get install bind9 -y
konfigurasi IP Forward :
/etc/bind/named.conf.options
```
![dns_server](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/bf8b1f69-f67d-4ce4-bf2a-8fcb65076454)
<br>
service bind9 restart

# **WEB SERVER (SEIN & STARK) :** 
```bash
apt-get clean
apt-get update
apt-get install apache2 -y
service apache2 start
/etc/apache2/sites-available/000-default.conf
nano /var/www/html/index.php
<?php
	phpinfo();
?>
apt-get install libapache2-mod-php7.0
/etc/apache2/ports.conf
Tambahkan ‘Listen 443’
service apache2 restart
```
## **Soal Nomor 1**
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.<br>
<br>**Langkah Penyelesaian Soal 1 :** <br>
sebelum paket keluar dia pasti keluar dari foosha maka pakai -s 10.20.0.0/21
```bash
IPETH0="$(ip -br a | grep eth0 | awk '{print $NF}' | cut -d'/' -f1)"
iptables -t nat -A POSTROUTING -o eth0 -s 10.20.0.0/21 -j SNAT --to-source "$IPETH0"
```
**testing**
<br>
Ping google di SEIN <br>
* Sebelum :
<img width="295" alt="1 Before" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/fc11045f-b623-4780-b529-b1b9b4fe8ecb">
<br> 
* Sesudah :<br>
  Masukkan echo nameserver 192.168.122.1 > /etc/resolv.conf pada Sein
<img width="361" alt="2  after" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/e5c278ed-95a7-407f-9107-a0a8f0065ed5">
<br>

## **Soal Nomor 2**
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.<br>
<br>**Langkah Penyelesaian Soal 2 :** <br>
Karena kita akan mencoba antara Revolte-SchewerMountains maka di Revolte:
```bash
iptables -A INPUT -p tcp –-dport 8080 -j ACCEPT
iptables -A INPUT -p tcp -j DROP
iptables -A INPUT -p udp -j DROP
```
<br>

**testing**
<br>
Uji menolak tcp dan udp : <br>
<img width="220" alt="1r" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/33306c71-6ed4-459f-96e5-475d6f0125cd">
<br>
<img width="139" alt="1rr" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/83f91f30-ccff-40f6-8e82-f0123140b170">
<br>
<img width="226" alt="2r" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/146612de-ccce-4926-8fd1-05674fd8e958">
<br>
<img width="133" alt="2rr" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/1d19cad2-3ec4-4982-87c2-4c2995af3900">
<br>
Uji hanya menerima tcp port 8080 : <br>
<img width="148" alt="3a" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/747c16df-4e56-42cb-b452-dc856852b1ff">
<br>
<img width="220" alt="3aa" src="https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/d68189e1-4499-4a9a-9cf7-c691f0c843b2">

## **Soal Nomor 3**
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.<br>
<br>**Langkah Penyelesaian Soal 3 :** <br>
Lakukan di Revolte atau Richter 
```bash
iptables -A INPUT -p icmp --icmp-type echo-request -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
**testing**
![3_1](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/4a7e0647-d074-48a1-895f-00ec90e9a631)
![3_2](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/e70dce84-70f9-44bf-905a-3f86be30a2ba)
![3_3](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/e0ed8a29-64bb-4eff-a8b9-bd99c4136b90)
![3_4](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/6109b068-1685-4e42-9ed4-7fd67aae251c)

## **Soal Nomor 4**
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.<br>
<br>**Langkah Penyelesaian Soal 4 :** <br>
* port 22 (port default SSH) dan Protokol yang biasanya digunakan untuk koneksi SSH
* Karena IP client akan selalu berganti sesuai yang diberikan oleh DHCP Server, maka lakukan di Sein atau Stark :
```bash
iptables -A INPUT -p tcp --dport 22 -s 10.20.x.x -j ACCEPT 
iptables -A INPUT -p tcp --dport 22 -j DROP
```
**testing**
<br>
* berhasil <br>
![4b](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/3a72c184-671a-42a9-b54c-3880693ac446)
![4bb](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/85d86b58-517b-4761-9577-ad51aa29e4c5)
* gagal <br>
![4g](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/16aa868d-9e5c-4106-938a-5807211c765b)
![4gg](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/b0925bd5-bc9f-4450-95ce-097e7f1ede51)

## **Soal Nomor 5**
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.<br>
<br>**Langkah Penyelesaian Soal 5 :** <br>
Lakukan di Sein atau Stark : 
```bash
iptables -A INPUT -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 08:00 --timestop 16:00 -j ACCEPT
iptables -A INPUT -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 08:00 --timestop 16:00 -j ACCEPT
iptables -A INPUT -j REJECT
```
**Testing**
<br>
date -s "19 DEC 2023 14:00:00" <br>
![5_1](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/cc2b2952-ed26-4c22-af7e-5058c1092f0c)
![5_11](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/5a38ff70-285c-4409-9f90-38fc3a0ae1ad)
<br>
date -s "19 DEC 2023 18:00:00" <br>
![5_2](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/edd62869-a8df-4c40-a76f-fdedf2a9e06d)
![5_22](https://github.com/lalaladi/Jarkom-Modul-5-B23/assets/90541607/1baba45a-ed65-46b6-8fae-99c214b51268)
