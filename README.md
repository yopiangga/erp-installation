
# Install BlueSeer ERP on Linux Desktop

A brief description of what this project does and who it's for




## Download ZIP file

```bash
  wget https://github.com/blueseerERP/blueseer/releases/download/v6.2/blueseer.generic.linux.v62.zip
```

## Extract zip

```bash
  unzip blueseer -d /home/{user}/blueseer
```

## Execute

```bash
  cd /home/{user}/blueseer
  ./login.sh
```

# Install Dolibarr ERP on Ubuntu

A brief description of what this project does and who it's for


## Install support package

```bash
apt-get install software-properties-common -y
add-apt-repository ppa:ondrej/php -y
apt-get install apache2 mariadb-server php7.4 libapache2-mod-php7.4 php7.4-common php7.4-curl php7.4-intl php7.4-mbstring php7.4-mcrypt php7.4-json php7.4-xmlrpc php7.4-soap php7.4-mysql php7.4-gd php7.4-xml php7.4-cli php7.4-zip wget unzip git -y
nano /etc/php/7.4/apache2/php.ini
```

## Restart application

```bash
systemctl start apache2
systemctl enable apache2
systemctl start mariadb
systemctl enable mariadb
```

## Secure mode

```bash
mysql_secure_installation
```

## Configuration database & user

```bash
mysql -u root -p
CREATE DATABASE dolibarrdb;
CREATE USER dolibarr;
GRANT ALL PRIVILEGES ON dolibarrdb.* TO 'dolibarr'@'localhost' IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
EXIT
```

## Setup modul application

```bash
git clone https://github.com/dolibarr/dolibarr
cp -r dolibarr /var/www/html/dolibarr
chown -R www-data:www-data /var/www/html/dolibarr/
chmod -R 775 /var/www/html/dolibarr/
cp /var/www/htmldolibar/htdocs/conf/conf.php.example /var/www/htmldolibar/htdocs/conf/conf.php
chmod 777 /var/www/htmldolibar/htdocs/conf/conf.php
mkdir /var/www/htmldolibar/documents 
chmod -R 777 /var/www/htmldolibar/documents
```

## Apache2 Configuration Virtual Host

```bash
nano /etc/apache2/sites-available/dolibarr.conf
```
```bash
<VirtualHost *:80>
     ServerAdmin admin@example.com
     DocumentRoot /var/www/html/dolibarr/htdocs

     <Directory /var/www/html/dolibarr/htdocs/>
          Options +FollowSymlinks
          AllowOverride All
          Require all granted
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/dolibarr_error.log
     CustomLog ${APACHE_LOG_DIR}/dolibarr_access.log combined

</VirtualHost>
```

## Enabling configuration file

```bash
a2ensite dolibarr
a2enmod rewrite
```

## Restart System

```bash
systemctl restart apache2
systemctl status apache2
```

