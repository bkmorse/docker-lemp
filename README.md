# docker
Run Nginx, php-fpm and MariaDB using [Docker]

## Requirements
Install [Docker] and [Compose]

## Containers
- php 7.1
- nginx
- mysql 5.7
- mailhog
- redis

## PHP Libraries
- curl
- mcrypt
- gd
- png
- composer
- zip
- mysqli
- pdo_mysql
- soap

## Environment file
```
copy env.example .env
```
Once copied, set the db settings and set project name, it will prefix the containers with that project name

## NGINX config
Modify docker/nginx.conf server_name to be the local dev url
Then modify your /etc/hosts file by adding:
```
127.0.0.1 projectname.local
```
Modify the nginx.conf to point to the right public folder, for example: path/to/public, or path/to/web

## Mailhog
Access the frontend of mailhog by pointing your web browser to:
http://projectname.local:8025 or http://localhost:8025

The SMTP server will be: localhost, and the port: 1025

## Connecting to database
host: 127.0.0.1
port: 3306

Set the username and password as you set it in the .env file

## Usage
```
docker-compose build (run the first time and anytime you modify the setup)
docker-compose up -d
docker-compose logs
docker-compose stop
docker-compose rm
```