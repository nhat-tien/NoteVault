---
date: "2024-09-06"
tags:
  - linux
  - laravel
hub: "" 
---

## vendor does not exist and could not be created

Add your user in the www-data group (this action require you to logout and login again)

```bash
sudo usermod -a -G www-data `whoami`
```

Give the right permissions to /var/www

```bash
sudo chown root:root /var/www
sudo chmod 755 /var/www/
```

Give these permissions to your project

```bash
sudo chown -R www-data:www-data /var/www/<project>
sudo chmod -R 774 /var/www/<project>
```

[https://stackoverflow.com/questions/22390001/runtimeexception-vendor-does-not-exist-and-could-not-be-created](https://stackoverflow.com/questions/22390001/runtimeexception-vendor-does-not-exist-and-could-not-be-created) 
