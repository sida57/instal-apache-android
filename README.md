# Instalasi Apache
## 📺 Video Instalasi: [sida57](https://www.youtube.com/@sida57)
## Pertama, kita akan menginstal paket PHP dan Apache menggunakan pkg. Buka Termux, lalu jalankan perintah berikut:
~~~
pkg install php-apache
~~~
Perintah ini akan mengunduh dan menginstal semua komponen yang diperlukan untuk menjalankan server web.

## Konfigurasi Apache

Setelah instalasi selesai, langkah selanjutnya adalah mengkonfigurasi Apache agar bisa mengenali file PHP dan menggunakan folder yang kita inginkan sebagai root direktori web. Gunakan editor teks nano untuk membuka file konfigurasi Apache:
~~~
nano -l $PREFIX/etc/apache2/httpd.conf
~~~
Dalam file tersebut, kamu perlu melakukan beberapa perubahan di baris-baris tertentu. Gunakan perintah Ctrl + W di nano untuk mencari baris-baris yang akan kita ubah.
- Mengatur ServerName
Cari baris ke-53 dan ubah menjadi:
~~~
ServerName localhost
~~~
Perintah ini menentukan nama server yang akan digunakan oleh Apache.
- Mengaktifkan Modul PHP
Cari baris ke-66 sampai 71. Pastikan baris-baris ini tidak diawali dengan tanda # (komentar). Baris-baris ini mengaktifkan modul PHP sehingga Apache bisa memproses file dengan ekstensi .php.
~~~
LoadModule mpm_prefork_module libexec/apache2/mod_mpm_prefork.so
LoadModule php_module libexec/apache2/libphp.so
<FilesMatch \.php$>9
SetHandler application/x-httpd-php
</FilesMatch>
~~~
- Mengubah DocumentRoot
Cari baris ke-249 dan 250, lalu ubah jalur DocumentRoot dan Directory ke direktori web yang akan kamu gunakan. Dalam contoh ini, kita akan menggunakan folder htdocs yang ada di direktori home Termux. Kamu bisa membuatnya jika belum ada.
DocumentRoot "/data/data/com.termux/files/home/htdocs"
~~~
<Directory "/data/data/com.termux/files/home/htdocs">
~~~
- Mengatur DirectoryIndex
Terakhir, cari baris ke-283 dan tambahkan index.php di samping index.html. Ini memastikan bahwa server akan mencari file index.php terlebih dahulu saat seseorang mengakses halaman utama.
~~~
DirectoryIndex index.html index.php
~~~
Setelah semua perubahan selesai, simpan file dengan menekan Ctrl + O, lalu Enter, dan keluar dari editor dengan Ctrl + X.
## Menjalankan dan Menghentikan Apache
Sekarang, web server sudah siap dijalankan. Buat folder htdocs terlebih dahulu, lalu jalankan Apache dengan perintah:
~~~
apachectl
~~~
Jika tidak ada pesan error, Apache sudah berjalan. Sekarang, buka browser di HP-mu dan akses alamat localhost:8080 untuk melihat apakah server sudah berfungsi dengan baik.
Untuk menghentikan web server, cukup jalankan perintah:
~~~
apachectl stop
~~~
Dengan langkah-langkah di atas, kamu sekarang sudah bisa menginstal, mengkonfigurasi, dan menjalankan web server Apache dengan dukungan PHP di Termux.

