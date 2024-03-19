# Laravel

This is a docker configuration for laravel project.
In this config you need to have a working docker and docker-compose in your system

## Usage

1. Make sure you already set your .env file
2. If you are using my configuration for the database

```bash
# use the container name for the mysql container
DB_HOST=mysql_container-mysql-1
```

3. Copy Dockerfile, docker-compose.yml, and makefile to root folder
4. Run, make setup in your console

```bash
make setup
```
