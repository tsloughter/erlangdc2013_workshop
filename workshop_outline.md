## ErlangDC 2013 Heroku Workshop

### Architecture

#### Platform

* Dynos
* Routing
* Slugs

#### Application

* Buildpacks
* Processes
** Web
** Workers

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

```
$ make rel
$ ./_rel/bin/erlangdc2013
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
$ heroku pg:psql DATABASE_URL
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

### Deploying

#### Push

```
$ git push heroku master
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

### Metrics

### Additional

* Custom Domains
* SSL
