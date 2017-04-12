# Ahorratec
Personal install

34.210.14.12

sudo apt-get update

sudo apt-get install apache2 mysql-server mysql-client php libapache2-mod-php php-mysql php-curl php-pear php-dev php-mcrypt php-json git-core redis-server build-essential ufw ntp -y

sudo apt-get install php-pear
sudo pear channel-discover pear.swiftmailer.org
sudo pear install swift/swift

sudo sh -c 'echo "extension=dio.so" > /etc/php/7.0/apache2/conf.d/20-dio.ini'
sudo sh -c 'echo "extension=dio.so" > /etc/php/7.0/cli/conf.d/20-dio.ini'
sudo sh -c 'echo "extension=redis.so" > /etc/php/7.0/apache2/conf.d/20-redis.ini'
sudo sh -c 'echo "extension=redis.so" > /etc/php/7.0/cli/conf.d/20-redis.ini'

sudo a2enmod rewrite
sudo sh -c "echo '<Directory /var/www/html/emoncms>' >> /etc/apache2/sites-available/emoncms.conf"
sudo sh -c "echo '  Options FollowSymLinks' >> /etc/apache2/sites-available/emoncms.conf"
sudo sh -c "echo '  AllowOverride All' >> /etc/apache2/sites-available/emoncms.conf"
sudo sh -c "echo '  DirectoryIndex index.php' >> /etc/apache2/sites-available/emoncms.conf"
sudo sh -c "echo '  Order allow,deny' >> /etc/apache2/sites-available/emoncms.conf"
sudo sh -c "echo '  Allow from all' >> /etc/apache2/sites-available/emoncms.conf"
sudo sh -c "echo '</Directory>' >> /etc/apache2/sites-available/emoncms.conf"
sudo ln -s /etc/apache2/sites-available/emoncms.conf /etc/apache2/sites-enabled/
sudo a2ensite emoncms
sudo service apache2 reload
 
 cd /var/www/
 sudo chown $USER html
 cd html
 git clone -b stable https://github.com/emoncms/emoncms.git

 mysql -u root -p
 CREATE DATABASE ahorratec DEFAULT CHARACTER SET utf8;
 CREATE USER 'erick'@'localhost' IDENTIFIED BY 'Ahorratec4462';
 GRANT ALL ON ahorratec.* TO 'erick'@'localhost';
 flush privileges;
 exit
 
sudo mkdir /var/lib/phpfiwa
sudo mkdir /var/lib/phpfina
sudo mkdir /var/lib/phptimeseries
sudo chown www-data:root /var/lib/phpfiwa
sudo chown www-data:root /var/lib/phpfina
sudo chown www-data:root /var/lib/phptimeseries

cd /var/www/html/emoncms/
cp default.settings.php settings.php
nano settings.php

cd /var/www/html/emoncms/Modules
git clone https://github.com/emoncms/dashboard.git
git clone https://github.com/emoncms/app.git

sudo apt-get install gettext
sudo dpkg-reconfigure locales
//Editar archivo locale 
sudo locale-gen es_ES //sirve?

sudo reboot


sudo -i
passwd

cd /var/www/html/emoncms/scripts/logger/ && sudo chmod +x install.sh

touch /var/log/emoncms.log
chmod 666 /var/log/emoncms.log


//para errores 

tail -n 999 /var/log/syslog | less

 
