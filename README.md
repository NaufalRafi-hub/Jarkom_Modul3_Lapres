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
+ melakukan konfigurasi gresik

![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_3.4.jpg)

cara :
+ melakukan konfigurasi sidoarjo

### No 4 Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_4.1.jpg)

cara :
+ `nano etc/dhcp/dhcp.conf` dalam tuban
+ mengubah range IP, broadcast address, default lease time, dan max lease time
+ menambahkan `subnet 192.168.0.0 netmask 255.255.255.0 {
range 192.168.1.50 192.168.1.70;
option routers 192.168.1.1;
option broadcast-address 192.168.1.255;
option domain-name-servers 10.151.77.66, 202.46.129.2;
default-lease-time 600;
max-lease-time 600;
}`
+ melakukan konfigurasi pada banyuwangi dan madiun
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_4.2.jpg)
![alt text](https://github.com/NaufalRafi-hub/Jarkom_Modul3_Lapres/blob/main/imageprak3/img3_4.3.jpg)

