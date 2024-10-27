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
