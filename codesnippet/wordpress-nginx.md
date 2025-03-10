---
date: 2024-01-21
tags:
  - nginx
  - wordpress
---
```
server {
    listen 80;
    server_name wordpresstest.net;
    root /var/www/wordpresstest.net;

    index index.html index.htm index.php;

    location / {
       # try_files $uri $uri/ =404;
	try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

    location = /favicon.ico { log_not_found off; access_log off; }
    location = /robots.txt { log_not_found off; access_log off; allow all; }
    location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
        expires max;
        log_not_found off;
    }
    
    include snippets/phpmyadmin.conf;
}
```
