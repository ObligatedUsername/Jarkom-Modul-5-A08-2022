# Jarkom-Modul-5-A08-2022

| **No** | **Nama**                   | **NRP**    |
| ------ | -------------------------- | ---------- |
| 1      | Dhani Rizki A. C. T. P.    | 5025201226 |
| 2      | Khariza Azmi Alfajira H.   | 5025201044 |
| 3      | Farros Hilmi Syafei        | 5025201012 |


## Topologi
![This is an image](https://github.com/ObligatedUsername/Jarkom-Modul-5-A08-2022/blob/master/assets/A.1.png)

## Setelah subnetting
![This is an image](https://github.com/ObligatedUsername/Jarkom-Modul-5-A08-2022/blob/master/assets/A.2.png)

## VLSM 
### Tabel Subnet 
![This is an image](https://github.com/ObligatedUsername/Jarkom-Modul-5-A08-2022/blob/master/assets/B.1.png)

### Tree
![This is an image](https://github.com/ObligatedUsername/Jarkom-Modul-5-A08-2022/blob/master/assets/B.2.png)

### Tabel Lengkap Subnet
![This is an image](https://github.com/ObligatedUsername/Jarkom-Modul-5-A08-2022/blob/master/assets/B.3.png)
 
### Routing
#### Konfigurasi IP (Router)
##### Strix:
```
auto eth1
iface eth1 inet static
    	address 10.3.7.145
    	netmask 255.255.255.252
auto eth2
iface eth2 inet static
    	address 10.3.7.149
    	netmask 255.255.255.252
 ```
##### Westalis:
```
auto eth0
iface eth0 inet static
    	address 10.3.7.146
    	netmask 255.255.255.252
auto eth1
iface eth1 inet static
    	address 10.3.7.129
    	netmask 255.255.255.248
auto eth2
iface eth2 inet static
    	address 10.3.7.1
    	netmask 255.255.255.128
auto eth3
iface eth3 inet static
    	address 10.3.0.1
    	netmask 255.255.252.0
 ```
##### Ostania:
```
auto eth0
iface eth0 inet static
    	address 10.3.4.1
    	netmask 255.255.254.0
auto eth1
iface eth1 inet static
    	address 10.3.7.150
    	netmask 255.255.255.252
auto eth2
iface eth2 inet static
    	address 10.3.6.1
    	netmask 255.255.255.0
auto eth3
iface eth3 inet static
    	address 10.3.7.137
    	netmask 255.255.255.248
 ```
#### Konfigurasi IP (Server)
##### Eden:
```
auto eth0
iface eth0 inet static
    	address 10.3.7.130
    	netmask 255.255.255.248
    	gateway 10.3.7.129
```
##### WISE:
```
auto eth0
iface eth0 inet static
    	address 10.3.7.131
    	netmask 255.255.255.248
    	gateway 10.3.7.129
 ```
##### Garden:
```
auto eth0
iface eth0 inet static
    	address 10.3.7.138
    	netmask 255.255.255.248
    	gateway 10.3.7.137
 ```
##### SSS:
```
auto eth0
iface eth0 inet static
    	address 10.3.7.139
    	netmask 255.255.255.248
    	gateway 10.3.7.137
```
#### Konfigurasi IP (Client)
```
auto eth0
iface eth0 inet dhcp
```
### Routing
##### Strix:
```
route add -net 10.3.7.128 netmask 255.255.255.248 gw 10.3.7.146
route add -net 10.3.7.0 netmask 255.255.255.128 gw 10.3.7.146
route add -net 10.3.0.0 netmask 255.255.252.0 gw 10.3.7.146
route add -net 10.3.6.0 netmask 255.255.255.0 gw 10.3.7.150
route add -net 10.3.7.136 netmask 255.255.255.248 gw 10.3.7.150
route add -net 10.3.4.0 netmask 255.255.254.0 gw 10.3.7.150
```
### Westalis:
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.3.7.145
```
### Ostania:
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.3.7.149
```

### IP Dinamis Pada Client menggunakan DHCP Server
##### WISE (DHCP Server):
```
- /etc/default/isc-dhcp-server
Tambahkan INTERFACES=”eth0”
```
```
- /etc/dhcp/dhcpd.conf
subnet 10.3.7.128 netmask 255.255.255.248 {
    	option routers 10.3.7.129;
}
```
```
subnet 10.3.7.0 netmask 255.255.255.128 {
    	range 10.3.7.2 10.3.7.63;
    	option routers 10.3.7.1;
    	option broadcast-address 10.3.7.127;
    	option domain-name-servers 10.3.7.130;
    	default-lease-time 600;
    	max-lease-time 7200;
}
 
subnet 10.3.0.0 netmask 255.255.252.0 {
    	range 10.3.0.2 10.3.2.189;
    	option routers 10.3.0.1;
    	option broadcast-address 10.3.3.255;
    	option domain-name-servers 10.3.7.130;
    	default-lease-time 600;
    	max-lease-time 7200;
}
 
subnet 10.3.4.0 netmask 255.255.254.0 {
    	range 10.3.4.2 10.3.5.0;
    	option routers 10.3.4.1;
    	option broadcast-address 10.3.5.255;
    	option domain-name-servers 10.3.7.130;
    	default-lease-time 600;
    	max-lease-time 7200;
}
 
subnet 10.3.6.0 netmask 255.255.255.0 {
    	range 10.3.6.2 10.3.6.201;
    	option routers 10.3.6.1;
    	option broadcast-address 10.3.6.255;
    	option domain-name-servers 10.3.7.130;
    	default-lease-time 600;
    	max-lease-time 7200;
}
```
##### Westalis, Strix, & Ostania:
```
- /etc/default/isc-dhcp-relay
Tambahkan SERVERS=”10.3.7.131” & INTERFACES”[Semua interface yang harus dihubungkan]”
```
Misal untuk Westalis, INTERFACES=”eth0 eth1 eth2 eth3”, karena eth0 terhubung menuju router Strix yang juga terhubung dengan router Ostania yang terhubung dengan client” yang perlu dicapai DHCP Server, eth1 untuk mengarah kembali menuju DHCP Server, dan eth2 & eth3 terhubung dengan client. <br/>
 
Setelah menambahkan konfigurasi pada DHCP Server dan Relay, jangan lupa untuk restart menggunakan ```service isc-dhcp-(server | relay) restart.``` <br/>
 
Konfigurasi iptables keluar di Strix tanpa menggunakan MASQUERADE
Konfigurasi network interface pada Strix:
auto eth0
iface eth0 inet static
    	address 192.168.122.2
    	netmask 255.255.255.252
    	gateway 192.168.122.1
 
Restart node Strix, lalu jalankan:
iptables -t nat -A POSTROUTING -s 10.3.0.0/21 -o eth0 -j SNAT –to-source 192.168.122.2
 
Juga jalankan berikut pada semua router dan server:
echo nameserver 192.168.122.1 > /etc/resolv.conf
 
Lalu untuk membuka koneksi dari luar untuk client, install bind9 pada Eden, lalu pada /etc/bind/named.conf.options tambahkan konfigurasi berikut:
	- hapus comment pada forwarders dan isinya, lalu ganti 0.0.0.0 dengan 192.168.122.1
	- comment dnssec-validation dan tambahkan allow-query { any; }; di bawahnya
 
Restart bind9 dengan service bind9 restart
 
Konfigurasi iptables drop untuk semua TCP & UDP dari luar topologi pada DHCP Server(WISE)
Di WISE, lakukan:
iptables -A INPUT -p tcp -i eth0 -j DROP
iptables -A INPUT -p udp -i eth0 -j DROP
 
DHCP dan DNS Server dibatasi agar hanya dapat menerima 2 koneksi ICMP secara bersamaan, selebihnya didrop
Di WISE & Eden, lakukan:
iptables -A INPUT -p icmp -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP
 
Akses Web Server hanya pada hari Senin - Jumat pada jam 07.00 - 16.00
Di Garden & SSS, lakukan:
iptables -A INPUT -m time --timestart 07:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -j REJECT
 
Setiap request dari client menuju Garden dengan port 80 didistribusikan secara bergantian pada SSS dan Garden secara berurutan, dan request dari client menuju SSS dengan port 443 akan didistribusikan seperti sebelumnya, tetapi pada Garden pertama, lalu SSS
Di Ostania, lakukan:
iptables -A PREROUTING -t nat -p tcp -d 10.3.7.138 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.3.7.139
iptables -A PREROUTING -t nat -p tcp -d 10.3.7.139 --dport 443 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.3.7.138
 
Logging semua paket yang didrop dengan standard syslog level
Di semua server dan router, tambahkan aturan iptables berikut sebelum aturan” lainnya:
Iptables -A INPUT -j LOG –log-level info –log-prefix “dropped packet: “
 
Lalu jalankan:
Service rsyslog start
 
–log-prefix tidak diperlukan, tapi dapat membantu memperjelas pesan untuk paket yang didrop di file log sistem
 
Log dapat dilihat di /var/log/kern.log atau /var/log/syslog, menggunakan program cat
