# Installation Guide

> Installation guide is based on **Ubuntu**. Of course, you can use any unix-based system, but make sure that your OS supports the following commands.<br/>

To create your new AtroCore application, first make sure you're using PHP 7.1 or above.

Before you start you need to configure your web server:

- [Apache server configuration](https://github.com/atrocore/atrocore-docs/blob/master/en/administration/apache-server-configuration.md)
- [Nginx server configuration](https://github.com/atrocore/atrocore-docs/blob/master/en/administration/nginx-server-configuration.md)

After you have configured your web server you may start to install the Application.

## 1. Create your project directory
```
cd /var/www && mkdir my-atrocore-project && cd my-atrocore-project 
```
> **my-atrocore-project** – project name

## 2. Download project files

> git is required for this step, so make sure that [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) is installed. It is still possible to install the application, if you have no git installed, plese see 2.6.

> It is essential because of stability reasons, that you use the conposer version, which is embedded in our software. That is why `php composer.phar update` is used.

### 2.1. If you want to install AtroPIM and AtroDAM with demo data
```
git clone https://github.com/atrocore/skeleton-pim.git . && php composer.phar update
```

### 2.2. If want want to install the AtroPIM with AtroDAM without demo data
```
git clone https://github.com/atrocore/skeleton-pim-no-demo.git . && php composer.phar update
```

### 2.3. If you want to install AtroDAM with demo data
```
git clone https://github.com/atrocore/skeleton-dam.git . && php composer.phar update
```

### 2.4. If you want to install AtroDAM without demo data
```
git clone https://github.com/atrocore/skeleton-dam-no-demo.git . && php composer.phar update
```

### 2.5. If you want to install AtroCore only
Please install AtroDAM and than remove AtroDAM module via Administration > Module Manager.

### 2.6. Installation without `git` command
If you have no git installed you may still copy the files to the project folder manually.

You can download the files from one of this directory:
- https://github.com/atrocore/skeleton-pim
- https://github.com/atrocore/skeleton-pim-no-demo
- https://github.com/atrocore/skeleton-dam 
- https://github.com/atrocore/skeleton-dam-no-demo

Than upload the files to your project folder and run
```
php composer.phar update
```


   
## 3. Change recursively the user and group ownership for project files
```
chown -R www-data:www-data /var/www/my-atrocore-project/
```
>**www-data** – depends on your webserver and can be one of the following: www, www-data, apache, etc.

## 4. Change the permissions for project files
```
find . -type d -exec chmod 755 {} + && find . -type f -exec chmod 644 {} +;
find client data custom upload -type d -exec chmod 775 {} + && find client data custom upload -type f -exec chmod 664 {} +
```     
## 5. Configure the crontab

   5.1. Open crontab for www-data user:
```
crontab -e -u www-data
``` 
   5.2. Add the following configuration:
```      
* * * * * /usr/bin/php /var/www/my-atrocore-project/index.php cron 
```

## 6. Create MySQL database and user

User must have all privileges for database. You can create database and user with all privileges by executing next few commands:

> If MySQL Database is not installed, you need to install it.

Connect to MySQL as a root user:
```
mysql -u root -p
```
Create the database **atrocore**:
```
CREATE DATABASE atrocore;
```
Create user **atrocore_user** with password **atrocore_password** and grant all needed privileges:
```
CREATE USER atrocore_user@localhost;
ALTER USER atrocore_user@localhost IDENTIFIED BY 'atrocore_password';
GRANT ALL ON atrocore.* TO atrocore_user@localhost WITH GRANT OPTION;
```

## 7. Go to http://YOUR_PROJECT/ to start the installation wizard 

Start the installation wizard for your AtroCore Application in the web interface. Follow the instructions in the wizard.
