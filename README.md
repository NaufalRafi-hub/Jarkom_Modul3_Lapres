# Jarkom_Modul3_Lapres
Laporan Resmi Praktikum Modul 3 Jaringan Komputer 2020  Kelompok C07 (0099 &amp; 0157)
# Pembahasan Jawaban
### No 1 membuat topologi jaringan

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_1.jpg)

cara :
+ rm kota sebelumnya yang ada di praktikum
+ menambahkan kota malang sebagai DNS server
+ kota Tuban sebagai DHCP server
+ kota Mojokerto sebagai Proxy server
+ menambahkan kota dalam klien, yaitu Sidoarjo, Gresik, Banyuwangi, Madiun
+ memory maisng-masing ktoa diset sesuai yang soal inginkan

### No 2 surabaya menjadi perantara ( DHCP Relay ) antara DHCP Server dan client.

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_2.jpg)

cara :
+ `apt-get install isc-dhcp-relay` dalam surabaya
+ nano `etc/default/isc-dhcp-relay`
+ menambahkan `SERVERS="10.151.77.68"` dalam DHCP relay forward
+ menambahkan `INTERFACES="eth1 eth2 eth3"` dalam interface DHCP relay request

### No 3 Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_3.1.jpg)
 
 cara:
+ `nano etc/default/isc-dhcp-server` dalam tuban
+ menambahkan `INTERFACEv4="eth0"`

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_3.2.jpg)

cara:
+ `nano etc/dhcp/dhcp.conf` dalam tuban
+ menambahkan `subnet 192.168.0.0 netmask 255.255.255.0 {
range 192.168.0.10 192.168.0.100;
range 192.168.0.110 192.168.0.200;
option routers 192.168.0.1;
option broadcast-address 192.168.0.255;
option domain-name-servers 10.151.77.66, 202.46.129.2;
default-lease-time 300;
max-lease-time 300;
}`
+ `service isc-dhcp-server restart`

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_3.3.jpg)

cara :
+ melakukan konfigurasi gresik dengan menulis `ifconfig`

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_3.4.jpg)

cara :
+ melakukan konfigurasi sidoarjo dengan menulis `ifconfig`

### No 4 Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_4.1.jpg)

cara :
+ `nano etc/dhcp/dhcp.conf` dalam tuban
+ mengubah range IP
+ menambahkan `subnet 192.168.0.0 netmask 255.255.255.0 {
range 192.168.1.50 192.168.1.70;
option routers 192.168.1.1;
option broadcast-address 192.168.1.255;
option domain-name-servers 10.151.77.66, 202.46.129.2;
default-lease-time 600;
max-lease-time 600;
}`
+ melakukan konfigurasi pada banyuwangi dan madiun dengan menulis `ifconfig`
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_4.2.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_4.3.jpg)

### No 5	Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_5.1.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_5.2.jpg)

cara :
+ `nano etc/dhcp/dhcp.conf` dalam tuban
+ mengubah domain-name-sercers
+ `10.151.77.66, 202.46.129.2`

### No 6	Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_6.1.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_6.2.jpg)

cara :
+ `nano etc/dhcp/dhcp.conf` dalam tuban
+ mengubah `default-lease-time` dan `max-lease-time` pada subnet 1 dan 3
+ pada subnet 1 ditulis `default-lease-time 300` (5menit)
+ pada subnet 3 ditulis `default-lease-time 600` (10menit)

### No 7	User autentikasi milik Anri

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_7.1.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_7.2.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_7.3.jpg)
cara :
+ `apt-get install squid` pada proxy server, yaitu Mojokerto
+ `service squid status`  untuk mengecek apakah squid sudah running
+ `apt-get install apache2-utils`
+ buat user dan passsword
+ `htpasswd -c /etc/squid/passwd userta_c07
inipassw0rdta_c07`
+ `nano etc/squid/squid.conf`
+ mengecek apakah sudah diganti `nano etc/squid/passwd
+ melakukan konfigurasi squid
+ `http_port 8080
visible_hostname mojokerto

auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Proxy
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive on
acl USERS proxy_auth REQUIRED
http_access deny !USERS`
+ `restart squid`
+ ubah proxy browser menjadi ip Mojokerto
+ coba buka website yang diinginkan

### No 8 setiap hari Selasa-Rabu pukul 13.00-18.00

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_8.2.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_8.1.jpg)
cara :
+ membuat file baru bernama acl.conf dalam folder squid
+ `nano etc/squid/acl.conf`
+ menambahkan isi acl.conf dengan
+ `acl WORK1 time TW 13:00-18:00`
+ simpan
+ buka file squid.conf
+ menambahkan konfigurasi
+ `http_access allow WORK1`

### No 9	setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00)

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_9.2.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_9.1.jpg)

cara :
+ buka file acl.conf dalam folder squid
+ `nano etc/squid/acl.conf`
+ menambahkan isi acl.conf dengan
+ `acl DEADLINE1 time TWH 21:00-24:00`
+ `acl DEADLINE2 time TWH 00:00-09:00`
+ simpan
+ buka file squid.conf
+ menambahkan konfigurasi
+ `http_access allow DEADLINE1`
+ `http_access allow DEADLINE2`

### No 10	mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_10.1.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_10.2.jpg)

+ buka file acl.conf
+ menambahkan `acl lan src all` dan `acl google dstdomain .google.com`
+ simpan
+ buka file squid.conf
+ menambahkan `deny_info http://monta.if.its.ac.id lan
http_reply_access deny google lan
http_access allow all`

### No 11	error page default squid

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_11.jpg)

cara :
+ download file yang diinginkan
+ menuliskan `wget 10.151.36.202/error403.tar.gz`
+ di extract `tar -xvf error403.tar.gz`
+ menuliskan `mv /usr/share/squid/errors/English/ERR_ACCESS_DENIED usr/share/squid/errors/English/ERR_ACCESS_DENIDE
cp -r ERR_ACCESS_DENIED /usr/share/squid/errors/English/ERR_ACCESS_DENIED`

### No 12	proxy cukup dengan mengetikkan domain janganlupa-ta.yyy.pw dan memasukkan port 8080

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_12.1.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_12.2.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_12.3.jpg)

cara :
+ menuliskan dalam kolom HTTP Proxy "janganlupa-ta.c07.pw" dengan port "8080"
+ masuk kedalam folder named.conf.local dalam malang, karena sebagai DNS Server
+ `nano etc/bind/named.conf.local`
+ menambahkan `zone "janganlupa-ta.c07.pw" {
type master;
file "/etc/bind/jarkom/janganlupa-ta.c07.pw";
}`
+ buka file janganlupa-ta.c07.pw
+ nano `etc/bind/jarkom/janganlupa-ta.c07.pw`
+ menambahkan IP malang
