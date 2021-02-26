# Apache server configuration
> All settings listed here are made on an Ubuntu server.

## 1. Install Apache Web Server
```
sudo apt install apache2
```

## 2. Install PHP and libraries
To install all necessary libraries, run these commands in the terminal:
```
sudo apt-get update
sudo apt-get install php-mysql php-json php-gd php-zip php-imap php-mbstring php-curl ghostscript php-mailparse php-imagick
sudo phpenmod imap mbstring
sudo service apache2 restart
```
The steps bellow are needed to make your virtual host work.
> These steps will solve your problem, if you get an empty page with 404 code response.

## 3. Enable mod_rewrite support for Apache
To enable mod_rewrite, run these commands in a terminal:
```
sudo a2enmod rewrite
sudo service apache2 restart
```

## 4. Create configuration for your virtual host

```
cd /etc/apache2/sites-available/
sudo cp 000-default.conf atrocore.conf
```

## 5. Edit your configuration file and add the domain name, you want to use:

> you may use "sudo vi atrocore.conf" for it.

```
DocumentRoot /var/www/your-atrocore-project-path
ServerName your-atrocore-url.com
```

## 6. Modify the Directory directive to enable .htaccess support

```
<Directory /var/www/your-atrocore-project-path>
AllowOverride All
</Directory>
```

> Here an **example** of the server configuration settings:
```
<VirtualHost *:80>
ServerName atrocore.local
ServerAlias www.atrocore.local
DocumentRoot /var/www/atrocore.local
<Directory var/www/atrocore.local/>
AllowOverride All
</Directory>
</VirtualHost>
```

> To enable .htaccess support on other linux systems you may need to edit the server configuration settings in `/etc/apache2/apache2.conf` or `/etc/httpd/conf/httpd.conf`.

Afterward, restart apache:
```
sudo service apache2 restart
```
