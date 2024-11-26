---
date: 2023-12-19
tags:
  - mongodb
---

[Stackoverflow](https://stackoverflow.com/questions/4881208/how-to-secure-mongodb-with-username-and-password)

I want to set up user name & password authentication for my MongoDB instance, so that any remote access will ask for the user name & password. I tried the tutorial from the MongoDB site and did following:

```javascript
use admin
db.addUser('theadmin', '12345');
db.auth('theadmin','12345');
```

After that, I exited and ran mongo again. And I don't need password to access it. Even if I connect to the database remotely, I am not prompted for user name & password.

---

**UPDATE** Here is the solution I ended up using

```javascript
1) At the mongo command line, set the administrator:

    use admin;
    db.addUser('admin','123456');

2) Shutdown the server and exit

    db.shutdownServer();
    exit

3) Restart mongod with --auth

  $ sudo ./mongodb/bin/mongod --auth --dbpath /mnt/db/

4) Run mongo again in 2 ways:

   i) run mongo first then login:

        $ ./mongodb/bin/mongo localhost:27017
        use admin
        db.auth('admin','123456');

  ii) run & login to mongo in command line.

        $ ./mongodb/bin/mongo localhost:27017/admin -u admin -p 123456
```

The username & password will work the same way for `mongodump` and `mongoexport`.