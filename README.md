# Jarkom-Modul-3-B23-2023
# **Praktikum Modul 3 Jaringan Komputer**
Berikut adalah Repository dari Kelompok B23 untuk pengerjaan Praktikum Modul 3. Dalam Repository ini terdapat daftar anggota kelompok, dokumentasi dan Penjelasan tiap soal, _Screenshot_, dan Kendala yang Dialami. 

# **Anggota Kelompok**
| Nama                      | NRP        | Kelas               |
| ------------------------- | ---------- | ------------------- |
| Armadya Hermawan Sarwono  | 5025211243 | Jaringan Komputer B |
| Dian Lies Seviona Dabukke | 5025211080 | Jaringan Komputer B |

# **Dokumentasi dan Penjelasan Soal**
Berikut adalah dokumentasi yang tiap soal dan penjelasan terkait perintah yang digunakan :
![Topologi](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/96f77bc2-ca19-445a-a4b2-1619bb58fad1)
Aura
```bash
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.20.1.0
	netmask 255.255.255.0
auto eth2
iface eth2 inet static
	address 10.20.2.0
	netmask 255.255.255.0
auto eth3
iface eth3 inet static
	address 10.20.3.0
	netmask 255.255.255.0
auto eth4
iface eth4 inet static
	address 10.20.4.0
	netmask 255.255.255.0
```
Himmei
```bash
auto eth0
iface eth0 inet static
	address 10.20.1.1
	netmask 255.255.255.0
	gateway 10.20.1.0
```
Heiter
```bash
auto eth0
iface eth0 inet static
	address 10.20.1.2
	netmask 255.255.255.0
	gateway 10.20.1.0
```
Denken
```bash
auto eth0
iface eth0 inet static
	address 10.20.2.1
	netmask 255.255.255.0
	gateway 10.20.2.0
```
Eisen
```bash
auto eth0
iface eth0 inet static
	address 10.20.2.2
	netmask 255.255.255.0
	gateway 10.20.2.0
```
Lugner
```bash
auto eth0
iface eth0 inet static
	address 10.20.3.1
	netmask 255.255.255.0
	gateway10.20.3.0
```
Linie
```bash
auto eth0
iface eth0 inet static
	address 10.20.3.2
	netmask 255.255.255.0
	gateway 10.20.3.0
```
Lawine
```bash
auto eth0
iface eth0 inet static
	address 10.20.3.3
	netmask 255.255.255.0
	gateway 10.20.3.0
```
Richter
```bash
auto eth0
iface eth0 inet dhcp
```
Revolte
```bash
auto eth0
iface eth0 inet dhcp
```
Sein (dibuat static untuk ping domain)
```bash
auto eth0
iface eth0 inet static
	address 10.20.4.4
	netmask 255.255.255.0
	gateway 10.20.4.0
```
Stark
```bash
auto eth0
iface eth0 inet dhcp
```
Frieren
```bash
auto eth0
iface eth0 inet static
	address 10.20.4.1
	netmask 255.255.255.0
	gateway 10.20.4.0
```
Flamme
```bash
auto eth0
iface eth0 inet static
	address 10.20.4.2
	netmask 255.255.255.0
	gateway 10.20.4.0
```
Fern
```bash
auto eth0
iface eth0 inet static
	address 10.20.4.3
	netmask 255.255.255.0
	gateway 10.20.4.0
```

## **Soal Nomor 1**
Kali ini, kalian diminta untuk melakukan register domain berupa riegel.canyon.yyy.com untuk worker Laravel dan granz.channel.yyy.com untuk worker PHP mengarah pada worker yang memiliki IP [prefix IP].x.1. <br>
<br>**Langkah Penyelesaian Soal 1 :** <br>
```bash
apt-get update
apt-get install bind9 -y
nano /etc/bind/named.conf.local
```
Isikan :
```bash
zone "riegel.canyon.b23.com" {
        type master;
        file "/etc/bind/jarkom/riegel.canyon.b23.com";
};
zone "granz.channel.b23.com" {
        type master;
        file "/etc/bind/jarkom/granz.channel.b23.com";
};
```
```bash
mkdir /etc/bind/jarkom
cp /etc/bind/db.local /etc/bind/jarkom/riegel.canyon.b23.com
nano /etc/bind/jarkom/riegel.canyon.b23.com
```
Isikan :
```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.b23.com. root.riegel.canyon.b23.com. (
                      2023111401          ; Serial
                          604800          ; Refresh
                           86400          ; Retry
                          2419200         ; Expire
                          604800 )        ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.b23.com.
@       IN      A       10.20.4.3        ;IP Fern
www     IN      CNAME   riegel.canyon.b23.com.
@       IN      AAAA       ::1 
```
```bash
cp /etc/bind/db.local /etc/bind/jarkom/granz.channel.b23.com
nano /etc/bind/jarkom/granz.channel.b23.com
```
Isikan :
```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.b23.com. root.granz.channel.b23.com. (
                   2023111401          ; Serial
                          604800          ; Refresh
                            86400          ; Retry
                         2419200         ; Expire
                         604800 )        ; Negative Cache TTL
;
@       IN      NS      granz.channel.b23.com.
@       IN      A       10.20.3.1         ;IP Lugner
www     IN      CNAME   granz.channel.b23.com.
@       IN      AAAA       ::1 
```
service bind9 restart
<br>
**Bukti : di Sein**
![ping riegel](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/c0b6a48b-e988-4068-86a5-e0245efd5713)
<br>

## **Soal Nomor 2**
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.<br>
<br>**Langkah Penyelesaian Soal 2 :** <br>
<ins>DHCP Relay</ins>
<br>
Kita lakukan konfigurasi DHCP Relay di router Aura dengan isi dari INTERFACES menyesuaikan jumlah interface output yang terhubung dengan client.
```bash
apt-get update
apt-get install isc-dhcp-relay -y
nano /etc/default/isc-dhcp-relay
```
Isi seperti gambar dibawah ini<br>
![conf DHCP Relay](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/3c193612-4b1f-4e99-b69d-e8fe047238c1)
```bash
service isc-dhcp-relay start
```
Selanjutnya, kita lakukan konfigurasi untuk mengaktifkan IP Forwarding :
```bash
nano /etc/sysctl.conf
**Isikan :** 
net.ipv4.ip_forward=1

service isc-dhcp-relay restart
```
<ins>DHCP Server</ins>
<br>
Lakukan konfigurasi pada DHCP Server yaitu Himmei, seperti berikut :
```bash
apt-get update
apt-get install isc-dhcp-server
nano /etc/default/isc-dhcp-server    
```
```bash
# Defaults for isc-dhcp-server initscript
# sourced by /etc/init.d/isc-dhcp-server
# installed at /etc/default/isc-dhcp-server by the maintainer scripts

#
# This is a POSIX shell fragment
#

# Path to dhcpd's config file (default: /etc/dhcp/dhcpd.conf).
#DHCPD_CONF=/etc/dhcp/dhcpd.conf

# Path to dhcpd's PID file (default: /var/run/dhcpd.pid).
#DHCPD_PID=/var/run/dhcpd.pid

# Additional options to start dhcpd with.
#       Don't use options -cf or -pf here; use DHCPD_CONF/ DHCPD_PID instead
#OPTIONS=""

# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
#       Separate multiple interfaces with spaces, e.g. "eth0 eth1".
INTERFACESv4="eth0"
```
lalu, nano /etc/dhcp/dhcpd.conf
```bash
subnet 10.20.1.0 netmask 255.255.255.0 {

}
subnet 10.20.2.0 netmask 255.255.255.0 {

}
subnet 10.20.4.0 netmask 255.255.255.0 {

}
subnet 10.20.3.0 netmask 255.255.255.0 {

}
```
service isc-dhcp-server restart

<ins>DNS Server</ins>
<br>
```bash
apt-get update
 apt-get install bind9 -y
```

## **Soal Nomor 3**
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 <br>
<br>**Langkah Penyelesaian Soal 3 :** <br>
pada Himmel, tambahkan :
```bash
nano /etc/dhcp/dhcpd.conf
subnet 10.20.3.0 netmask 255.255.255.0 {
    range 10.20.3.16 10.20.3.32;
    range 10.20.3.64 10.20.3.80;
    option routers 10.20.3.1;
    option broadcast-address 10.20.3.255;
    default-lease-time 600;
    max-lease-time 7200;
}
service isc-dhcp-server restart
```
**Bukti : lakukan ip a pada client di switch3**
![switch3](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/cf8557f3-a9d0-4fff-855c-9ba522382410)

## **Soal Nomor 4**
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 <br>
<br>**Langkah Penyelesaian Soal 4 :** <br>
```bash
nano /etc/dhcp/dhcpd.conf
**Tambahkan :**
subnet 10.20.4.0 netmask 255.255.255.0 {
    range 10.20.4.12 10.20.4.20;
    range 10.20.4.160 10.20.4.168;
    option routers 10.20.4.1;
    option broadcast-address 10.20.4.255;
    default-lease-time 600;
    max-lease-time 7200;
}
service isc-dhcp-server restart
```
**Bukti : lakukan ip a pada client di switch4**
![switch4](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/da1afa1d-9a7c-479f-9de3-cf789b2b21aa)

## **Soal Nomor 5**
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut<br>
<br>**Langkah Penyelesaian Soal 5 :** <br>
Pada Himmei (DHCP Server) atur option domain-name-servers menjadi DNS Heiter:
```bash
nano /etc/dhcp/dhcpd.conf
**Tambahkan :**
subnet 10.20.4.0 netmask 255.255.255.0 {
    range 10.20.4.12 10.20.4.20;
    range 10.20.4.160 10.20.4.168;
    option routers 10.20.4.1;
    option broadcast-address 10.20.4.255;
    option domain-name-servers 10.20.1.2;
    default-lease-time 600;
    max-lease-time 7200;
}

subnet 10.20.3.0 netmask 255.255.255.0 {
    range 10.20.3.16 10.20.3.32;
    range 10.20.3.64 10.20.3.80;
    option routers 10.20.3.1;
    option broadcast-address 10.20.3.255;
    option domain-name-servers 10.20.1.2;
    default-lease-time 600;
    max-lease-time 7200;
}
service isc-dhcp-server restart
```
Lakukan nano /etc/resolv.conf pada client di  switch3 dan switch4 apakah hasilnya sudah seperti, jika sudah seperti ini berarti pemberian nameserver berhasil<br>
![nameserver](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/39f3ec04-f2df-4fec-a652-8dfaf51ae92f)
<br>
Lalu pada Heiter (DNS Server), lakukan konfigurasi IP Forward : 
```bash
nano /etc/bind/named.conf.options
**Isikan :**
forwarders {
      192.168.122.1;
};

//=====================================================================$
// If BIND logs error messages about the root key being expired,
// you will need to update your keys.  See https://www.isc.org/bind-keys
//=====================================================================$
//dnssec-validation auto;
allow-query{any;};
auth-nxdomain no;    # conform to RFC1035
listen-on-v6 { any; };
service bind9 restart
```
**Bukti :ping google.com pada Client Richter**
![ping google](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/5810c996-6d83-4832-8213-c3c7913ec9a2)

## **Soal Nomor 6**
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit <br>
<br>**Langkah Penyelesaian Soal 6 :** <br>
Pada Himmel  :
```bash
nano /etc/dhcp/dhcpd.conf
**Edit:**
subnet 10.20.3.0 netmask 255.255.255.0 {
    range 10.20.3.16 10.20.3.32;
    option routers 10.20.3.1;
    option broadcast-address 10.20.3.255;
    option domain-name-servers 10.20.1.2;
    default-lease-time 180; //3 menit
    max-lease-time 5760; //96 menit 
}

subnet 10.20.4.0 netmask 255.255.255.0 {
    range 10.20.4.12 10.20.4.20;
    range 10.20.4.160 10.20.4.168;
    option routers 10.20.4.1;
    option broadcast-address 10.20.4.255;
    option domain-name-servers 10.20.1.2;
    default-lease-time 720; //12 menit
    max-lease-time 5760; //96 menit 
}
service isc-dhcp-server restart
```
