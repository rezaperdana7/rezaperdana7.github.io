---
id: 1038
title: Menjalankan Modem Esia Max-D (Cyrus MC400) Di Linux
date: 2013-10-30T05:41:47+00:00
author: Reza Perdana
layout: post
guid: http://blog.rezaperdana.web.id/?p=1038
permalink: /menjalankan-modem-esia-max-d-cyrus-mc400-di-linux/
wp_review_location:
  - bottom
wp_review_color:
  - '#1e73be'
wp_review_fontcolor:
  - '#555555'
wp_review_bgcolor1:
  - '#e7e7e7'
wp_review_bgcolor2:
  - '#ffffff'
wp_review_bordercolor:
  - '#e7e7e7'
image: /wp-content/uploads/2013/10/rezaperdana.com_-88x88.jpg
categories:
  - REVIEW
tags:
  - linux
---
Berawal dari kerusakan yang tidak diketahui sebabnya, modem aha tipe olive saya yang merupakan generasi awal hingar bingarnya aha di dunia internet indonesia tidak dapat digunakan lagi. Sayang nih kartu aha saya udah terlanjur dipaket internet bulanan Rp 100000 untuk 7 GB. Akhirnya saya pinjam modem teman saya yang merknya cyrus MC400. Wah, tertolong juga akhirnya paket internet saya gak terbuang sia-sia.

Plug and play di windows memang tidak berlaku di linux. Pengalaman saya menggunakan modem aha tipe olive menjadi buktinya. Dengan konfigurasi singkat pada linux mint olivia modem olive sudah bisa digunakan, namun ternyata hal yang sama tidak berlaku bagi modem cyrus. Konfigurasi langsung lewat network manager tidak berlaku, mungkin disebabkan hardware cyrus MC400 ini belum terdaftar. Dan bukan linux namanya kalau hal ini tidak bisa diakali. Berikut langkah-langkah untuk menjalankan modem cyrus MC400 ini di linux (tested on linux mint olivia 🙂 )<!--more-->

1. Buka terminal dan masukkan command berikut untuk mengecek apakah modem kita terdeteksi sebagai usb

<pre>dmesg | tail</pre>

Bus Device dengan ID Vendor 15EB dan ID product 7152 adalah modem cyrus

2. Daftarkan device modem cyrus tersebut pada modeswitch

<pre class="prettyprint">sudo gedit /etc/usb_modeswitch.conf</pre>

Lalu copy script berikut

<pre class="prettyprint"># cyrus mc400 (evdo)
#
Vendor = 0x15eb
Product = 0x7152
TargetVendor = 0x15eb
targetProduct = 0x7152</pre>

3. Save, setelah itu buka file manager dengan akses root dan buatlah file baru pada direktori &nbsp;/etc/udev/rules.d/ dengan nama cyrus-mc400.rules sehingga terbentuk direktori baru /etc/udev/rules.d/cyrus-mc400.rules

4. Kembali ke terminal dan buka direktori yang baru dibuat tadi

<pre class="prettyprint">sudo gedit /etc/udev/rules.d/cyrus-mc400.rules</pre>

5. Copy script berikut

<pre class="prettyprint"># /etc/udev/rules.d/cyrus-mc400.rules
#
# Cyrus mc400 (EVDO)
#
SUBSYSTEM=="usb", SYSFS{idVendor}=="15eb",
SYSFS{idProduct}=="7152", RUN+="/usr/sbin/usb_modeswitch – vendor 0x15eb –product 0×7152 –message-content
5553424312345678c00000008000069f030000000000000000000000000000"</pre>

6. Save, selanjutnya kita injeksi parameter modem dengan modprobe

<pre class="prettyprint">sudo modprobe usbserial vendor=0x15eb product=0X7152</pre>

7. Install aplikasi wvdial

<pre class="prettyprint">sudo apt-get install wvdial</pre>

8. Lakukan konfigurasi wvdial

<pre class="prettyprint">sudo gedit /etc/wvdial.conf</pre>

9. Copy Script berikut

<pre class="prettyprint">[Dialer aha]
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0
Stupid Mode = 1
Modem Type = Analog Modem
Command Line = ATDT
ISDN = 0
New PPPD = yes
Phone = #777
Modem = /dev/ttyUSB0
Username = aha
Password = aha
Baud = 460800</pre>

10. Save, lalu coba kita koneksikan wvdial untuk mengaktifkan internet

<pre class="prettyprint">sudo wvdial aha</pre>

11. Sampai sini sudah selesai, jika ingin menambahkan launcher agar tidak perlu mengulang proses, jalnkan pada terminal

<pre class="prettyprint">gedit aha.sh</pre>

12. Copy script berikut

<pre class="prettyprint">/bin/bashsudo eject /dev/sr1sleep 2sudo modprobe usbserial vendor=0X15eb product=0X7152sleep 2sudo wvdial aha</pre>

13. Save dan kita ubah ekstensinya dengan command

<pre class="prettyprint">sudo chmod +x aha.sh</pre>

14. Jadi setiap akan memulai koneksi, jalankan perintah

<pre class="prettyprint">./aha.sh</pre>

Demikian langkah-langkah yang harus dilalui untuk menjalankan modem cyrus di linux. Selamat mencoba sobat 🙂

Referensi: <span style="text-decoration: underline;">http://xrdiscominblog.blogspot.com/</span>