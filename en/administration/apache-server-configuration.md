# Apache server configuration
Note that all configuration settings listed here are made on Ubuntu server.

### PHP requirements
To install all necessary libraries, run these commands in the terminal:
```
sudo apt-get update
sudo apt-get install php-mysql php-json php-gd php-zip php-imap php-mbstring php-curl ghostscript php-mailparse php-imagick
sudo phpenmod imap mbstring
sudo service apache2 restart
```

### Fixing the empty page (with 404 code response) when you are trying to install AtroCore via browser install wizard
When you are trying to install AtroCore via browser install wizard, you may get an empty page with 404 code response.
To fix it, try the following steps one by one. After each step check if the issue is solved. If it works, then further steps are not needed.

##### 1. Enable mod_rewrite support for Apache
To enable mod_rewrite, run these commands in a terminal:
```
sudo a2enmod rewrite
sudo service apache2 restart
```

##### 2. Enable .htaccess support
To enable .htaccess support, add/edit the server configuration settings `/etc/apache2/sites-available/ATRO_VIRTUAL_HOST.conf` or `/etc/apache2/apache2.conf` (or `/etc/httpd/conf/httpd.conf`):
```
<Directory /PATH_TO_ATRO/>
AllowOverride All
</Directory>
```
Here an **example** of the server configuration settings:
```
<VirtualHost *:80>
ServerName atropim.local
ServerAlias www.atropim.local
DocumentRoot /var/www/atropim.local
<Directory var/www/atropim.local/>
AllowOverride All
</Directory>
</VirtualHost>
```

Afterward, restart apache:
```
sudo service apache2 restart
```
