# GibbonEdu

![](https://camo.githubusercontent.com/b9d2769edd3e7a5cdd59d0f429f2f1c796a163d38b812498d00b9691fed7d593/68747470733a2f2f676962626f6e6564752e6f72672f696d672f676962626f6e2d6c6f676f2e706e67)

> Gibbon merupakan sebuah *platform open source* untuk *school management* yang bersifat fleksibel. Aplikasi ini dirancang untuk mempermudah para guru, murid, orang tua, dan lembaga instansi sekolah.

---

### Daftar Isi
- [Anggota Kelompok](#anggota-kelompok)
- [Instalasi](#instalasi)
- [Dokumentasi Website](#dokumentasi-website)
- [Referensi](#referensi)

---

## Anggota Kelompok

| Nama                  | NIM           | Username Github                      |
| :-------------------- | :------------ | :----------------------------------- |
| Afiqah Nur Amalia     | G6401201021   | https://github.com/afiqahnuramalia   |
| Aiko Nur Fajrin D     | G6401201062   | https://github.com/aiwillsurvaiv     |
| Shabrina Basyasyah    | G6401201076   | https://github.com/ShabrinaBasyasyah |

---

## Instalasi
Kebutuhan Sistem
  1. Ubuntu 20.04
  2. Buat non-root user dengan sudo access.
  
#### a. Install Apache, MariaDB, dan PHP

```
$ sudo apt install apache2 mariadb-server php libapache2-mod-php php-common php-sqlite3 php-mysql php-gmp php-curl php-intl php-mbstring php-xmlrpc php-gd php-bcmath php-xml php-cli php-zip unzip git -y
```

#### b. Konfigurasikan MariaDB untuk Gibbon
Setelah menginstall LAMP stack pada server, harus dilakukan beberapa konfigurasi untuk dapat menjalankan Gibbon

###### 1. Login pada mysql

```
$ sudo mysql
```

###### 2. Setelah login, buat database "gibbondb"

```
CREATE DATABASE gibbondb;
```

###### 3. Buatlah user baru dan masukkan password

```
CREATE USER 'gibbon'@'localhost' IDENTIFIED BY 'StrongPassword';
```

###### 4. Grant semua fitur pada gibbondb pada user gibbon

```
GRANT ALL ON gibbondb.* TO 'gibbon'@'localhost' WITH GRANT OPTION;
```

###### 5. Flush privilages 

```
FLUS PRIVILAGES;
```

###### 6. Keluar dari MySQL shell

```
EXIT;
```

#### c. Instalasi Gibbon

```
$ sudo wget https://github.com/GibbonEdu/core/archive/refs/tags/v24.0.00.zip
$ sudo unzip v24.0.00.zip
$ sudo cp -r core-24.0.00/* /var/www/html/gibbon
$ sudo chown -R www-data:www-data /var/www/html/gibbon/
$ sudo chmod -R 755 /var/www/html/gibbon/
$ cd /var/www/html/gibbon/
$ sudo apt install composer -y
$ sudo composer install
```

#### d. Konfigurasi Apache
###### 1. Edit default Apache virtual host configuration file 000-default.conf

```
$ sudo nano /etc/apache2/sites-available/000-default.conf
```

```
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/gibbon

     <Directory /var/www/html/gibbon/>
          Options FollowSymlinks
          AllowOverride All
          Require all granted
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/error.log
     CustomLog ${APACHE_LOG_DIR}/access.log combined

     <Directory /var/www/html/gibbon/>
            RewriteEngine on
            RewriteBase /
            RewriteCond %{REQUEST_FILENAME} !-f
            RewriteRule ^(.*) index.php [PT,L]
    </Directory>
</VirtualHost>
```

```
$ sudo a2enmod rewrite
$ sudo systemctl restart apache2
```

#### e. Acces Gibbon Web Interface

http://34.87.56.48/

---

## Dokumentasi Website

![](https://github.com/aiwillsurvaiv/First-Project/blob/main/dokum-komdat-1.png)
![](https://github.com/aiwillsurvaiv/First-Project/blob/main/dokum-komdat-2.png)

---

## Referensi

1. [About Gibbon](https://gibbonedu.org/about/)
2. [How to Install Gibbon LMS on Ubuntu 20.04](https://www.vultr.com/docs/install-gibbon-lms-on-ubuntu-20-04/)
3. [Product Review of Gibbon](https://www.thetechedvocate.org/product-review-of-gibbon/)

---

