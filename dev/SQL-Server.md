---
date: 2023-09-08
tags:
  - sqlserver
---
# SQL Server

```sh
sqlcmd -S ADMIN-PC -E
```

## Command
### Stop/Start SQL SERVER

❗ Mở terminal bằng quyền quản trị 

```sh
net {stop|start} "SQL Server (MSSQLSERVER)"
```

### print the structure of a table

```sql
DESC table_name
```
