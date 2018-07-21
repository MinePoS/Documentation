Warning
Please note MinePoS is currently in **ALPHA** we do **NOT** recommend installing it on a production server.

.. _Introduction:
Introduction
===============
MinePoS is a free alternative game donation store.

.. _Requirements:
Requirements
===============
* Dedicated Server / VPS
* SSH Access
* Sub-domain
* MySQL Server & Database 



.. _Installation-Nginx:
Installation-Nginx
===================
#. Login to your server via SSH
#. Run the following command :: curl -s https://gist.githubusercontent.com/AndrewAubury/8b8a44214d54150a4360366ddd0d8be5/raw/de3caaf86bfb5bbb6dcc513e9cd24d3f00147acc/install-minepos.sh | bash
#. Follow the installer.
#. Log in to MinePoS and change your password

.. _Installation-Apache2
Installation-Apache2
===================

Preparing your OS
==================
   1. `apt -y install software-properties-common`
   2. `add-apt-repository -y ppa:ondrej/php`
   3. `apt update`
   4. :code:`apt -y install php7.2 php7.2-cli php7.2-gd php7.2-mysql php7.2-pdo php7.2-mbstring php7.2-tokenizer php7.2-bcmath php7.2-xml php7.2-fpm php7.2-curl php7.2-zip curl tar unzip git`

Preparing Apache2
==================
   1. :code:`mkdir -p /var/www/minepos/`
   2. nano /etc/apache2/sites-enabled/minepos.conf

.. code-block:: text

    <VirtualHost *:80>
        DocumentRoot "/var/www/minepos/public"
        ServerName <domain>           
        <Directory "/var/www/minepos/public">
           AllowOverride All
        </Directory>
    </VirtualHost>


3. Run systemctl restart apache2

Optional Setup with SSL certificate 
====================================
Setup HTTPS: Follow the instructions with let https://certbot.eff.org/lets-encrypt/ubuntuxenial-apache

Installing Minepos
==================
   1.Run the following commands

.. code-block:: text

    cd /var/www/minepos/
    wget https://github.com/MinePoS/Backend/archive/v0.0.6.zip
    unzip v0.0.6.zip
    rm v0.0.6.zip
    mv Backend-0.0.6/* .
    rm -Rf Backend-0.0.6
    cp example.env .env
    chmod -R 755 storage/* bootstrap/cache public/*
    curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
    composer install
    php artisan key:generate --force

2. Edit .env Filling the fields
3. php artisan migrate --seed
