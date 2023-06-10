# Laporan Konfigurasi SMTP Server

### Dosen pengampu: Dr. Ferry Astika Saputra. S.T, M. Sc.
### Kelas : 2 D4 Teknik Informatika A

### 1. Sandy Pradana Putra (3121600017)

### 2. Obed Christian S (3121600022)

### 3. Muhammad Rizqy F (3121600024)

### 4. Daffa Ridwan R (3121600027)

**SMTP** merupakan singkatan dari Simple Mail Transfer Protokol berfungsi sebagai protokol yang memfasilitasi dalam hal transfer <u>e-mail</u>. 

SMTP menggunakan 3 port, Port 25 digunakan untuk non SSL, port 587 untuk TLS dan 465 untuk SSL. Namun oleh sebagian ISP, port 25 telah ditutup karena dianggap berbahaya dengan tidak adanya encryption module yang digunakan.

Berikut cara konfigurasi SMTP Server pada Sistem Operasi Linux:
1. Menginstall package Postfix 


[![Screenshot-4711.png](https://i.postimg.cc/wB8pCGBf/Screenshot-4711.png)](https://postimg.cc/MnDNRtVV)

2. Mengisi nama email sistem

Fase ini akan dijalankan secara otomatis sehingga user akan diminta mengisi email system name.

```console
mail.kampus-04.takehome.com
```

3. Lalu konfigurasi file **main.cf** seperti berikut ini

[![Screenshot-4725.png](https://i.postimg.cc/8zNLV3dy/Screenshot-4725.png)](https://postimg.cc/8jX7RZ0W)

4. Konfigurasi Dovecot

Edit file konfigurasi `/etc/dovecot/dovecot.conf`.

```console
sudo nano /etc/dovecot/dovecot.conf
```

Uncomment dan edit baris berikut.

```console
# from
#listen = *, ::

# to
listen = *
```

Edit file konfigurasi `/etc/dovecot/conf.d/10-auth.conf`.

```console
sudo nano /etc/dovecot/conf.d/10-auth.conf
```

Uncomment dan ganti dari yes ke no.

```console
# connection is considered secure and plaintext authentication is allowed.
# See also ssl=required setting.
disable_plaintext_auth = no
```

Edit file konfigurasi `/etc/dovecot/conf.d/10-mail.conf`.

```console
sudo nano /etc/dovecot/conf.d/10-mail.conf
```

Uncomment pada `mail_location = maildir:~/Maildir` dan beri comment pada `mail_location = mbox:~/mail:INBOX=/var/mail/%u`.

Restart dovecot service.

```console
sudo systemctl restart dovecot
```

5. Menambahkan User Email

Tambahkan beberapa user dan password menggunakan perintah adduser yang akan digunakan untuk user email. Pada percobaan kali ini akan membuat dua user, yaitu user `b` dan user `c`. dengan perintah di bawah.

```console
sudo adduser b
```

```console
sudo adduser c
```

Restart postfix dan dovecot service.

```console
sudo systemctl restart postfix dovecot
```
