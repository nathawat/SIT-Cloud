sudo su
apt-get update
apt-get upgrade -y
apt-get dist-upgrade -y
apt-get autoremove -y
apt-get install apache2 php5 php5-cli php5-fpm php5-gd libssh2-php libapache2-mod-php5 php5-mcrypt php5-mysql git unzip zip postfix php5-curl mailutils php5-json -y
a2enmod rewrite headers
php5enmod mcrypt

nano /etc/apache2/sites-enabled/000-default.conf

<VirtualHost *:80>
        #ServerName sit-cloud.com
        #ServerAlias www.sit-cloud.com
        DocumentRoot /var/www/blog

        <Directory /var/www/blog>
                Options -Indexes
                AllowOverride All
                Order allow,deny
                Allow from all
        </Directory>
</VirtualHost>

cd /var/www/
wget https://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
mv wordpress blog
cd blog
chmod -R 744 .
chown -R www-data:www-data .

service apache2 restart
