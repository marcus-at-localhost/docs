# Installation

> Installation guide is based on **Ubuntu**. Of course, you can use any unix-based system, but make sure that your OS supports the following commands.<br/>

To create your new AtroCore application, first make sure you're using PHP 7.1 or above and have [Composer](https://getcomposer.org/download/) installed.

Before you start you need to configure your web server:

- [Nginx server configuration](https://github.com/atrocore/atrocore-docs/edit/master/en/administration/installation.md)
- [Apache server configuration](https://github.com/atrocore/atrocore-docs/blob/master/en/administration/apache-server-configuration.md)

After you have configured your web server you may start to install the Application.

I. Create your new project by running:
```
composer create-project atrocore/skeleton-pim my-atrocore-project
```
> **my-atrocore-project** – project name
   
II. Change recursively the user and group ownership for project files: 
```
chown -R www-data:www-data my-atrocore-project/
```
>**www-data** – depends on your webserver and can be one of the following: www, www-data, apache, etc.

III. Change the permissions for project files: 
```
find . -type d -exec chmod 755 {} + && find . -type f -exec chmod 644 {} +;
find data custom upload -type d -exec chmod 775 {} + && find data custom upload -type f -exec chmod 664 {} +
```     
IV. Configure the crontab as described below.

1. Open crontab for www-data user:
```
crontab -e -u www-data
``` 
2. Add the following configuration:
```      
* * * * * /usr/bin/php /var/www/my-atrocore-project/index.php cron 
```

V. Create MySQL database and user. User must have all privileges for database. You can create database and user with all privileges by executing next few commands:

> If MySQL Database is not installed, you need to install it.

Connect to mysql:
```
mysql -u root -p
```
Create database **atrocore**:
```
CREATE DATABASE atrocore;
```
Create user **atrocore_user** with password **atrocore_password** and grant all needed privileges:
```
CREATE USER atrocore_user@localhost;
ALTER USER atrocore_user@localhost IDENTIFIED BY 'atrocore_password';
GRANT ALL ON atrocore.* TO atrocore_user@localhost WITH GRANT OPTION;
```

VI. Go to http://YOUR_PROJECT/ to start the installation wizard for your AtroCore Application in the web interface. Follow the instructions in the wizard.