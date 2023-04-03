# README

```bash
docker run -it -e DATABASE_DRIVER='mysql' \
-e DATABASE_ENCODING='utf8' \
-e SAMPLE_DATA_LENGTH='100' \
-e DATABASE_HOST='host.docker.internal' \
-e DATABASE_PORT='3306' \
-e DATABASE_NAME='compalex_dev' \
-e DATABASE_USER='root' \
-e DATABASE_PASSWORD='password' \
-e DATABASE_DESCRIPTION='Developer database' \
-e DATABASE_HOST_SECONDARY='host.docker.internal' \
-e DATABASE_PORT_SECONDARY='3306' \
-e DATABASE_NAME_SECONDARY='compalex_prod' \
-e DATABASE_USER_SECONDARY='root' \
-e DATABASE_PASSWORD_SECONDARY='password' \
-e DATABASE_DESCRIPTION_SECONDARY='Production database' \
-p 8000:8000 dlevsha/compalex
```

You need to change variables for your own

`DATABASE_DRIVER` - database driver, possible value

- `mysql` - for MySQL database
- `pgsql` - for PostgreSQL database
- `dblib` - for Microsoft SQL Server database
- `oci` - for Oracle database

`DATABASE_HOST` and `DATABASE_HOST_SECONDARY` - database host name or IP for first and second server

If your compared DB run locally:

- for [MacOS](https://docs.docker.com/docker-for-mac/networking/) and [Windows](https://docs.docker.com/docker-for-windows/networking/)
  user: use `host.docker.internal` instead of `localhost` in `DATABASE_HOST` and `DATABASE_HOST_SECONDARY` param.
  Because we run script inside container we need to use Host machine IP for connection.

- for [Linux](https://docs.docker.com/network/host/) user: use `--network host` option and `localhost` in `DATABASE_HOST` and `DATABASE_HOST_SECONDARY` param.

If you connect to DB outside your machine (external IP) use: `-e DATABASE_HOST='[Your external IP]'`.

`DATABASE_PORT` and `DATABASE_PORT_SECONDARY` - database port for first and second server

Default ports for DB:

- `3306` - Mysql
- `5432` - PostgreSQL
- `1433` - MSSQL
- `1521` - Oracle

`DATABASE_NAME` and `DATABASE_NAME_SECONDARY` - first and second database name

`DATABASE_USER` / `DATABASE_PASSWORD` and `DATABASE_USER_SECONDARY` / `DATABASE_PASSWORD_SECONDARY` - login and password to access your databases

`DATABASE_DESCRIPTION` and `DATABASE_DESCRIPTION_SECONDARY` - server description (not necessary). For information only. These names will display as a database name.

You can also use `docker-compose.yml`.

```
version: "3.7"

services:
  compalex:
    image: dlevsha/compalex
    container_name: compalex
    environment:
      - DATABASE_DRIVER=mysql
      - DATABASE_ENCODING=utf8
      - SAMPLE_DATA_LENGTH=100
      - DATABASE_HOST=host.docker.internal
      - DATABASE_PORT=3306
      - DATABASE_NAME=compalex_dev
      - DATABASE_USER=root
      - DATABASE_PASSWORD=password
      - DATABASE_DESCRIPTION=Developer database
      - DATABASE_HOST_SECONDARY=host.docker.internal
      - DATABASE_PORT_SECONDARY=3306
      - DATABASE_NAME_SECONDARY=compalex_prod
      - DATABASE_USER_SECONDARY=root
      - DATABASE_PASSWORD_SECONDARY=password
      - DATABASE_DESCRIPTION_SECONDARY=Production database
    ports:
      - "8000:8000"
```

## Requirements

If you prefer use Compalex as PHP script please read instruction bellow.

Compalex is only supported by PHP 5.4 and up with PDO extension.

## Installation

    $ git clone https://github.com/trekkiebigyan/Database-Compare.git
    $ cd compalex

Open `.environment`. You'll see configuration params

```ini
[ Main settings ]
; Possible DATABASE_DRIVER: 'mysql', 'pgsql', 'dblib', 'oci'.
; Please use 'dblib' for Microsoft SQL Server
DATABASE_DRIVER = mysql
DATABASE_ENCODING = utf8
SAMPLE_DATA_LENGTH = 100

[ Primary connection params ]
DATABASE_HOST = localhost
DATABASE_PORT = 3306
DATABASE_NAME = compalex_dev
DATABASE_USER = root
DATABASE_PASSWORD =
DATABASE_DESCRIPTION = Developer database

[ Secondary connection params ]
DATABASE_HOST_SECONDARY = localhost
DATABASE_PORT_SECONDARY = 3306
DATABASE_NAME_SECONDARY = compalex_prod
DATABASE_USER_SECONDARY = root
DATABASE_PASSWORD_SECONDARY =
DATABASE_DESCRIPTION_SECONDARY = Production database
```

where

`DATABASE_DRIVER` - database driver, possible value

- `mysql` - for MySQL database
- `pgsql` - for PostgreSQL database
- `dblib` - for Microsoft SQL Server database
- `oci` - for Oracle database

`[ Primary connection params ]` and `[ Secondary connection params ]`sections describes settings for first and second databases.

Where

`DATABASE_HOST` and `DATABASE_HOST_SECONDARY` - database host name or IP for first and second server

`DATABASE_PORT` and `DATABASE_PORT_SECONDARY` - database port for first and second server

Default ports:

- `3306` - Mysql
- `5432` - PostgreSQL
- `1433` - MSSQL
- `1521` - Oracle

`DATABASE_NAME` and `DATABASE_NAME_SECONDARY` - first and second database name

`DATABASE_USER` / `DATABASE_PASSWORD` and `DATABASE_USER_SECONDARY` / `DATABASE_PASSWORD_SECONDARY` - login and password to access your databases

`DATABASE_DESCRIPTION` and `DATABASE_DESCRIPTION_SECONDARY` - server description (not necessary). For information only. These names will display as a database name.

Inside `compalex` directory run

    $ php -S localhost:8000

Now open your browser and type `http://localhost:8000/`

You'll see database schema of two compared databases.

-
