Obed christian s
3121600022

## Percobaan Static Routing

Pada percobaan ini, siapkan dulu topologi seperti pada gambar dibawah ini
![Topologi](https://i.postimg.cc/Gh2xfpf1/Topologi.png)

Lakukan konfigurasi IP yang akan digunakan sebagai berikut:

| Perangkat | Interface | IP Address     | Gateway     |
| --------- | --------- | -------------- | ----------- |
| PC0       | fa0       | 192.168.1.2/24 | 192.168.1.1 |
| PC1       | fa0       | 192.168.3.3/24 | 192.168.3.2 |
| Router0   | Gig0/1    | 192.168.1.1/24 |             |
|           | Gig0/0    | 192.168.2.1/24 |             |
| Router1   | Gig0/0    | 192.168.2.2/24 |             |
|           | Gig0/1    | 192.168.3.2/24 |             |

### IP Configuration PC0

![IPConfig](https://i.postimg.cc/bwfdtCkF/PC0.png)

### IP Configuration PC1

![IPConfig](https://i.postimg.cc/261Bwq6H/PC1.png)

### Router0

![Router0Gig0](https://i.postimg.cc/d1nwLnvp/Route0-Gig0.png)
![Router0Gig1](https://i.postimg.cc/RCsvmPgn/Route0-Gig1.png)

### Router1

![Router1Gig0](https://i.postimg.cc/fy026THC/Route1-Gig0.png)
![Router1Gig1](https://i.postimg.cc/L5LdjTMm/Route1-Gig1.png)

Selanjutnya konfigurasi router staticnya. berikut konfigurasi routing staticnya:

Router0

- ip route 192.168.3.0 255.255.255.0 192.168.2.2

Router1

- ip route 192.168.1.0 255.255.255.0 192.168.2.1

Konfigurasi router dilakukan untuk menentukan rute yang dapat dilalui oleh paket saat mencari tujuan dengan menggunakan jaringan yang sudah ada.

### Percobaan Ping PC0 - PC1

![ping](https://i.postimg.cc/kMxhFDbM/ping.png)

Setelah melakukan ping, terjadi RTO 2 kali pada ping pertama dan ping kedua disebabkan terjadinya arp pada saat broadcast domain antara PC-0 dengan router0 dan terjadi brodcast lagi pada saat ping kedua antara router0 an router1. pada ping ketiga baru terhubung langsung sebab proses arp sudah selesai.
