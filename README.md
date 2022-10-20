# GibbonEdu
# Sekilas Tentang
Gibbon merupakan sebuah platform open source untuk school management yang bersifat fleksibel. Aplikasi ini dirancang untuk mempermudah para guru, murid, orang tua, dan lembaga instansi sekolah.
# Instalasi
Prerequisites:
  1. Deploy Vultr Ubuntu 20.04 server terbaru
  2. Buat non-root user derngan sudo access.
  
a. Install Apache, MariaDB, dan PHP
$ sudo apt install apache2 mariadb-server php libapache2-mod-php php-common php-sqlite3 php-mysql php-gmp php-curl php-intl php-mbstring php-xmlrpc php-gd php-bcmath php-xml php-cli php-zip unzip git -y

b. Konfigurasikan MariaDB untuk Gibbon
Setelah menginstall LAMP stack pada server, harus dilakukan beberapa konfigurasi untuk dapat menjalankan Gibbon

  1. Login pada mysql
  $ sudo mysql
