# Nginx server configuration
> all configuration settings listed here are made on Ubuntu server.

## 1. Install all necessary PHP libraries
To install all necessary libraries, run these commands in the terminal:
```
sudo apt-get update
sudo apt-get install php-mysql php-json php-gd php-zip php-imap php-mbstring php-curl ghostscript php-mailparse php-imagick
sudo phpenmod imap mbstring
sudo service nginx restart
```

## 2. Configure a Virtual Host on Nginx
To create this file, open a terminal and run the command:
```
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/atrocore.conf
```
Open this file (`/etc/nginx/sites-available/atrocore.conf`) and modify the code following the format printed below (some settings may be different based on your configuration):
```
server {
  listen 80;
  root /var/www/atrocore.local; ## Specify your document root
  server_name apropim.local;  ## Replace apropim.local to your domain name
  server_tokens off; ## Don't show the nginx version number
  index index.php index.html;
  resolver 172.17.0.1 valid=60s ipv6=off;

  client_max_body_size 50M;
  
  location ~ (composer\.json)$ {
    deny all;
  }
  
  location ~ /\.ht {
    deny all;
  }
  
  location / {
    try_files $uri $uri/ @router;
    index index.html index.php;
    error_page 403 = @router;
    error_page 404 = @router;
  }

  location @router {    
    rewrite ^/(.*)$ /index.php?treoq=$1;
  }

  location ~ \.php$ {
    try_files $fastcgi_script_name =404;
    fastcgi_keep_conn on;
    fastcgi_pass unix:/var/run/php-fpm.sock;
    include fastcgi_params;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
  }
  
}
```
## 3. Restart Nginx
```
sudo service nginx restart
```
