---
id: 1403
title: '[CODEIGNITER] Koneksi 2 Database Dalam 1 Aplikasi'
date: 2019-07-02T09:31:43+00:00
author: Reza Perdana
layout: post
guid: https://rezaperdana.com/?p=1403
permalink: /codeigniter-koneksi-2-database-dalam-1-aplikasi/
image: /wp-content/uploads/2019/07/Untitled-design-88x88.jpg
categories:
  - PROGRAMMING
tags:
  - codeigniter
  - database
  - php
---
Codeigniter memungkinkan kita untuk melakukan koneksi ke 2 database bahkan lebih disaat bersamaan. 2 database atau lebih tersebut juga tentu saja dapat berupa database yang berbeda platform, kita asumsikan saya database 1 adalah database mysqli (maria db) dengan nama db\_siswa lalu database 2 adalah database postgresql dengan nama db\_sekolah

Buka folder aplikasi tempat project kita berada, dalam hal ini project saya bernama CI-study. Buka Application/config/database.php. Lalu tambahkan source code berikut:

<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">//  Database default kita disable dahulu
// $db['default'] = array(
// 	'dsn'	=> '',
// 	'hostname' => '',
// 	'username' => '',
// 	'password' => '',
// 	'database' => '',
// 	'dbdriver' => 'mysqli',
// 	'dbprefix' => '',
// 	'pconnect' => FALSE,
// 	'db_debug' => (ENVIRONMENT !== 'production'),
// 	'cache_on' => FALSE,
// 	'cachedir' => '',
// 	'char_set' => 'utf8',
// 	'dbcollat' => 'utf8_general_ci',
// 	'swap_pre' => '',
// 	'encrypt' => FALSE,
// 	'compress' => FALSE,
// 	'stricton' => FALSE,
// 	'failover' => array(),
// 	'save_queries' => TRUE
// );

$db['con_mysqli'] = array(
	'dsn'	=> '',
	'hostname' => 'localhost',
	'username' => 'root',
	'password' => 'root',
	'database' => 'db_siswa',
	'dbdriver' => 'mysqli',
	'dbprefix' => '',
	'pconnect' => FALSE,
	'db_debug' => (ENVIRONMENT !== 'production'),
	'cache_on' => FALSE,
	'cachedir' => '',
	'char_set' => 'utf8',
	'dbcollat' => 'utf8_general_ci',
	'swap_pre' => '',
	'encrypt' => FALSE,
	'compress' => FALSE,
	'stricton' => FALSE,
	'failover' => array(),
	'save_queries' => TRUE
);

$db['con_postgre'] = array(
	'dsn'	=> '',
	'hostname' => 'localhost',
	'username' => 'postgres',
	'password' => 'postgres',
	'database' => 'db_sekolah',
	'dbdriver' => 'postgre',
	'dbprefix' => '',
	'pconnect' => FALSE,
	'db_debug' => (ENVIRONMENT !== 'production'),
	'cache_on' => FALSE,
	'cachedir' => '',
	'char_set' => 'utf8',
	'dbcollat' => 'utf8_general_ci',
	'swap_pre' => '',
	'encrypt' => FALSE,
	'compress' => FALSE,
	'stricton' => FALSE,
	'failover' => array(),
	'save_queries' => TRUE
);

</pre>

Pastikan host, username dan password sudah disesuaikan dengan profil database masing-masing. Save, lalu untuk memanggil masing-masing database untuk operasi CRUD (Create Read Update Delete) maka kita panggil dengan function berikut:

<pre class="EnlighterJSRAW" data-enlighter-language="php" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">function panggil_database()
    {
        $db_mysqli= $this->load->database('con_mysqli', TRUE); //  koneksi ke db_siswa mysqli
        $db_postgre = $this->load->database('con_postgre', TRUE); //  koneksi ke db_sekolah postgresql
        $siswa = $db_mysqli->get('tb_siswa')->result(); //  tb_siswa contoh nama tabel
        $siswa = $db_mysqli->get('tb_sekolah')->result(); //  tb_sekolah contoh nama tabel
        // lanjutkan logic selanjutnya
        
    }</pre>

Function diatas belum dapat langsung menampilkan data, perlu dilanjutkan dengan fungsi `mysqli_fetch_array` atau `mysqli_fetch_object` sesuai kebutuhan masing-masing.

<div class="wp-block-image">
  <figure class="aligncenter size-large is-resized"><img src="https://i0.wp.com/www.openprofessionalgroup.com/wp-content/uploads/2017/02/61629580-300x188.jpg?resize=381%2C239&#038;ssl=1" alt="" width="381" height="239" data-recalc-dims="1" /></figure>
</div>

Demikian tutorial Codeigniter singkat kali ini. Semoga dapat bermanfaat, terima kasih

_Melangkahlah &#8216;tuk hari esok!_