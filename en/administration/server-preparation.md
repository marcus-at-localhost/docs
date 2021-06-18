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

So, to only allow traffic on port 80 and 443, use the Apache profile:
```
sudo ufw allow in "Apache Full"
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
Apache                     ALLOW       Anywhere                  
Apache Full                ALLOW       Anywhere                  
Apache (v6)                ALLOW       Anywhere (v6)             
Apache Full (v6)           ALLOW       Anywhere (v6)  
```
Traffic on port 80 and 443 is now allowed through the firewall.
You can do a spot check right away to verify that everything went as planned by visiting your server’s public IP address in your web browser:
```
http://your_server_ip 
```
You’ll see the default Ubuntu 20.04 Apache web page. It should look something like this:
![apache_default](../../_assets/administration/server-preparation/apache_default.png)