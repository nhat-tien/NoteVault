
## Mysql
```bash
docker run -d \
  --name db \
  -e MYSQL_DATABASE=database_name \
  -e MYSQL_ROOT_USER=root \
  -e MYSQL_ROOT_PASSWORD=mypassword \
  -p 3306:3306 \
  -v db-mysql:/var/lib/mysql \
  -v $(pwd)/db-mysql/init.sql:/docker-entrypoint-initdb.d/init.sql \
  mysql:8.0
```


