---
date: "2024-08-23"
tags:
  - laravel
hub: ""
---

```bash
cd /etc/systemd/system/
touch laravel-app.service
vi laravel-app.service 
```

```txt
[Unit]
Description=Vstep Octane

[Service]
User=www-data
Group=www-data
Restart=on-failure
ExecStart=/usr/bin/php /var/www/vstep-be/artisan octane:start
ExecStop=/usr/bin/php /var/www/vstep-be/artisan octane:stop

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable laravel-app.service
sudo systemctl start laravel-app.service
```

When make a change in service file, you had to run: 

```bash
sudo systemctl daemon-reload 
sudo systemctl restart laravel-app.service
```
