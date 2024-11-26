
[https://stackoverflow.com/questions/45473624/laravel-migrate-specific-files-from-migrations/45473710#45473710](https://stackoverflow.com/questions/45473624/laravel-migrate-specific-files-from-migrations/45473710#45473710) 

Just look at the migrations table in your database, there will be a list of migration file name and batch number value.

Suppose you have following structure,

id     migration                                           batch

1      2014_10_12_000000_create_users_table                  1 
2      2014_10_12_100000_create_password_resets_table        1
3      2016_09_07_103432_create_tabel_roles                  1


If you want to just rollback 2016_09_07_103432_create_tabel_roles migration, change it's migration batch value to 2 which is highest among all and then just execute following.

```bash
php artisan migrate:rollback
```
Here only table with batch value 2 will be rolled back. Now, make changes to that table and run following console command.

```bash 
php artisan migrate
```

Batch value in the migrations table defines order of the migrations. when you rollback, migrations that are latest or have highest batch value are rolled back at first and then others. So, you can change the value in database and then rollback a particular migration file.

Although it's not a good idea to change batch number every time because of relationship among the table structure, we can use this case for some cases where single table rollback doesn't violates the integrity among the tables.

Hope you understand.
