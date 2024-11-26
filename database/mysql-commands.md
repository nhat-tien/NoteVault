---
tags:
  - mysql
date: "2023-08-24"
stage: budding
---

## Start 

Services -> Khởi động thủ công -> MySQL80

## Shutdown

```bash
mysqladmin -u root -p shutdown 
```

### Check database current use

```sql
SELECT DATABASE() FROM DUAL;
```

### Check where mysql store data

```bash
mysql -e "show variables like 'datadir'"
```
## USER

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

## DATABASE

### Create database
```sql
CREATE DATABASE mydatabase;
```

### Delete database
```sql
DROP DATABASE mydatabase;
```

### Show databases

```sql
SHOW DATABASES;
```

### Use database
```sql
USE <database_name>;
```

### Show all table
```sql
SHOW TABLES;
```

### Show column in table
```sql
 DESCRIBE TABLES;
```

### Modify table 
```sql
ALTER TABLE <table-name> MODIFY <column-name> <data-type>;
```
