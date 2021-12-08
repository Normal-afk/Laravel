# Laravel

###### Latar belakang

Project ini dibuat untuk menyelesaikan persyaratan pelatihan sertifikasi Junior Web Developer. Project sederhana ini telah menerapkan mvc pada laravel dan dapat melakukan CRUD kedalam database.

## HOW TO USE / INSTALL

##### REQUIRETMENT

- PHP VERSION >= 7.3.2
- Install git-client atau cli
- Install php xdebug (optional)
- install composer

##### INSTALL menggunakan composer

1.  _install phpxdebug_ (optional : agar pesan error debug menjadi rapih/ pretty )
2.  _buka terminal di htdocs pada xampp/laragon atau dir publicnya_

    <br>

    ```bash

    PS C:\xampp\htdocs>

    ```

3.  _install project_

    <br>
    ** PS C:\xampp\htdocs> composer create-project nagara/prosedural-php namaproject**
    <br>

    ```bash
    PS C:\xampp\htdocs> composer create-project nagara/prosedural-php applikasi-saya
    ```

## Structur / Arsitekture

<p>
oke berikut ini adalah gaya structur folder yang gue pakai
</p>

- _#apps_
  - _#config_
  - _#controller_
  - _#model_
  - _#view_
  - _#htaccess_
  - _#init.php_
- \*#database
  - _#error_vew.php_
  - _#function_error.php_
- _#public_
  - _#css_
  - _#js_
  - _#image_
- _#routes_
  - _#function_
  - _#getonvfile_
  - _#index_
  - _#routing_
- _#storage_
  - _#pdf_
  - _#doc_
  - _#img_
- _#.env_
- _#.env.example_
- _#.htaccess_
- _#index.php_

## Penjelasan Singkat

###### apps

folder apps adalah nanti dimana sebuah project small web dirancang, atau di atur mulai dari dcontroller, model dan view sebagai tampilannya.

<br>

###### config

folder config ini mengatur segala configurasi pada database mysqli, membuat constand dan menjalankan config untuk memanggil function connection database.

<br>

###### database

folder database ini adalah sebuah cheatsheet sintax mysqli

<br>

###### controller

folder controller ini adalah bentuk prosedural functional programing

###### routes

folder routes ini adalah untuk mengatur path atau arah routing pada apps

<br>

###### view

folder view ini adalah dimana hal yang berkaitan dengan html atau template yang akan di tampilkan pada halaman user

<br>

###### .htaccess

htaccess disini di set agar tidak bisa membuka folder corenya yaitu apps

<br>

###### autoload.php

autoload disini adalah untuk memanggil sebuah loading file pada folder config dengan urutan database yang pertama di require

<br>

###### init.php

untuk memanggil file config pada folder apps

<br>

###### public

folder public untuk meletakan asset seperti css, js dan image

<br>

###### storage

folder storage adalah tempat file hasil upload disimpan

<br>

###### .htaccess

default akses remove index.php for first open atau ketika pertama dibuka

<br>

###### index.php

untuk memanggil file autoload.php

## Basic Usage

## connection database

untuk config pada database diletakan pada file .env

```

DB_HOST=localhost
DB_PORT=3306
DB_NAME=namadatabasenya
DB_USER=userdatabasenya
DB_PASS=


```

## mengatur path url dan apps

untuk mengatur config path url dan apps juga terdapat pada file .env

```

# configurasi Path here
APP_NAME=prosedural-php-native
APP_FOLDER=/prosedural-php-native/
APP_HOST=http://localhost/
APP_URL=http://localhost/prosedural-php-native/

```

### routes

mendefiniskan arah route

```php
# example :
# $router->get('pattern', function() {
#    view("nama_view");
# });


$router->get('/', function() {
    view("welcome");
});

$router->get('login', function() {
    view("auth/login");
});


```

## controller

buat nama controllernya di folder apps > controller, lalu buat function function didalamnnya

```php
# example

function title()
{
   $title = 'home page';
   return $title;
}

/**
 * mencetak nilai string deskripsi
 * @return string
 */
function deskripsi()
{
  $deskripsi = "halaman home page";
}


```

## model

buat model untuk berinteraksi dengan query database,

```php
# example model

function get_all_data()
{
    # call connection ke database
    $conn = database();

    # query sintax pada database
    $sql = "SELECT * FROM users";

    # myqli execute
    $result = $conn->query($sql);

    #return data
    return $result->fetch_all(MYSQLI_ASSOC);
}

/**
 * docuemntations return singe data
 * @return object
 */

function get_single_data_by_condition($id)
{
    # call connection ke database
    $conn = database();

    # query sintax pada database
    $sql = "SELECT * FROM users WHERE id=$id ";

    # myqli execute
    $result = $conn->query($sql);

     #return data
    return $result->fetch_object();
}

```

## memanggil connection database

untuk memanggil connection pada database , cukup panggil function database() dan save ke dalam variabel, memanggil connection akan dibutuhkan ketika berinteraksi query dan model .

```php

# call connection ke database
$conn = database();

```

## memanggil model pada controller

untuk memanggil model pada controller bisa dilakukan dengan melakukan load file model dengan function model("nama_modelnya");

```php
# example controller user

function getDataUser()
{
  # load model di pada function
  model("userModel);

  # panggil function yang ada pada model
  $data = get_all_data();

  # mengembalikan nilai
  return $data;
}

```

## memanggil controller pada view

untuk memanggil pada controller dan menggunakan semua function yang sudah di deklarasi bisa melakukan call controller dengan function controller("namacontrollernya") di paling awal berkas view

```html

<?php
# example

#load controller
controller("loginController")


# next html code

?>

<!DOCTYPE html>
<html lang="en">

<meta http-equiv="content-type" content="text/html;charset=UTF-8" />
<head>

some code html here
...

</html>

```

## memanggil view lainnya

untuk memanggil view lainnya bisa gunakan function view("nama_viewnya),

```html
# example

<?php view("header") ?>

<p>some html code</p>
...

<?php view("footer")?>
```

## memanggil asset

untuk memanggil asset pada folder public gunakan function asset("namaassetnya"), asset bisa berupa berkas css, js, dan gambar biasanya di panggil pada berkas view.

```html
# example <link rel="stylesheet" type="text/css" href="<?= asset("vendor/bootstrap/css/bootstrap.min.css") ?>">
```

## memanggil arah url

untuk memanggil arah url bisa dilakukan dengan function url("nama-urlnya"), biasanya digunakan untuk navigasi antar halaman, example http://domain/home, atau http://domain/about dan lain lain. yang dimana arah urlnya didaftarkan pada routes terlebih dahulu.

```html
# example

<ul type="none" class="navbar-nav">
    <li class="nav-item"><a href="<?= url("login") ?>">Login page</a></li>
    <li class="nav-item"><a href="<?= url("register") ?>">Login page</a></li>
    <li class="nav-item"><a href="<?= url("about") ?>">Login page</a></li>
    <li class="nav-item"><a href="<?= url("home") ?>">Login page</a></li>
</ul>

```

## memanggil function timezone

untuk memanggil function timezone buka folder apps > config > timezone.php disana tersedia beberapa function yang sudah saya buat untuk waktu

mengatur zona waktu :

```php
date_default_timezone_set('Asia/Jakarta');
```

memanggil tahun :

```php

year_now() // return tahun 2021

```

## debug

untuk debug bisa menggunakan beberapa opsi berikut ini

- dd(valuenya);
- dump(valuenya);
- var_dump(valuenya);
- var_dump(valuenya);die;

## routing url parameter

jika menerima slug atau parameter pada url satu parameter

```php

$router->get('data/{id}', function($id) {
    view("backend/penduduk", $id);
});

```

lalu pada berkas viewnya :

```html
# example

<?php
# load controllernya
controller("pendudukController");

$parameter = $data;
dump($parameter[1]); // return id

?>

<!DOCTYPE html>
<html lang="en">
  ...
</html>
```

jika menerima slug atau parameter pada url lebih dari satu parameter

```php
$router->get('data/{id}/{username}', function($id, $username) {
    view("backend/penduduk", [$id, $username]);
});

```

lalu pada berkas viewnya

```html
# example

<?php
# load controllernya
controller("pendudukController");

$parameter = $data;
dump($parameter[0]); // return id
dump($parameter[1]); // return username

?>

<!DOCTYPE html>
<html lang="en">
  ...
</html>
```

## passing slug ke controller

untuk memasingnya ke controller buat function pada berkas controllenya dan berikan paramter, contoh :

berkas pada routenya web.php

```php
$router->get('data/{id}/{username}', function($id, $username) {
    view("backend/penduduk", [$id, $username]);
});
```

berkasi view penduduk.php

```html
# example

<?php
# load controllernya
controller("pendudukController");

$parameter = $data;
dump($parameter[0]); // return debug id
dump($parameter[1]); // return debug username

#call function yang ada di dalam controllernya
getuserid($parameter[0]); // return id

?>

<!DOCTYPE html>
<html lang="en">
  ...
</html>
```

berkas controller penduduk.php

```html
<?php

function getuserid($id)
{
  echo $id; // return id
}

?>
```

## passing paramter ke model

untuk memasingnya ke dalam file model dari controller sama saja caranya load modelnya lalu pass melalui functionnya yang ada di controller ke function model

berkas pada routenya web.php

```php
$router->get('data/{id}/{username}', function($id, $username) {
    view("backend/penduduk", [$id, $username]);
});
```

berkasi view penduduk.php

```html
# example

<?php
# load controllernya
controller("pendudukController");

$parameter = $data;
dump($parameter[0]); // return debug id
dump($parameter[1]); // return debug username

#call function yang ada di dalam controllernya
getuserid($parameter[0]); // return id

?>

<!DOCTYPE html>
<html lang="en">
  ...
</html>
```

berkas controller penduduk.php

```php
<?php

function getuserid($id)
{
  model("pendudukModel");

  return get_user_data_by($id)
}

?>

```

berkas controller model penduduk.php

```php
/**
 * docuemntations return singe data
 * @return object
 */

function get_user_data_by($id)
{
    $conn = database();

    // sintac query
    $sql = "SELECT * FROM users WHERE id=$id ";
    $result = $conn->query($sql);
    return $result->fetch_object(); // return object
}


```

## membuat templating atau memecah template

untuk memecah bagian HTML menjadi beberapa bagian seperti header, footer dan content, itu disebut templating, untuk membuat templating bisa memanggil function view

example :

view

- auth
  - layout
    - header.php
    - footer.php
  - pages
    - login.php

##### controller di load di awal view sebelum meletakan berkas view

```php
<?php
# load controllernya
controller("loginController");
?>

<!-- # load template header -->
<?= view("auth/layout/header")?>

# content here ...

```

berkas login.php

```html
<!-- # load template header -->
<?= view("auth/layout/header")?>

<div class="limiter">
  <div class="container-login100"># content here ...</div>
</div>
<!-- # load template footer -->
<?= view("auth/layout/footer")?>
```

berkas header.php

```html
<!DOCTYPE html>
<html lang="en">
  <meta http-equiv="content-type" content="text/html;charset=UTF-8" />
  <head>
    <title><?= title() ?></title>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <!--===============================================================================================-->
    <link rel="icon" type="image/png" href="images/icons/favicon.ico" />
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("vendor/bootstrap/css/bootstrap.min.css") ?>
    ">
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("fonts/font-awesome-4.7.0/css/font-awesome.min.css") ?>
    ">
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("fonts/Linearicons-Free-v1.0.0/icon-font.min.css") ?>
    ">
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("vendor/animate/animate.css") ?>
    ">
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("vendor/css-hamburgers/hamburgers.min.css") ?>
    ">
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("vendor/animsition/css/animsition.min.css") ?>
    ">
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("vendor/select2/select2.min.css") ?>
    ">
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("vendor/daterangepicker/daterangepicker.css") ?>
    ">
    <!--===============================================================================================-->
    <link rel="stylesheet" type="text/css" href="
    <?= asset("css/util.css") ?>
    "> <link rel="stylesheet" type="text/css" href="
    <?= asset("css/main.css") ?>
    ">
    <!--===============================================================================================-->
  </head>
  <body></body>
</html>
```

berkas footer.php

```html


<!--===============================================================================================-->
<script src="<?= asset("vendor/jquery/jquery-3.2.1.min.js") ?>"></script>
<!--===============================================================================================-->
	<script src="<?= asset("vendor/animsition/js/animsition.min.js") ?>"></script>
<!--===============================================================================================-->
	<script src="<?= asset("vendor/bootstrap/js/popper.js") ?>"></script>
	<script src="<?= asset("vendor/bootstrap/js/bootstrap.min.js") ?>"></script>
<!--===============================================================================================-->
	<script src="<?= asset("vendor/select2/select2.min.js") ?>"></script>
<!--===============================================================================================-->
	<script src="<?= asset("vendor/daterangepicker/moment.min.js") ?>"></script>
	<script src="<?= asset("vendor/daterangepicker/daterangepicker.js") ?>"></script>
<!--===============================================================================================-->
	<script src="<?= asset("vendor/countdowntime/countdowntime.js") ?>"></script>
<!--===============================================================================================-->
	<script src="<?= asset("js/main.js") ?>"></script>
</body>

</html>


```
