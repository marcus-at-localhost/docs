# Linux Server Preparation
This guide describing how to prepare server for an installation.

> Installation guide is based on **Ubuntu 20.04**.

## 1. Installing Apache and Updating the Firewall
The Apache web server is among the most popular web servers in the world. It’s well documented, has an active community of users, and has been in wide use for much of the history of the web, which makes it a great default choice for hosting a website.

Install Apache using Ubuntu’s package manager, ```apt```:
```
sudo apt update
sudo apt -y install apache2
```
Once the installation is finished, you’ll need to adjust your firewall settings to allow HTTP traffic. UFW has different application profiles that you can leverage for accomplishing that. To list all currently available UFW application profiles, you can run:
```
sudo ufw app list
```
You’ll see output like this:
```
Available applications:
  Apache
  Apache Full
  Apache Secure
  OpenSSH
```
Here’s what each of these profiles mean:
* **Apache**: This profile opens only port 80 (normal, unencrypted web traffic).
* **Apache Full**: This profile opens both port 80 (normal, unencrypted web traffic) and port 443 (TLS/SSL encrypted traffic).
* **Apache Secure**: This profile opens only port 443 (TLS/SSL encrypted traffic).

So, to allow traffic on port 80 and 443, use the Apache profile:
```
sudo ufw allow in "Apache Full"
sudo ufw allow in "OpenSSH" # OPTIONAL. In case if you just enable firewall, don't forget to allow ssh connection, because it can be your last connection :)
```
You can verify the change with:
```
sudo ufw status
```
You’ll see output like this:
```
Status: active

To                         Action      From
--                         ------      ----
Apache Full                ALLOW       Anywhere                  
OpenSSH                    ALLOW       Anywhere                  
Apache Full (v6)           ALLOW       Anywhere (v6)             
OpenSSH (v6)               ALLOW       Anywhere (v6)
```
Traffic on port 80 and 443 is now allowed through the firewall.
You can do a spot check right away to verify that everything went as planned by visiting your server’s public IP address in your web browser:
```
http://your_server_ip 
```
You’ll see the default Ubuntu 20.04 Apache web page. It should look something like this:
![apache_default](../../_assets/administration/server-preparation/apache_default.png)

## 2. Installing MySQL
Now that you have a web server up and running, you need to install the database system to be able to store and manage data for your site. MySQL is a popular database management system used within PHP environments.

Again, use ```apt``` to acquire and install this software:
```
sudo apt -y install mysql-server
```
When the installation is finished, it’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Start the interactive script by running:
```
sudo mysql_secure_installation 
```
This will ask if you want to configure the ```VALIDATE PASSWORD PLUGIN```.

> **Note:** Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. It is safe to leave validation disabled, but you should always use strong, unique passwords for database credentials.

Answer ```Y``` for yes, or anything else to continue without enabling.
```
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No: 
```
If you answer “yes”, you’ll be asked to select a level of password validation. Keep in mind that if you enter ```2``` for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words.

Regardless of whether you chose to set up the ```VALIDATE PASSWORD PLUGIN```, your server will next ask you to select and confirm a password for the MySQL **root** user. This is not to be confused with the **system root**. The **database root** user is an administrative user with full privileges over the database system.

If you enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to continue with that password. If you are happy with your current password, enter ```Y```. For the rest of the questions, press ```Y``` and hit the ENTER key at each prompt.

When you’re finished, test if you’re able to log in to the MySQL console by typing:
```
sudo mysql 
```
This will connect to the MySQL server as the administrative database user **root**, which is inferred by the use of sudo when running this command. You should see output like this:
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 8.0.25-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```
To exit the MySQL console, do:
```
Ctrl + D
```