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
<br>
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

# **VLSM Testing** 
| Aura - A1                 | Aura - A12   | Aura - A4           |
| ------------------------- | ------------ | ------------------- |
|![ping A1](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/1a1d18c0-5265-4f04-8ec7-ad8aa9a4b123)   | ![ping A2](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/77eb6a31-f560-497c-a8f7-4a4a4b361c3b) | ![ping A4](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/57fc4538-4922-4b7d-be29-71448ff0244e) |

| Aura - A7                 | Aura - A8  | Aura - A11          |
| ------------------------- | ---------- | ------------------- |
| ![ping A7](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/3c4ce0af-da4e-4425-8c84-1e2bb3042741)  | ![ping A8](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/ca4bf93e-9f36-40a7-a9b5-aeef65f13990) | ![ping A11](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/4d1a828f-c1ac-4aac-ab2a-b10d5a270cd0) |
                                                      
| Aura - A13                | Aura - A16 | Aura - A17          |
| ------------------------- | ---------- | ------------------- |
| ![ping A13](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/ff29a65c-629c-4108-b86c-7f18eb4f93cf)  | ![ping A16](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/6802a251-c2de-44c4-8dd8-7010aa9530a7) | ![ping A17](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/4635bd3d-8062-4fcf-ad93-ddd2af1de851) |

| Aura - Switch 9           | Frieren - Lugner  |
| ------------------------- | ----------------- |
| ![ping Switch 9](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/41a2f3db-2c85-487e-bcb7-e4018d977b3b)  | ![ping Frieren - Lugner](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/04e62753-e229-49c8-b003-febe0ffa2069)
 |
