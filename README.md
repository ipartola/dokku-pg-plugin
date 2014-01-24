PostgreSQL plugin for Dokku
---------------------------

Project: https://github.com/progrium/dokku

**Warning: This plugin is under development and still only tested with the below dependencies**

Requirements
------------
* dokku-link plugin: https://github.com/rlaneve/dokku-link

Installation
------------
```
cd /var/lib/dokku/plugins
git clone https://github.com/jlachowski/dokku-pg-plugin postgresql
dokku plugins-install
```


Commands
--------
```
$ dokku help
    postgresql:create <app>           Create a PostgreSQL container for <app>
    postgresql:clone <app> <trg>      Clone PostgreSQL container of <app> for <trg>
    postgresql:rebuild <app>          Rebuil PostgreSQL container of <app> (keep persistend data)
    postgresql:delete <app>           Delete specified PostgreSQL container for <app>
    postgresql:info <app>             Display <app> PostgreSQL container informations
    postgresql:link <app> <pgsql>     Link an app to a PostgreSQL container
    postgresql:list                   Display list of PostgreSQL containers
    postgresql:logs <app>             Display last logs from <app> PostgreSQL container
```

Simple usage
------------

Create a new DB:
```
$ dokku postgresql:create foo            # Server side
$ ssh dokku@server postgresql:create foo # Client side

```

Deploy your app with the same name (client side):
```
$ git remote add dokku git@server:foo
$ git push dokku master

```

Link your app to the database
```bash
dokku postgresql:link app_name database_name
```


Advanced usage
--------------

Inititalize the database with SQL statements:
```
cat init.sql | dokku postgresql:create foo
```

Deleting databases:
```
dokku postgresql:delete foo
```

Clone databases (foo to bar):
```
dokku postgresql:clone foo bar
```

Rebuilding container (preserves database):
```
dokku postgresql:rebuild foo
```

Linking an app to a specific database:
```
dokku postgresql:link foo bar
```

PostgreSQL logs (per database):
```
dokku postgresql:logs foo
```

Database informations:
```
dokku postgresql:info foo
```

List of containers:
```
dokku postgresql:list
```
