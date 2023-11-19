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
## **Soal Nomor 7**
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.
<br>
<br>**Langkah Penyelesaian Soal 7 :** <br>
Pada Lawine:
```bash
apt-get update && apt-get install nginx
apt-get install php7.3
service nginx status
mkdir /var/www/granz.channel.b23.com
```
nano /var/www/granz.channel.b23.com/index.php
```bash
<!DOCTYPE html>
<html>
<head>
    <title>Granz Channel Map</title>
    <link rel="stylesheet" type="text/css" href="css/styles.css">
</head>
<body>
    <div class="container">
        <h1>Welcome to Granz Channel</h1>
        <p><?php
            $hostname = gethostname();
            echo "Request ini dihandle oleh: $hostname<br>"; ?> </p>
        <p>Enter your name to validate:</p>
        <form method="POST" action="index.php">
            <input type="text" name="name" id="nameInput">
            <button type="submit" id="submitButton">Submit</button>
        </form>
        <p id="greeting"><?php
            if(isset($_POST['name'])) {
                $name = $_POST['name'];
                echo "Hello, $name!";
            }
        ?></p>
    </div>


    <script src="js/script.js"></script>
</body>
</html>
```
nano /var/www/granz.channel.b23.com/info.php
```bash
<?php
    phpinfo()
?>
```
mkdir /var/www/granz.channel.b23.com/js
nano /var/www/granz.channel.b23.com/js/script.js
```bash
document.addEventListener("DOMContentLoaded", function () {
    var nameInput = document.getElementById("nameInput");
    var submitButton = document.getElementById("submitButton");
    var greeting = document.getElementById("greeting");


    submitButton.addEventListener("click", function (event) {
        event.preventDefault();
        var name = nameInput.value;
        greeting.textContent = "Hello, " + name + "!";
    });
});
```
mkdir /var/www/granz.channel.b23.com/css
nano /var/www/granz.channel.b23.com/css/styles.css
```bash
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #f0f0f0;
}

.container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

h1 {
    color: #333;
}

p {
    color: #666;
}

input[type="text"] {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
}


button {
    background-color: #007BFF;
    color: #fff;
    border: none;
    padding: 10px 20px;
    cursor: pointer;
}

#greeting {
    font-weight: bold;
    color: #007BFF;
    margin-top: 20px;
}
```
```bash
nano /etc/nginx/sites-available/default
**Tambahkan pada bagian index :**
index index.html index.htm index.php;
**lalu uncomment beberapa bagian ini :**
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
#
#   # With php-fpm (or other unix sockets):
    fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
#   # With php-cgi (or other tcp sockets):
#   fastcgi_pass 127.0.0.1:9000;
}
```
```bash
 ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled
service php7.3-fpm start
service nginx restart
service php7.3-fpm restart
```

## **Soal Nomor 8**
Kepala suku dari Bredt Region memberikan resource server sebagai berikut:
Lawine, 4GB, 2vCPU, dan 80 GB SSD.
Linie, 2GB, 2vCPU, dan 50 GB SSD.
Lugner 1GB, 1vCPU, dan 25 GB SSD.
aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second.
 <br>
<br>**Langkah Penyelesaian Soal 8 :** <br>
Pada Eisen :
```bash
apt-get update
apt-get install nginx -y
service nginx start
nano /etc/nginx/sites-available/lb-rr
 # Default menggunakan Round Robin
 upstream worker {
 	server 10.20.3.3; #IP lawine
 	server 10.20.3.2; #IP linie
 	server 10.20.3.1; #IP lugner

 }

 server {
 	listen 80;

	server_name granz.channel.b23.com www.granz.channel.b23.com;

 	root /var/www/html;

    	index index.html index.htm index.nginx-debian.html;

    	

    	location / {
        proxy_pass http://worker;
    }
 }
 ```
 ```bash
ln -s /etc/nginx/sites-available/lb-rr /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default
service nginx restart
```
<br>Pada DNS Server :<br>
```bash
nano /etc/bind/jarkom/granz.channel.b23.com
Edit : 
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
@       IN      A       10.20.2.2         ;IP Eisen
www     IN      CNAME   granz.channel.b23.com.
@       IN      AAAA       ::1 
```
Lalu, service bind9 restart 
<br>
**Bukti : Jalankan Pengujian dengan Apache Benchmark (ab) pada Client Revolte**
```bash
ab -n 1000 -c 100 http://granz.channel.B03.com
```
![no 7](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/dbb9f82d-49d1-487f-98d5-5eca940ac0be) 

## **Soal Nomor 9**
Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
a. Nama Algoritma Load Balancer
b. Report hasil testing pada Apache Benchmark
c. Grafik request per second untuk masing masing algoritma. 
d. Analisis
<br>
<br>**Langkah Penyelesaian Soal 9 :** <br>
<br>
Pada Eisen :<br>
**lb-roundrobin**
```bash
nano /etc/nginx/sites-available/lb-rr
# Default menggunakan Round Robin
 upstream worker {
 	server 10.20.3.3; #IP lawine
 	server 10.20.3.2; #IP linie
 	server 10.20.3.1; #IP lugner

 }
 server {
 	listen 80;

	server_name granz.channel.b23.com www.granz.channel.b23.com;

 	root /var/www/html;

    	index index.html index.htm index.nginx-debian.html;

    	location / {
        proxy_pass http://worker;
    }
 }
 ```
**lb-leastconnection**
```bash
nano /etc/nginx/sites-available/lb-lc
 upstream worker {
	least_conn;
 	server 10.20.3.3; #IP lawine
 	server 10.20.3.2; #IP linie
 	server 10.20.3.1; #IP lugner

 }
 server {
 	listen 80;

	server_name granz.channel.b23.com www.granz.channel.b23.com;

 	root /var/www/html;

    	index index.html index.htm index.nginx-debian.html;

    	location / {
        proxy_pass http://worker;
    }
 }
 ```
**lb-IPhash**
```bash
nano /etc/nginx/sites-available/lb-ih
 upstream worker {
	ip_hash;
 	server 10.20.3.3; #IP lawine
 	server 10.20.3.2; #IP linie
 	server 10.20.3.1; #IP lugner

 }
 server {
 	listen 80;

	server_name granz.channel.b23.com www.granz.channel.b23.com;

 	root /var/www/html;

    	index index.html index.htm index.nginx-debian.html;

    	location / {
        proxy_pass http://worker;
    }
 }
 ```
**lb-generichash**
```bash
nano /etc/nginx/sites-available/lb-gh
 upstream worker {
	hash $request_uri consistent;
 	server 10.20.3.3; #IP lawine
 	server 10.20.3.2; #IP linie
 	server 10.20.3.1; #IP lugner

 }
 server {
 	listen 80;

	server_name granz.channel.b23.com www.granz.channel.b23.com;

 	root /var/www/html;

    	index index.html index.htm index.nginx-debian.html;

    	location / {
        proxy_pass http://worker;
    }
 }
 ```
```bash
ln -s /etc/nginx/sites-available/lb-rr /etc/nginx/sites-enabled
ln -s /etc/nginx/sites-available/lb-ih /etc/nginx/sites-enabled
ln -s /etc/nginx/sites-available/lb-gh /etc/nginx/sites-enabled
ln -s /etc/nginx/sites-available/lb-lc /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default
service nginx restart
```
Lalu, pada ketiga worker lakukan perintah : 
```bash
ab -n 200 -c 10 -g http://granz.channel.B03.com
```
- Round Robin<br>
![no 7](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/dbb9f82d-49d1-487f-98d5-5eca940ac0be) 
- Least Connection<br>
![least_Connection](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/2e429d44-278d-4a65-96cb-a3051efec785)
- Ip Hash<br>
![Ip_Hash](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/208062f8-0385-44cd-8247-4fc481e38aab)
- Generic Hash<br>
![Generic_Hash](https://github.com/lalaladi/Jarkom-Modul-2-B23-2023/assets/90541607/62893811-63b3-4775-9b70-e20608ce1176)
<br>
file output yang dihasilkan oleh Apache Benchmark (ab) saat melakukan pengujian :  <a href="https://docs.google.com/spreadsheets/d/19G_bxOU47g8Yfww7l2C0UedpdCG4sVTmMIL_JeLyRFE/edit#gid=0)https://docs.google.com/spreadsheets/d/19G_bxOU47g8Yfww7l2C0UedpdCG4sVTmMIL_JeLyRFE/edit#gid=0">File_Data</a>

## **Soal Nomor 10**
Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.
<br>
<br>**Langkah Penyelesaian Soal 10 :** <br>
Langsung saja kita jalankan perintah berikut pada Client Revolte : 
```bash
ab -n 1000 -c 100 http://granz.channel.B23.com
```
- 3 Worker
- 2 Worker
- 1 Worker

## **Soal Nomor 11**
Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/
<br>
<br>**Langkah Penyelesaian Soal 11 :** <br>
Pada Eisen, lakukan perintah berikut : 
```bash
mkdir /etc/nginx/rahasisakita
htpasswd -c /etc/nginx/rahasisakita/htpasswd netics
```
Dan masukkan passwordnya : **ajkb23**. Lalu tambahkan pada konfigurasi nginx : 
```bash
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/rahasisakita/htpasswd; 
```
service nginx restart<br>
**Bukti : pada Revolte**
lynx granz.channel.B03.com

## **Soal Nomor 12**
Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id. 
<br>
<br>**Langkah Penyelesaian Soal 12 :** <br>
Pada Eisen : <br>
nano /etc/nginx/sites-available/lb-granz
```bash
 upstream worker {
 	server 10.20.3.3; #IP lawine
 	server 10.20.3.2; #IP linie
 	server 10.20.3.1; #IP lugner
}
server {
    listen 80;
    server_name granz.channel.B23.com www.granz.channel.B23.com;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    location / {
        proxy_pass http://worker;
    }

 	location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    auth_basic "Restricted Content";
    auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;

 }
```
```bash
ln -s /etc/nginx/sites-available/lb-granz /etc/nginx/sites-enabled
service nginx restart
```
Bukti : <br>
lynx 10.20.2.2/its


## **Soal Nomor 13**
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168.
<br>
<br>**Langkah Penyelesaian Soal 13 :** <br>
Di Himmei kita fixed-in client terlebih dahulu yang memiliki IP sesuai seperti di soal  pada client. Kita pilih Client Richter : <br>
nano /etc/dhcp/dhcpd.conf
```bash
host Richter {
    hardware ethernet 96:05:97:2a:29:65;
    fixed-address 10.20.3.70;
}
service isc-dhcp-server restart
```
Selanjutnya, kita beralih ke Eisen (LB), edit konfigurasi sebagai berikut : <br>
nano /etc/nginx/sites-available/lb-granz
```bash
 upstream worker {
 	server 10.20.3.3; #IP lawine
 	server 10.20.3.2; #IP linie
 	server 10.20.3.1; #IP lugner
}
server {
    listen 80;
    server_name granz.channel.B23.com www.granz.channel.B23.com;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

  location / {
        allow 10.20.3.69;
        allow 10.20.3.70;
        allow 10.20.4.167;
        allow 10.20.4.168;
        deny all;
        proxy_pass http://worker;
    }

    location / {
        proxy_pass http://worker;
    }

 	location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    auth_basic "Restricted Content";
    auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;

 }
```
service nginx restart<br>
Bukti : lynx 10.20.2.2/its


## **Soal Nomor 14**
Semua data yang diperlukan, diatur pada Denken dan harus dapat diakses oleh Frieren, Flamme, dan Fern.
<br>
<br>**Langkah Penyelesaian Soal 14 :** <br>
Pada Denken : 
```bash
apt-get update
apt-get install mariadb-server -y
service mysql start
```
Karena database akan diakses oleh tiga worker, tambahkan konfigurasi berikut pada /etc/mysql/my.cnf
```bash
[client-server]

# Import all .cnf files from configuration directory
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/

[mysqld]
skip-networking=0
skip-bind-address
```
pada file /etc/mysql/mariadb.conf.d/50-server.cnf ubah [bind-address] menjadi 0.0.0.0 dan restart mysql.
Setelah itu lakukan konfigurasi mysql sebagai berikut: <br>
mysql -u root -p
```bash
DROP USER IF EXISTS 'kelompokB23'@'%';
DROP USER IF EXISTS 'kelompokB23'@'localhost';
CREATE USER 'kelompokb23'@'%' IDENTIFIED BY 'passwordb23';
CREATE USER 'kelompokb23'@'localhost' IDENTIFIED BY 'passwordb23';
CREATE DATABASE dbkelompokb23;
GRANT ALL PRIVILEGES ON *.* TO 'kelompokb23'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokb23'@'localhost';
FLUSH PRIVILEGES;
```
Untuk pembuktian, kita lakukan pada worker laravel sebagai berikut : 
```
apt-get update
apt-get install -y lsb-release ca-certificates apt-transport-https software-properties-common gnupg2
curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt-get update
apt-get install php7.3-mbstring php7.3-xml php7.3-cli php7.3-common php7.3-intl php7.3-opcache php7.3-readline php7.3-mysql php7.3-fpm php7.3-curl unzip wget -y
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/bin/composer
apt-get install git -y
git clone https://github.com/elshiraphine/laravel-simple-rest-api.git
composer install
```
Kemudian, jalankan perintah berikut agar database dapat terlihat : 
```bash
mariadb --host=10.20.2.1 --port=3306 --user=kelompokB23 --password=passwordB23 dbkelompokB23 -e "SHOW DATABASES;"
```

## **Soal Nomor 15**
Frieren, Flamme, dan Fern memiliki Riegel Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer
<br>
<br>**Langkah Penyelesaian Soal 15 :** <br>
Pada tiap worker Laravel : 
```
apt-get update
apt-get install php8.0-mbstring php8.0-xml php8.0-cli php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt-get install git -y
apt-get install git -y 
cd /var/www && git clone https://github.com/martuafernando/laravel-praktikum-jarkom 
cd /var/www/laravel-praktikum-jarkom && composer update
cp .env.example .env

echo 'APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=10.20.2.1
DB_PORT=3306
DB_DATABASE=dbkelompokb23
DB_USERNAME=kelompokb23
DB_PASSWORD=passwordb23

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"' > /var/www/laravel-praktikum-jarkom/.env
cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
cd /var/www/laravel-praktikum-jarkom && php artisan config:cache
cd /var/www/laravel-praktikum-jarkom && php artisan migrate
cd /var/www/laravel-praktikum-jarkom && php artisan db:seed
cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
cd /var/www/laravel-praktikum-jarkom && php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```
Setelah berhasil, lanjutkan dengan konfigurasi nginx berikut : <br>
nano /etc/nginx/sites-available/riegel
```bash
    server {
    listen [SPECIFIC-PORT];

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
      include snippets/fastcgi-php.conf;
      fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/riegel_error.log;
    access_log /var/log/nginx/riegel_access.log;
}
```
Atur port untuk masing-masing worker sebagai berikut:<br>
10.20.4.1 = 8001	;Frieren 
<br>
10.20.4.2 = 8002	;Flamme
<br>
10.20.4.3 = 8003	;Fern

```bash
ln -s /etc/nginx/sites-available/riegel /etc/nginx/sites-enabled/riegel
rm /etc/nginx/sites-enabled/default
service php8.0-fpm start
service php8.0-fpm restart
service nginx restart
```
Bukti : pada masing-masing worker<br>
lynx http://10.20.4.1:8001
<br>
lynx http://10.20.4.2:8002
<br>
lynx http://10.20.4.3:8003

**Soal**
<br>
Riegel Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada grimoire.
## **Nomor 16**
POST /auth/register
<br>
<br>**Langkah Penyelesaian Soal 16 :** <br>
Pada Sein : <br>
nano  register.json
```bash
{
  "username": "kelompokB23",
  "password": "passwordB23",
}
```
Kita menggunakan file .json sebagai testing endpoint POST /auth/register yang dapat membantu dalam otomatisasi proses.
Bukti : Pada client Sein, jalankan perintah apache benchmark berikut 
```bash
ab -n 100 -c 10 -p register.json -T application/json http://10.20.4.3:8003/api/auth/register
```

## **Nomor 17**
POST /auth/register
<br>
<br>**Langkah Penyelesaian Soal 17 :** <br>
Masih di Sein : <br>
nano login.json
```bash
{
  "username": "kelompokB23",
  "password": "passwordB23"
} 
```
jalankan saja perintah : 
```bash
ab -n 100 -c 10 -p login.json -T application/json http://10.20.4.3:8003/api/auth/login
```

## **Nomor 18**
GET /me
<br>
<br>**Langkah Penyelesaian Soal 18 :** <br>
Di Sein : 
```bash
curl -X POST -H "Content-Type: application/json" -d @login.json http://10.20.4.3:8003/api/auth/login > get_token.txt

token=$(cat get_token.txt | jq -r '.token')
```
Bukti di Sein : 
```bash
ab -n 100 -c 10 -H "Authorization: Bearer $token" http://10.20.4.3:8003/api/me
```

## **Soal Nomor 19**
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur Riegel Channel maka implementasikan Proxy Bind pada Eisen untuk mengaitkan IP dari Frieren, Flamme, dan Fern.
<br>
<br>**Langkah Penyelesaian Soal 19 :** <br>
Pada Eisen, lakukan konfigurasi nginx berikut : <br>
nano /etc/nginx/sites-available/from_laravel
```bash 
echo 'upstream worker {
    server 10.20.4.1:8001;
    server 10.20.4.2:8002;
    server 10.20.4.3:8003;
}

server {
    listen 80;
    server_name riegel.canyon.B23.com www.riegel.canyon.B23.com;

    location / {
        proxy_pass http://worker;
    }
} ' > /etc/nginx/sites-available/from_laravel
```
```bash

ln -s /etc/nginx/sites-available/from_laravel /etc/nginx/sites-enabled

service nginx restart
```
Bukti : Di Sein
```bash
ab -n 100 -c 10 -p login.json -T application/json http://www.riegel.canyon.B23.com/api/auth/login
```

## **Soal Nomor 20**
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Frieren, Flamme, dan Fern. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada Grimoire.
<br>
<br>**Langkah Penyelesaian Soal 20 :** <br>
Untuk melakukan testing, pada masing-masing worker siapkan script berikut :
<br> 
Script Pertama<br> 
nano /etc/php/8.0/fpm/pool.d/www.conf
```bash
[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 10
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3
```
service php8.0-fpm restart
**Bukti : **

Script Kedua<br>
nano /etc/php/8.0/fpm/pool.d/www.conf
```bash
[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 25
pm.start_servers = 5
pm.min_spare_servers = 3
pm.max_spare_servers = 10
```
service php8.0-fpm restart<br>
**Bukti : **

Script Ketiga<br>
nano /etc/php/8.0/fpm/pool.d/www.conf
```bash
[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 75
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 20
```
service php8.0-fpm restart

## **Soal Nomor 21**
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Eisen. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second.
<br>
<br>**Langkah Penyelesaian Soal 21 :** <br>
Pada Eisen : 
nano /etc/nginx/sites-available/from_laravel
```bash 
upstream worker {
least_conn;
    server 10.20.4.1:8001;
    server 10.20.4.2:8002;
    server 10.20.4.3:8003;
}

server {
    listen 80;
    server_name riegel.canyon.B23.com www.riegel.canyon.B23.com;

    location / {
        proxy_pass http://worker;
    }
}
```
service nginx restart<br>
**Bukti : **
<br>
Di Sein, kita gunakan script terakhir
```bash
ab -n 100 -c 10 -p login.json -T application/json http://www.riegel.canyon.B23.com/api/auth/login
```
