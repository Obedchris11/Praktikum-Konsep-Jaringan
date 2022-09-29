## Nama:Obed christian s

## 3121600022/D4ITA

## Praktikum 5 - VLAN

### A. Pengertian VLAN

VLAN adalah subnetwork yang dapat mengelompokkan kumpulan perangkat pada jaringan area lokal fisik (LAN) yang terpisah. VLAN juga memudahkan administrator jaringan dalam mempartisi jaringan tunggal untuk diaktifkan sesuai dengan persyaratan fungsional dan keamanan sistem yang dimiliki.

## Kegunaan VLAN

- Untuk menyatukan lebih dari satu LAN
  Dengan VLAN, LAN bisa berkomunikasi satu sama lain dengan mudah. Misalnya suatu universitas memiliki banyak gedung dengan tiap gedung memiliki LAN-nya masing-masing.

- Mempermudah administrasi
  VLAN memiliki server terpusat yang bisa menjangkau keseluruhan penggunanya. Dengan adanya VLAN, seluruh komputer bisa dijangkau tanpa harus pergi secara fisik ke tempat lain. Server terpusat pada VLAN memudahkan kontrol terhadap jaringan sehingga keamaan pada VLAN lebih terjaga.

- Meningkatkan keamanan
  VLAN dengan server terpusat meningkatkan keamanan lalu lintas data. Hal ini karena semua komputer bisa dikontrol dari mulai pengaturan domain broadcast, firewall, hingga pengawasan akan gangguan-gangguan yang terjadi pada jaringan.

## Jenis-jenis VLAN dalam Switch

1. Default VLAN
   VLAN yang sudah ada semenjak switch diaktifkan dan secara otomatis dinamakan dengan VLAN1. Biasanya VLAN default tidak bisa diubah maupun dinonaktifkan.

2. Data VLAN
   Berdasarkan GeeksforGeeks, data VLAN yaitu VLAN yang digunakan untuk membagi seluruh jaringan menjadi dua kelompok. VLAN data hanya mengatur lalu lintas data yang dibuat oleh pengguna.

3. Native VLAN
   Native VLAN merupakan VLAN asli yang dapat diubah dan juga dinonaktifkan. Native VLAN juga tidak ditandai secara otomatis (untagged) saat diterima di port trunk.

4. Voice VLAN
   Voice VLAN adalah VLAN suara yang menggunakan IP voice over (VoIP). Seperti VLAN lainnya, voice VLAN dapat mengatur lalu lintas data secara terpisah dari VLAN lainnya.

5. Management VLAN
   Management VLAN adalah VLAN yang bertujuan untuk mengatur switch atau saklar. Management VLAN berfungsi mengatur switch seperti dalam pengawasan, manajemen bandwidth, dan pencatatan sistem.

## Cara kerja VLAN

Berikut adalah setail langkah demi langkah tentang cara kerja Virtual
Local Area Network :

- VLAN menghubungakan semua perangkat komputer dalam lebih dari satu LAN. VLAN menyediakan akses tautan data ke semua host komputer yang terhubung ke switch dan diberi ID yang sama.
  VLAN membuat domain broadcastnya sendiri, memisahkan jaringan fisik yang ada menjadi beberapa jaringan logis. Server VLAN mengatur bagaimana lalu lintas komunikasi berjalan, switch memastikan kemana data akan pergi dan proses selanjutnya dilakukan seperti LAN pada biasanya.

---

## Praktikum Pengoprasian VLAN

Yang pertama saya lakukan yaitu membuat topologi seperti pada gambar dibawah ini.

![topologi](https://i.postimg.cc/sxCWfvg9/Topologi.png)

Kemudian melakukan konfigurasi IP yang akan digunakan sebagai berikut:

| Device  | Interface | IP Address      | Gateway      |
| ------- | --------- | --------------- | ------------ |
| Router0 | vlan10    | 172.17.10.1/24  |              |
|         | vlan30    | 172.17.30.1/24  |              |
| pc0     | fa0/1     | 172.17.10.21/24 | 172.17.10.24 |
| pc1     | fa0/3     | 172.17.30.23/24 | 172.17.30.24 |

Setting VLAN Database pada Switch

![switch vlan config](https://i.postimg.cc/G2hN7mCK/VLAN-Conf-on-Switch.png)

Lalu mengubah settingan VLAN pada masing masing Connector Fa di dalam Switch. Tujuannya yaitu untuk menghubungkan jaringan dari 'Router 0' ke PC tujuan. PC0 terhubung ke Switch pada port 'Fa 0/1' yang memiliki 'VLAN 10' dan PC1 terhubung ke switch pada port 'Fa 0/2' yang memiliki akses 'VLAN 30'

- Fa 0/1

![Fa 0/1 on Switch](https://i.postimg.cc/s1FTrVtt/Fa1-on-Switch.png)

- Fa 0/2

![Fa 0/2 on Switch](https://i.postimg.cc/BZd362sG/Fa2-on-Switch.png)

- Fa 0/3

![Fa 0/3 on Switch](https://i.postimg.cc/xjbrWqmp/Fa3-on-Switch.png)

- Fa 0/4

![Fa 0/4 on Switch](https://i.postimg.cc/7h1Kqvwh/Fa4-on-Switch.png)

'VLAN 10' akan melalui port 'Gig 0/0' milik Router dan port 'Fa 0/3' milik Switch, sedangkan 'VLAN 30' akan melalui port 'Gig 0/1' milik router dan port 'Fa 0/4' milik Switch.

Konfigurasi Gig 0/0 & 0/1

- Gig 0/0

![config gi0/0](https://i.postimg.cc/ydjJKn2B/Gig0-on-Router.png)

- Gig 0/1

![config gi0/1](https://i.postimg.cc/59PHk7wS/Gig1-on-Router.png)

Setelah melakukan konfigurasi, langkah berikutnya yaitu melakukan testing dengan cara melakukan Ping melalui Command Prompt milik PC0 kemudian mengetikkan 'ping 172.17.30.23'. Maka akan menghasilkan output sebagai berikut.

![Ping PC0 - PC1](https://i.postimg.cc/hPWGYkXx/Ping-PC0-PC1.png)
