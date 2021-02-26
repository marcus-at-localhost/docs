# Nginx server configuration
> all configuration settings listed here are made on Ubuntu server.

### PHP requirements
To install all necessary libraries, run these commands in the terminal:
```
sudo apt-get update
sudo apt-get install php-mysql php-json php-gd php-zip php-imap php-mbstring php-curl ghostscript php-mailparse php-imagick
sudo phpenmod imap mbstring
sudo service nginx restart
```

### Enable rewrite rules in Nginx server
Add this code to your Nginx server block config file (/etc/nginx/sites-available/YOUR_SITE) inside server block:
```
server {
  # ...

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
