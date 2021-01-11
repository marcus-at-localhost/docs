## Nginx server configuration

Please update your nginx configuration with the following:
```
server {
  ...
  client_max_body_size 200M;

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
