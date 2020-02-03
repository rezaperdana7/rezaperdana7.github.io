---
id: 54
title: '[YII] Mengubah Default Nama Aplikasi'
date: 2018-02-21T10:09:46+00:00
author: Reza Perdana
layout: post
guid: https://rezaperdana.com/?p=54
permalink: /yii-2-mengubah-default-nama-aplikasi/
image: /wp-content/uploads/2018/02/yii2.jpg
categories:
  - PROGRAMMING
tags:
  - yii2
---
Assalamualaikum, _good morning!_

Kali ini saya akan share 1 masalah sederhana saat saya akan memulai membangun aplikasi menggunakan framework YII 2 dengan basic template

Hal pertama yang ingin saya ubah namun bingung dimana mengatur perubahannya adalah pada nama aplikasi yang defaultnya adalah &#8216;my application&#8217;

Setelah googling beberapa saat, akhirnya saya menemukan cara praktis untuk mengubahnya. Mari langsung kita mulai

<!--more-->

Masuk pada direktori aplikasi anda/config/web.php

Lihat pada baris keenam dan ketujuh yang sintaksnya

`$config = [<br />
'id' => 'basic',`

Lalu tambahkan sintaks berikut beserta nama aplikasi yang ingin digunakan

`'name' => 'Nama-aplikasi-anda',`

Sehingga menjadi seperti berikut. Sistem Informasi Jaringan &#8211; SIMJAR adalah aplikasi yang akan saya gunakan

<figure style="width: 508px" class="wp-caption aligncenter"><img class="size-medium" src="https://rusqjg.ch.files.1drv.com/y4mQe17IYvc3piNU1W_jFbAwZA4PD7MWhJfwZMeeUuJKgmzbw1hBejCltOyH53T6lTvx-i4yjQ0yfiKbxJWR0Q2x0mvhZ5a4ByA02uLc6FhuG7hvy5-OJBH5xSjRnKG-O8gZnbPHkDLhaNiMAkGowFTRN8-U_TEwSj9JJSRMbs8RUTnASsLlL8B4OryoNnNzxYat7-P_4XCV7NFYjUE07v2Wg?width=508&height=117&cropmode=none" width="508" height="117" /><figcaption class="wp-caption-text">Final sintaks mengubah nama aplikasi di YII 2</figcaption></figure>

<figure style="width: 1249px" class="wp-caption aligncenter"><img class="size-medium" src="https://rus8jg.ch.files.1drv.com/y4mZNAsKeZdKOAQ1u_Gd80fmu938MqRhgFeNQ_pUlr0sVe1obOLSDHvmF090flcnPbx0Pbcmt5E6iz171IBAJ456t3wDjTW-SbK3QDc7fWCLX-TXpDlGu-9dAPcEwgnCYw1ORgz0GM6pFti4Ep7Y_riemJA-rYZm_uyvJOfYN3J1avY7KBgRGWumOZ2gGBRUk8Zq_yBmCdXWjbbFSErGkH0fA?width=1249&height=416&cropmode=none" width="1249" height="416" /><figcaption class="wp-caption-text">Nama aplikasi sudah berubah 🙂</figcaption></figure>

Sekian untuk sharing session sederhana ini kawan-kawan, _**Have a nice day!**_

&nbsp;

&nbsp;