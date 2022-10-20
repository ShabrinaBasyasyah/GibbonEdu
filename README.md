# GibbonEdu

![](https://github.com/aiwillsurvaiv/First-Project/blob/main/gibbon-logo-flat.png)

> Gibbon merupakan sebuah platform open source untuk school management yang bersifat fleksibel. Aplikasi ini dirancang untuk mempermudah para guru, murid, orang tua, dan lembaga instansi sekolah.

---

### Daftar Isi
- [Anggota Kelompok](#anggota-kelompok)
- [Instalasi](#instalasi)

---

## Anggota Kelompok

| Nama                  | NIM           | Username Github                      |
| :-------------------- | :------------ | :----------------------------------- |
| Afiqah Nur Amalia     | G6401201021   | https://github.com/                  |
| Aiko Nur Fajrin D     | G6401201062   | https://github.com/aiwillsurvaiv     |
| Shabrina Basyasyah    | G6401201076   | https://github.com/ShabrinaBasyasyah |

---

## Instalasi
Prerequisites:
  1. Deploy Vultr Ubuntu 20.04 server terbaru
  2. Buat non-root user dengan sudo access.
  
#### a. Install Apache, MariaDB, dan PHP

$ sudo apt install apache2 mariadb-server php libapache2-mod-php php-common php-sqlite3 php-mysql php-gmp php-curl php-intl php-mbstring php-xmlrpc php-gd php-bcmath php-xml php-cli php-zip unzip git -y

#### b. Konfigurasikan MariaDB untuk Gibbon
Setelah menginstall LAMP stack pada server, harus dilakukan beberapa konfigurasi untuk dapat menjalankan Gibbon

###### 1. Login pada mysql

$ sudo mysql

###### 2. Setelah login, buat database "gibbondb"

CREATE DATABASE gibbondb;
  
###### 3. Buatlah user baru dengan password StrongPassword

CREATE USER 'gibbon'@'localhost' IDENTIFIED BY 'StrongPassword';
 
###### 4. Grant semua fitur pada gibbondb pada user gibbon

GRANT ALL ON gibbondb.* TO 'gibbon'@'localhost' WITH GRANT OPTION;

###### 5. Flush privilages 

FLUS PRIVILAGES;

###### 6. Keluar dari MySQL shell

EXIT;

#### c. Instalasi Gibbon

$ sudo wget https://github.com/GibbonEdu/core/archive/refs/tags/v24.0.00.zip

$ sudo unzip v24.0.00.zip

$ sudo cp -r core-24.0.00/* /var/www/html/gibbon

$ sudo chown -R www-data:www-data /var/www/html/gibbon/

$ sudo chmod -R 755 /var/www/html/gibbon/

$ cd /var/www/html/gibbon/

$ sudo apt install composer -y

$ sudo composer install

#### d. Konfigurasi Apache
###### 1. Edit default Apache virtual host configuration file 000-default.conf

$ sudo nano /etc/apache2/sites-available/000-default.conf

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

$ sudo a2enmod rewrite

$ sudo systemctl restart apache2

#### e. Acces Gibbon Web Interface

http://192.0.2.10

---
