**LAPORAN PRAKTIKUM KONSEP JARINGAN**
> Kelas : 2 D4 IT A
>
> Tugas Kelompok BGP
> Nama : Muhammad Rizal (3121600007) dan Obed christian s (3121600022)
>

# A. TOPOLOGI

[![Topologi.png](https://i.postimg.cc/W1NcPdjv/Topologi.png)](https://postimg.cc/Yhss6qhn)

Topologi di atas terdiri dari 10 Router. R1 sebagai router utama yang akan terhubung ke AS Number yang lain. Area R2 menggunakan routing protocol RIP, area R3 menggunakan OSPF, area R4 menggunakan Static Routing, sementara untuk menghubungkan area R2, R3, dan R4 menggunakan routing protocol BGP yang terhubung ke router pusat yakni R1.

| Devices |   IP Address    | CIDR |     Network     | Interface |
| :-----: | :-------------: | :--: | :-------------: | :-------: |
|   R1    |   14.14.14.1    |  24  |   14.14.14.0    |  ether2   |
|         |   13.13.13.1    |  24  |   13.13.13.0    |  ether3   |
|         |   12.12.12.1    |  24  |   12.12.12.0    |  ether4   |
|   R2    |   12.12.12.2    |  24  |   12.12.12.0    |  ether1   |
|         |   27.27.27.2    |  24  |   27.27.27.0    |  ether2   |
|         |   28.28.28.2    |  24  |   28.28.28.0    |  ether3   |
|   R3    |   13.13.13.3    |  24  |   13.13.13.0    |  ether1   |
|         |   36.36.36.3    |  24  |   36.36.36.0    |  ether2   |
|         |   35.35.35.3    |  24  |   35.35.35.0    |  ether3   |
|   R4    |   14.14.14.4    |  24  |   14.14.14.0    |  ether1   |
|         |   41.41.41.4    |  24  |   41.41.41.0    |  ether2   |
|         |   49.49.49.4    |  24  |   49.49.49.0    |  ether3   |
|   R5    |   35.35.35.5    |  24  |   35.35.35.0    |  ether1   |
|         |   50.50.50.50   |  -   |   50.50.50.50   |    lo0    |
|   R6    |   36.36.36.6    |  24  |   36.36.36.0    |  ether1   |
|         |   60.60.60.60   |  -   |   60.60.60.60   |    lo0    |
|   R7    |   27.27.27.7    |  24  |   27.27.27.0    |  ether1   |
|         |   70.70.70.70   |  -   |   70.70.70.70   |    lo0    |
|   R8    |   28.28.28.8    |  24  |   28.28.28.0    |  ether1   |
|         |   80.80.80.80   |  -   |   80.80.80.80   |    lo0    |
|   R9    |   49.49.49.9    |  24  |   49.49.49.0    |  ether1   |
|         |   90.90.90.90   |  -   |   90.90.90.90   |    lo0    |
|   R10   |   41.41.41.10   |  24  |   41.41.41.0    |  ether1   |
|         | 100.100.100.100 |  -   | 100.100.100.100 |    lo0    |

# B. Ruang Lingkup Kerja

Dalam pratikum kali ini kelompok kami bertugas untuk mengatur router R9 yng menggunakan routing RIP sesuai area yang telah ditentukan. Kami melakukan konfigurasi routing tersebut dengan perintah sebagai berikut:
> tambah alamat addres untuk router 9 dan route ke r4 : 

> /interface bridge
> add name=lo0
> /ip address
> add address=49.49.49.9/24 interface=ether1 network=49.49.49.0
> add address=90.90.90.90 interface=lo0 network=90.90.90.90

>Setting RIP
>/ip route
>add distance=1 gateway=49.49.49.4

# C. Table Routing

![image](https://user-images.githubusercontent.com/89308108/204983540-20ab6444-326e-4be5-895b-9b9566e14e61.png)

Terlihat dengan perintah ip route print untuk melihat isi tabel routing, bahwa router R9 sudah terhubung dengan router R4 dan R10 yang menggunakan routing protocol RIP. Selain itu juga terhubung dengan router R2 yang menggunakan routing protocol BGP. Karena terhubung dengan R1 yang menggunakan protocol BGP pada router R2-R4, maka router R10 juga menerima table routing yang otomatis terhubung juga dengan R1.

# D. Test Koneksi

> dengan Router 4
![image](https://user-images.githubusercontent.com/89308108/204984160-808df404-cea3-4873-8569-c5c37c2bbc7e.png)

> dengan Router 10
![image](https://user-images.githubusercontent.com/89308108/204984262-edce2f92-905a-415a-8a56-0fa8a01d026d.png)

> dengan Router 8
![image](https://user-images.githubusercontent.com/89308108/204984524-8f78a293-ed2d-4509-b85f-5ba0e579e6da.png)

> tracert R10
![image](https://user-images.githubusercontent.com/89308108/204984911-ed24e4c1-2422-4713-9988-8efa13dacf2b.png)

> tracert R8
![image](https://user-images.githubusercontent.com/89308108/204985324-6439a64c-4b86-4e3f-8869-306fe46a4da0.png)

Gambar-gambar di atas merupakan test koneksi dengan perintah ping ke IP Address yang telah ditentukan.

Berhasil melakukan ping ke IP Address pada router R4 (14.14.14.4), R10 (41.41.41.10), berhasil dilakukan karena sudah memiliki routing tabel dengan tujuan ke network berikut.

Gagal melakukan ping ke IP Address pada router  R8 (28.28.28.8) dan yang lainnya karena tidak memiliki routing tabel dengan tujuan ke network di atas. Sepertinya masalah karena tidak menerima routing tabel dari R2 dan R4 secara penuh, hanya menerima routing tabel sebatas dengan router R1 saja.




