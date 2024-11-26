

edit in `/etc/php/8.3/cli/php.ini`

> [!NOTE] 
> If you use php-fpm, edit in `/etc/php/8.3/fpm/php.ini`

```txt
upload_max_filesize= 950M 
```

and 

```txt
post_max_size = 950M 
```

If above solution not work, you may consider try this:
edit/add in `/etc/nginx/nginx.conf`

```txt
http {
      client_max_body_size 20M;         
}
```
