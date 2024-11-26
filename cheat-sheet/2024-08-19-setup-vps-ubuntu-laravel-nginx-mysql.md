
## System info

- Ubuntu 22.04

## Install nginx

```bash
sudo apt update
sudo apt install nginx
```

## Adjusting the firewall

```bash
# enable fireewall
sudo ufw enable
# allow port 22 for ssh
sudo ufw allow 22
# check status
sudo ufw status
# enable for Nginx
sudo ufw allow 'Nginx HTTP'
# sudo ufw app list
```

## Mysql

### Install

```bash
sudo apt install mysql-server
```

### Run security script 

```bash
sudo mysql_secure_installation
```

if you run into error, check [this](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04#step-2-configuring-mysql) 

### (Optional)  Set password for root

By default, you can access root by 

```bash
sudo mysql -u root
```

It use `auth_socket`, but, if you like, you can set password for root

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

### Create user
```sql
CREATE USER '<user_name>'@'localhost' IDENTIFIED BY '<password>';
```

### Granting a User Permissions
```sql
USE my_db;
-- GRANT ALL ON my_db.* TO 'my_user'@'%';
-- If you create user with localhost, use below 
GRANT ALL ON my_db.* TO 'my_user'@'localhost';
```

### List all user
```sql
SELECT user FROM mysql.user;
```

[[mysql-commands]]

## Clone repo to /var/www

### Copy .env

## Change file permission

check [here](https://viblo.asia/p/laravel-file-permission-aWj53B8pl6m)  

```bash
# This work for me
sudo chown -R $USER:www-data storage
sudo chmod -R 775 storage
```

## PHP

If your ubuntu not have php version you want, then

### Add PHP Repository

```bash
sudo apt install ca-certificates apt-transport-https software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
```

### Now check apt

```bash
# replace X.X by php version you want
apt search phpX.X 
```

If success, move on next step

### Install PHP

#### Base

```bash
sudo apt install php8.3 php8.3-fpm php8.3-dom php8.3-xml php8.3-intl php8.3-zip php8.3-mysql php8.3-mbstring
```

#### For Mysql database


## Install Composer 

```bash
curl -sS https://getcomposer.org/installer -o composer-setup.php
php composer-setup.php
sudo mv composer.phar /usr/local/bin/composer 
```

## Setup nginx

```bash
cd /etc/nginx/sites-available 
touch <app-name>
vi <app-name>
```

**Example** [[bus_online]]
See error below [[#**Problem**: File not found, display nginx 404 page (instead laravel 404 page)]]

```txt
server {
    listen 80;
    server_name bus_online;
    root /var/www/bus_online_server/public;

    index index.html index.htm index.php;

    location / {
       # try_files $uri $uri/ =404;
	try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
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
}
```

**Restart Nginx**

```bash
sudo systemctl restart nginx
```

## Setup .env

## Troubleshoting

### Set up max size file upload 

[[upload-file-size]]


### **Problem**: The POST method is not supported for route admin/login. Supported methods: GET, HEAD.

**Solution**:
```bash
php artisan vendor:publish --force --tag=livewire:assets
```
[link](https://github.com/filamentphp/filament/discussions/11481) 

### **Problem**: File not found, display nginx 404 page (instead laravel 404 page)

**Solution**: I dont know how this work for me, I remove the code snip in nginx config

```txt
server {
    listen 80;
    server_name bus_online;
    root /var/www/bus_online_server/public;

    index index.html index.htm index.php;

    location / {
       # try_files $uri $uri/ =404;
       try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

    location = /favicon.ico { log_not_found off; access_log off; }
    location = /robots.txt { log_not_found off; access_log off; allow all; }

    # --------- COMMENT THIS BLOCK -----------
    # location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
    #    expires max;
    #    log_not_found off;
    # }    
    # ----------------------------------------
}
```

### set up octane swoole

> Remember correct the version

```bash
sudo apt install php7.4-swoole
```

```txt
server {
    listen 80;
    server_name bus_online;
    root /var/www/bus_online_server/public;

    index index.html index.htm index.php;

    charset utf-8;

    location / {
       # try_files $uri $uri/ =404;
       # try_files $uri $uri/ /index.php$is_args$args;
       try_files $uri $uri/ @octane;
    }
    
    location /index.php {
        try_files /not_exists @octane;
    }

# location ~ \.php$ {
#       include snippets/fastcgi-php.conf;
#       fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
#    }

    location ~ /\.ht {
        deny all;
    }

    location = /favicon.ico { log_not_found off; access_log off; }
    location = /robots.txt { log_not_found off; access_log off; allow all; }

    location @octane {
        set $suffix "";
 
        if ($uri = /index.php) {
            set $suffix ?$query_string;
        }
 
        proxy_http_version 1.1;
        proxy_set_header Host $http_host;
        proxy_set_header Scheme $scheme;
        proxy_set_header SERVER_PORT $server_port;
        proxy_set_header REMOTE_ADDR $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
 
        proxy_pass http://127.0.0.1:8000$suffix;
    }

    # --------- COMMENT THIS BLOCK -----------
    # location ~* \.(css|gif|ico|jpeg|jpg|js|png)$ {
    #    expires max;
    #    log_not_found off;
    # }    
    # ----------------------------------------
}
```


