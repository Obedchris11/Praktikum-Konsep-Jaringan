# Laporan Konfigurasi Roundcube (Mail Server)

### Dosen pengampu: Dr. Ferry Astika Saputra. S.T, M. Sc.
### Kelas : 2 D4 Teknik Informatika A

### 1. Sandy Pradana Putra (3121600017)

### 2. Obed Christian S (3121600022)

### 3. Muhammad Rizqy F (3121600024)

### 4. Daffa Ridwan R (3121600027)


## Install Mariadb dan Roundcube

Install roundcube sebagai webmail yang akan digunakan oleh client, dan package mariadb yang nantinya akan digunakan sebagai database dari roundcube.

```console
sudo apt install mariadb-server roundcube
```

- Pilih `yes` untuk membuat database secara otomatis oleh roundcube

- Masukkan password database roundcube.

Edit file `/etc/roundcube/config.inc.php`.

```console
sudo nano /etc/roundcube/config.inc.php
```

Isikan default host dengan nama domain mail server.

```console
$config['default_host'] = 'mail.kampus-04.takehome.com';
```

Ganti smtp server dengan nama domain mail server.

```console
$config['smtp_server'] = 'mail.kampus-04.takehome.com';
```

Ganti smtp port dari 587 ke 25.

```console
$config['smtp_port'] = 25;
```

Kosongkan value dari smtp user.

```console
$config['smtp_user'] = '';
```

Kosongkan value dari smtp password.

```console
$config['smtp_pass'] = '';
```

Configure ulang roundcube (langkah ini bisa dilewati).

```console
sudo dpkg-reconfigure roundcube-core
```

Kosongkan karena kita tidak menggunakan tls.

[![Screenshot-4727.png](https://i.postimg.cc/KYzQgNcD/Screenshot-4727.png)](https://postimg.cc/872L2L67)

Pilih bahasa untuk roundcube.

[![Screenshot-4728.png](https://i.postimg.cc/d0krYStp/Screenshot-4728.png)](https://postimg.cc/B83X5pFB)

Pilih pada pilihan apache.

[![Screenshot-4729.png](https://i.postimg.cc/RFwt36tT/Screenshot-4729.png)](https://postimg.cc/7GYhdLmC)

Pilih yes untuk merestart web server.

[![Screenshot-4730.png](https://i.postimg.cc/MHDjDCdM/Screenshot-4730.png)](https://postimg.cc/K31zcHXx)

Edit apache config untuk memasukkan konfigurasi tambahan dari roundcube ke apache config.

```console
sudo nano /etc/apache2/apache2.conf
```

Tambahkan pada baris paling bawah.

```console
Include /etc/roundcube/apache.conf
```

Selanjutnya, masuk ke directory website apache dan tambahkan file baru untuk mail server.

```console
cd /etc/apache2/sites-available
sudo nano 000-default.conf
```

[![Screenshot-4731.png](https://i.postimg.cc/Cxyz8LFP/Screenshot-4731.png)](https://postimg.cc/rKJVXTRx)

Disable apache default config dan enable kan mail config.

```console
a2dissite 000-default.conf
a2ensite mail.conf
```

Restart apache service.

```console
systemctl restart apache2
```

# Testing

Selanjutnya buka web browser pada sisi client dan masukkan domain dari mail server, maka akan muncul interface dari roundcube. Lalu login menggunakan salah satu user yang telah dibuat.

Klik pada compose dan isikan pesan untuk user lainnya. Lalu klik send.

[![Whats-App-Image-2023-06-09-at-16-36-07.jpg](https://i.postimg.cc/Gmd9zLfX/Whats-App-Image-2023-06-09-at-16-36-07.jpg)](https://postimg.cc/xcp012nm)

Lalu lihat user penerima, maka akan muncul pesan yang dikirim.

[![Whats-App-Image-2023-06-09-at-16-35-40.jpg](https://i.postimg.cc/wBPqKgW8/Whats-App-Image-2023-06-09-at-16-35-40.jpg)](https://postimg.cc/ns4bBbb0)
