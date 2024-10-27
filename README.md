# Jarkom-Modul-3-IT01-2024


## ***KELOMPOK IT 01***
| Nama      | NRP         |
  |-----------|-------------|
  | Aras Rizky Ananta| 5027221053   |
  | Hasan | 5027231073  |  

### Konfigurasi Awal
#### Prefix IP IT01
`10.64`

### Topologi Soal
#### Contoh
![image](https://github.com/user-attachments/assets/1e4e926e-82c5-40c7-ab21-b73cacbf306a)

#### Hasil Pembuatan Topologi IT01
![image](https://github.com/user-attachments/assets/7c451546-1dc4-4da8-b5c7-507be282ed5c)



## Setup Awal:
### Paradis
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.64.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
  address 10.64.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.64.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 10.64.4.1
	netmask 255.255.255.0
 
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.64.0.0/16
```

## nodes

Annie:
```
auto eth0
iface eth0 inet static
	address 10.64.1.2
	netmask 255.255.255.0
	gateway 10.64.1.1
```

Bertholdt: 
```
auto eth0
iface eth0 inet static
	address 10.64.1.3
	netmask 255.255.255.0
	gateway 10.64.1.1
```

Reiner: 
```
auto eth0
iface eth0 inet static
	address 10.64.1.4
	netmask 255.255.255.0
	gateway 10.64.1.1
```


Zeke:
```
auto eth0
iface eth0 inet static
	address 10.64.1.5
	netmask 255.255.255.0
	gateway 10.64.1.1
```

Armin: 
```
auto eth0
iface eth0 inet static
	address 10.64.2.2
	netmask 255.255.255.0 
gateway 10.64.2.1
```

Eren: 
```
auto eth0
iface eth0 inet static
	address 10.64.2.3
	netmask 255.255.255.0
	gateway 10.64.2.1
```

Mikasa: 
```
auto eth0
iface eth0 inet static
	address 10.64.2.4
	netmask 255.255.255.0
	gateway 10.64.2.1
```

Erwin:  
```
auto eth0
iface eth0 inet static
	address 10.64.2.5
	netmask 255.255.255.0
	gateway 10.64.2.1
```

Beast:
```
auto eth0
iface eth0 inet static
	address 10.64.3.2
	netmask 255.255.255.0
	gateway 10.64.3.1
```

Colossal: 
```
auto eth0
iface eth0 inet static
	address 10.64.3.3
	netmask 255.255.255.0
	gateway 10.64.3.1
```

Warhammer: 
```
auto eth0
iface eth0 inet static
	address 10.64.3.4
	netmask 255.255.255.0
	gateway 10.64.3.1
```

Fritz: 
```
auto eth0
iface eth0 inet static
	address 10.64.4.2
	netmask 255.255.255.0
	gateway 10.64.4.1
```

Tybur: 
```
auto eth0
iface eth0 inet static
	address 10.64.4.3
	netmask 255.255.255.0
	gateway 10.64.4.1
```

Depedencies: 
### Paradis (DHCP Relay)
```
apt-get update
apt-get install isc-dhcp-relay -y
```
### Tybur (DHCP Server)
```
apt-get update
apt-get install isc-dhcp-server -y
```
### Fritz (DNS Server)
```
apt-get update
apt-get install bind9 -y
```
### Beast dan Colossal (Load Balancer)
```
apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y
```
### Warhammer (Database Server)
```
apt-get update
apt-get install mariadb-server -y
```
### Annie, Bertholdt, Reiner (Laravel Worker)
```
apt-get update
apt-get install mariadb-server -y
```
### Armin, Eren, Mikasa (PHP Worker)
```
```
### Zeke dan Erwin (Client)
```
apt-get update
apt-get install lynx -y
apt-get install htop -y
apt-get install apache2-utils -y
apt-get install jq -y
```

## No.0
Pulau Paradis telah menjadi tempat yang damai selama 1000 tahun, namun kedamaian tersebut tidak bertahan selamanya. Perang antara kaum Marley dan Eldia telah mencapai puncak. Kaum Marley yang dipimpin oleh Zeke, me-register domain name marley.yyy.com untuk worker Laravel mengarah pada Annie. Namun ternyata tidak hanya kaum Marley saja yang berinisiasi, kaum Eldia ternyata sudah mendaftarkan domain name eldia.yyy.com untuk worker PHP (0) mengarah pada Armin.

0.	Buat script di fritz
   
```
apt-get update
apt-get install bind9 -y

forward="options {
directory \"/var/cache/bind\";
forwarders {
  	   192.168.122.1;
};

allow-query{any;};
listen-on-v6 { any; };
};
"
echo "$forward" > /etc/bind/named.conf.options

echo "zone \"marley.it01.com\" {
	type master;
	file \"/etc/bind/jarkom/marley.it01.com\";
};

zone \"eldia.it01.com\" {
	type master;
	file \"/etc/bind/jarkom/eldia.it01.com\";
};
" > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

riegel="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    marley.it01.com. root.marley.it01.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    marley.it01.com.
@       IN    A    10.64.1.2
"
echo "$riegel" > /etc/bind/jarkom/marley.it01.com

granz="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    eldia.it01.com. root.eldia.it01.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    eldia.it01.com.
@       IN    A    10.64.2.2
"
echo "$granz" > /etc/bind/jarkom/eldia.it01.com

service bind9 restart



echo “nameserver 192.168.122.1” >> /etc/resolv.conf
```


## No.1-5
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

Jauh sebelum perang dimulai, ternyata para keluarga bangsawan, Tybur dan Fritz, telah membuat kesepakatan sebagai berikut:
1. Semua Client harus menggunakan konfigurasi ip address dari keluarga Tybur (dhcp).
2. Client yang melalui bangsa marley mendapatkan range IP dari [prefix IP].1.05 - [prefix IP].1.25 dan [prefix IP].1.50 - [prefix IP].1.100 (2)
3. Client yang melalui bangsa eldia mendapatkan range IP dari [prefix IP].2.09 - [prefix IP].2.27 dan [prefix IP].2 .81 - [prefix IP].2.243 (3)
4. Client mendapatkan DNS dari keluarga Fritz dan dapat terhubung dengan internet melalui DNS tersebut (4)
5. Dikarenakan keluarga Tybur tidak menyukai kaum eldia, maka mereka hanya meminjamkan ip address ke kaum eldia selama 6 menit. Namun untuk kaum marley, keluarga Tybur meminjamkan ip address selama 30 menit. Waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit.
