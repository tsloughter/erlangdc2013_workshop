## ErlangDC 2013 Heroku Workshop

### Signup

http://api.heroku.com/signup

### Install

https://toolbelt.heroku.com/

##### Login

```
$ ssh-keygen -t rsa
$ heroku keys:add
$ heroku login
```

### Project

```
$ git clone https://github.com/tsloughter/erlangdc2013.git
```

http://postgresapp.com/ or ```sudo apt-get install postgresql```

```
λ sudo -u postgres createdb erlangdc
λ psql erlangdc
=> create table users (
       id text not null,                                                        
       apikey text not null,
       name text not null,
       email text not null,
       password_hash text not null,
       admin boolean not null default false,
       active boolean not null default true,
       created_at timestamp with time zone not null default localtimestamp,
       updated_at timestamp with time zone not null default localtimestamp
       );
=> insert into users (id, apikey, name, email, password_hash)
       values ('1', 'apikey_value', 'John', 'john@email.com', 'password_hash_value');
```

```
$ make rel
$ PORT=8080 DATABASE_URL=postgres://<username>:<password>@localhost:5432/erlangdc ./_rel/bin/erlangdc2013
```

### Create Heroku App

```shell
$ heroku create --buildpack https://github.com/tsloughter/heroku-buildpack-erlang.git
```

#### About Erlang Buildpack

* rebar
* relcool
* .preferred_otp_version

### Testing Locally

#### Foreman

Command-line tool for running Procfile-backed apps

```
$ foreman start
```

### Addons

### Setup Database

```
$ heroku addons:add heroku-postgresql:dev
$ heroku pg:info
=== HEROKU_POSTGRESQL_ORANGE_URL (DATABASE_URL)
Plan:        Dev
Status:      available
Connections: ?
PG Version:  ?
Created:     2013-02-08 16:21 UTC
Data Size:   0 B
Tables:      1
Rows:        0/10000 (In compliance)
Fork/Follow: Unsupported
$ heroku pg:psql HEROKU_POSTGRESQL_ORANGE_URL
=> create table users (
       id text not null,                                                        
       apikey text not null,
       name text not null,
       email text not null,
       password_hash text not null,
       admin boolean not null default false,
       active boolean not null default true,
       created_at timestamp with time zone not null default localtimestamp,
       updated_at timestamp with time zone not null default localtimestamp
       );
       
=> insert into users (id, apikey, name, email, password_hash)
       values ('1', 'apikey_value', 'John', 'john@email.com',
       'password_hash_value');
=> \q       
```

### Deploying

#### Push

```
$ git push heroku master
```

```
$ heroku ps:scale web=1
```

#### Processes

```
$ heroku ps
```

#### Releases

```
$ heroku releases
```

### Logs

#### Tail

```
$ heroku logs -t
```

#### Drain to Papertrail

```
$ heroku addons:add papertrail:choklad
$ heroku addons:open papertrail
```

### DataClips

https://postgres.heroku.com/databases

https://dataclips.heroku.com/

### Metrics

```
$ heroku addons:add librato:test
```

### Rollback

```
$ git push heroku master
-- AAAAAAAAAA IT BROKE
$ heroku rollback
```

### Coding Time

* Add POST support for adding new users
* Add DELETE support for removing users
