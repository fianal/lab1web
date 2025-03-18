# lab11_php_ci4

## Praktikum 1 : PHP Framework (Codeigniter)

<h1>Persiapan</h1>

<p>Sebelum memulai menggunakan Framework Codeigniter, perlu dilakukan konfigurasi pada
webserver. Beberapa ekstensi PHP perlu diaktifkan untuk kebutuhan pengembangan
Codeigniter 4.</p>

Berikut beberapa ekstensi yang perlu diaktifkan:

• php-json ekstension untuk bekerja dengan JSON;

• php-mysqlnd native driver untuk MySQL;

• php-xml ekstension untuk bekerja dengan XML;

• php-intl ekstensi untuk membuat aplikasi multibahasa;

• libcurl (opsional), jika ingin pakai Curl.

Untuk mengaktifkan ekstentsi tersebut, melalu XAMPP Control Panel, pada bagian Apache
klik Config -> PHP.ini

<h1>Instalasi Codeigniter 4</h1>

<p>Untuk melakukan instalasi Codeigniter 4 dapat dilakukan dengan dua cara, yaitu cara manual
dan menggunakan composer. Pada praktikum ini kita menggunakan cara manual.</p>

• Unduh Codeigniter dari website https://codeigniter.com/download
• Extrak file zip Codeigniter ke direktori htdocs/lab11_ci.
• Ubah nama direktory framework-4.x.xx menjadi ci4.
• Buka browser dengan alamat http://localhost/lab11_ci/ci4/public/

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/ci4.png)

<h1>Menjalankan CLI (Command Line Interface)</h1>

<p>Codeigniter 4 menyediakan CLI untuk mempermudah proses development. Untuk mengakses
CLI buka terminal/command prompt.</p>

Arahkan lokasi direktori sesuai dengan direktori kerja project dibuat (xampp/htdocs/lab11_ci/ci4/)

Perintah yang dapat dijalankan untuk memanggil CLI Codeigniter adalah:

```
php spark
```

Lalu nyalakan secara bersamaan dengan cara ketik:

```
php spark serve
```

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/phpspark.png)

<h1>Mengaktifkan Mode Debugging</h1>

<p>Codeigniter 4 menyediakan fitur debugging untuk memudahkan developer untuk mengetahui
pesan error apabila terjadi kesalahan dalam membuat kode program.</p>

<p>Semua jenis error akan ditampilkan sama. Untuk memudahkan mengetahui jenis errornya,
maka perlu diaktifkan mode debugging dengan mengubah nilai konfigurasi pada environment
variable CI_ENVIRONMENT menjadi development.</p>

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/env.png)

<p>Ubah nama file env menjadi .env kemudian buka file tersebut dan ubah nilai variable
CI_ENVIRINMENT menjadi development.</p>

<h2>Contoh Mode Debugging Pada CI4</h2>

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/ci4debugging.png)

<p>Contoh error yang terjadi. Untuk mencoba error tersebut, ubah kode pada file
app/Controller/Home.php hilangkan titik koma pada akhir kode.</p>

```
<?php

namespace App\Controllers;

class Home extends BaseController
{
    public function index(): string
    {
        return view('welcome_message')
    }
}
```

<h1>Struktur Direktori</h1>

<p>Untuk lebih memahami Framework Codeigniter 4 perlu mengetahui struktur direktori dan file
yang ada. Buka pada Windows Explorer atau dari Visual Studio Code -> Open Folder.</p>

Terdapat beberapa direktori dan file yang perlu dipahami fungsi dan kegunaannya.

• .github folder ini kita butuhkan untuk konfigurasi repo github, seperti konfigurasi untuk
build dengan github action;

• app folder ini akan berisi kode dari aplikasi yang kita kembangkan;

• public folder ini berisi file yang bisa diakses oleh publik, seperti file index.php, robots.txt,
favicon.ico, ads.txt, dll;

• tests folder ini berisi kode untuk melakukan testing dengna PHPunit;

• vendor folder ini berisi library yang dibutuhkan oleh aplikasi, isinya juga termasuk kode
core dari system CI.

• writable folder ini berisi file yang ditulis oleh aplikasi. Nantinya, kita bisa pakai untuk
menyimpan file yang di-upload, logs, session, dll.

Sedangkan file-file yang berada pada root direktori CI sebagai berikut.

• .env adalah file yang berisi variabel environment yang dibutuhkan oleh aplikasi.

• .gitignore adalah file yang berisi daftar nama file dan folder yang akan diabaikan oleh Git.

• build adalah script untuk mengubah versi codeigniter yang digunakan. Ada versi release
(stabil) dan development (labil).

• composer.json adalah file JSON yang berisi informasi tentang proyek dan daftar library
yang dibutuhkannya. File ini digunakan oleh Composer sebagai acuan.

• composer.lock adalah file yang berisi informasi versi dari libraray yang digunakan aplikasi.

• license.txt adalah file yang berisi penjelasan tentang lisensi Codeigniter;

• phpunit.xml.dist adalah file XML yang berisi konfigurasi untuk PHPunit.

• README.md adalah file keterangan tentang codebase CI. Ini biasanya akan dibutuhkan
pada repo github atau gitlab.

• spark adalah program atau script yang berfungsi untuk menjalankan server, generate kode,
dll.

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/filepath.png)

<p>Fokus kita pada folder app, dimana folder tersebut adalah area kerja kita untuk membuat
aplikasi. Dan folder public untuk menyimpan aset web seperti css, gambar, javascript, dll.</p>

<h1>Routing dan Controller</h1>

<p>Routing merupakan proses yang mengatur arah atau rute dari request untuk menentukan
fungsi/bagian mana yang akan memproses request tersebut. Pada framework CI4, routing
bertujuan untuk menentukan Controller mana yang harus merespon sebuah request. Controller
adalah class atau script yang bertanggung jawab merespon sebuah request.</p>

Router terletak pada file app/config/Routes.php,Pada file tersebut kita dapat mendefinisikan route untuk aplikasi yang kita buat.

Contoh
```
$routes->get('/', 'Home::index');
```

Kode tersebut akan mengarahkan rute untuk halaman home.

<h2>Membuat Route Baru</h2>
Tambahkan kode berikut ke dalam Routes.php

```
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```

Untuk mengetahui route yang ditambahkan sudah benar, buka CLI dan jalankan perintah
berikut.

```
php spark routes
```

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/phproutes.png)

<p>Selanjutnya coba akses route yang telah dibuat dengan mengakses alamat url
http://localhost:8080/about</p>

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/filenotfoundabt.png)

<p>Ketika diakses akan mucul tampilan error 404 file not found, itu artinya file/page tersebut tidak
ada. Untuk dapat mengakses halaman tersebut, harus dibuat terlebih dahulu Contoller yang
sesuai dengan routing yang dibuat yaitu Contoller Page.</p>

<h2>Membuat Controller</h2>
Selanjutnya adalah membuat Controller Page. Buat file baru dengan nama page.php pada
direktori Controller kemudian isi kodenya seperti berikut.

```
<?php
namespace App\Controllers;
class Page extends BaseController
{
public function about()
{
echo "Ini halaman About";
}
public function contact()
{
echo "Ini halaman Contact";
}
public function faqs()
{
echo "Ini halaman FAQ";
}
}
```

Selanjutnya refresh Kembali browser, maka akan ditampilkan hasilnya yaotu halaman sudah
dapat diakses.

<h2>Auto Routing</h2>
Secara default fitur autoroute pada Codeiginiter sudah aktif. Untuk mengubah status autoroute
dapat mengubah nilai variabelnya. Untuk menonaktifkan ubah nilai true menjadi false.

```
$routes->setAutoRoute(true);
```

Tambahkan method baru pada Controller Page seperti berikut.

```
public function tos()
{
echo "ini halaman Term of Services";
}
```

Method ini belum ada pada routing, sehingga cara mengaksesnya dengan menggunakan
alamat: http://localhost:8080/page/tos

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/halamantos.png)

<h1>Membuat View</h1>
<p>Selanjutnya adalam membuat view untuk tampilan web agar lebih menarik. Buat file baru
dengan nama about.php pada direktori view (app/view/about.php) kemudian isi kodenya
seperti berikut.</p>

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title><?= $title; ?></title>
</head>
<body>
  <h1><?= $title; ?></h1>
  <hr>
  <p><?= $content; ?></p>
</body>
</html>
```

Ubah method about pada class Controller Page menjadi seperti berikut:

```
public function about()
{
  return view('about', [
    'title' => 'Halaman Abot',
    'content' => 'Ini adalah halaman abaut yang menjelaskan tentang isi
halaman ini.'
  ]);
}
```

Kemudian lakukan refres pada halaman tersebut.

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/nostylecss.png)

<h1>Membuat Layout Web dengan CSS</h1>

<p>Pada dasarnya layout web dengan css dapat diimplamentasikan dengan mudah pada
codeigniter. Yang perlu diketahui adalah, pada Codeigniter 4 file yang menyimpan asset css
dan javascript terletak pada direktori public.</p>

Buat file css pada direktori public dengan nama style.css (copy file dari praktikum
lab4_layout. Kita akan gunakan layout yang pernah dibuat pada praktikum 4.

```
/* Reset dasar */
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f8f9fa;
}

/* Container utama */
#container {
    width: 100%; /* Lebar penuh */
    max-width: 1200px; /* Maksimal 1200px agar tidak terlalu lebar */
    margin: 0 auto;
    background: white;
    padding: 20px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

/* Header */
header {
    font-size: 24px;
    font-weight: bold;
    color: #777;
    padding: 20px 0;
    text-align: left;
}

/* Navigasi */
nav {
    background-color: #1f5faa;
    padding: 10px;
    display: flex;
    justify-content: left; /* Tengah pada layar besar */
    flex-wrap: wrap; /* Supaya tetap rapi di layar kecil */
}

nav a {
    padding: 15px 30px;
    display: inline-block;
    color: #ffffff;
    font-size: 14px;
    text-decoration: none;
    font-weight: bold;
}

nav a.active,
nav a:hover {
    background-color: #2b83ea;
    border-radius: 5px;
}

/* Hero Panel */
#hero {
    background-color: #e4e4e5;
    padding: 50px 20px;
    text-align: center;
    margin-bottom: 20px;
}

#hero h1 {
    margin-bottom: 20px;
    font-size: 35px;
}

#hero p {
    margin-bottom: 20px;
    font-size: 18px;
    line-height: 25px;
}

#hero a.btn {
    padding: 10px 20px;
    background-color: #428bca;
    color: white;
    text-decoration: none;
    font-weight: bold;
    display: inline-block;
    border-radius: 5px;
}

#hero a.btn:hover {
    background-color: #2b83ea;
}

/* Main Wrapper */
#wrapper {
    display: flex;
    flex-wrap: wrap;
    margin-top: 20px;
}

/* Main Content */
#main {
    flex: 3;
    padding: 20px;
    min-width: 300px;
}

/* Sidebar */
#sidebar {
    flex: 1;
    background: #f1f1f1;
    padding: 20px;
    margin-left: 20px;
    min-width: 250px;
}

/* Widget */
.widget-box {
    border: 1px solid #eee;
    margin-bottom: 20px;
    background: white;
}

.widget-box .title {
    padding: 10px 16px;
    background-color: #428bca;
    color: white;
    font-weight: bold;
}

.widget-box ul {
    list-style-type: none;
    padding: 0;
}

.widget-box li {
    border-bottom: 1px solid #eee;
}

.widget-box li a {
    padding: 10px 16px;
    color: #333;
    display: block;
    text-decoration: none;
}

.widget-box li:hover a {
    background-color: #eee;
}

.widget-box p {
    padding: 15px;
    line-height: 25px;
}

/* Footer */
footer {
    background: black;
    color: white;
    text-align: lift;
    padding: 10px;
    margin-top: 20px;
}

/* Responsiveness */
@media screen and (max-width: 768px) {
    #wrapper {
        flex-direction: column;
    }
    
    #sidebar {
        margin-left: 0;
        margin-top: 20px;
    }

    nav {
        justify-content: center;
        flex-direction: column;
        text-align: center;
    }

    nav a {
        display: block;
        padding: 10px;
    }
}
```

Kemudian buat folder template pada direktori view kemudian buat file header.php dan
footer.php

<h2>File app/view/template/header.php</h2>

```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title><?= $title; ?></title>
<link rel="stylesheet" href="<?= base_url('/style.css');?>">
</head>
<body>
<div id="container">
<header>
<h1>Layout Sederhana</h1>
</header>
<nav>
<a href="<?= base_url('/');?>" class="active">Home</a>
<a href="<?= base_url('/artikel');?>">Artikel</a>
<a href="<?= base_url('/about');?>">About</a>
<a href="<?= base_url('/contact');?>">Kontak</a>
</nav>
<section id="wrapper">
<section id="main">
```

<h2>File app/view/template/footer.php</h2>

```
</section>
<aside id="sidebar">
<div class="widget-box">
<h3 class="title">Widget Header</h3>
<ul>
<li><a href="#">Widget Link</a></li>
<li><a href="#">Widget Link</a></li>
</ul>
</div>
<div class="widget-box">
<h3 class="title">Widget Text</h3>
<p>Vestibulum lorem elit, iaculis in nisl volutpat,
malesuada tincidunt arcu. Proin in leo fringilla, vestibulum mi porta,
faucibus felis. Integer pharetra est nunc, nec pretium nunc pretium ac.</p>
</div>
</aside>
</section>
<footer>
<p>&copy; 2021 - Universitas Pelita Bangsa</p>
</footer>
</div>
</body>
</html>
```

<h2>Kemudian ubah file app/view/about.php seperti berikut.</h2>

```
<?= $this->include('template/header'); ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->include('template/footer'); ?>
```

![img](https://github.com/fianal/lab1web/blob/main/img_lat1web/withstylecss.png)




