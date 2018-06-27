# docker-mac-php-performance
Using native PHP with dockerized services (e.g. nginx) as a way to deal with bind mounts performance problem on docker-for-mac

# Configs
* `docker-compose.yml` - basic config
* `docker-compose.prod.yml` - The default way of running php apps using docker. Everything in containers
* `docker-compose.dev.yml` - Dockerized nginx uses natively installed PHP

# Set up
1. Install native php 7.2 `brew install php72`
2. Download [Composer](https://getcomposer.org/)
3. Install dependencies `php composer.phar install`


# Native php + dockerized nginx
Start php-fpm service
```
brew services start php@7.2
```
Start docker-compose with dev config
```
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --force-recreate --remove-orphans
```
Check results [http://localhost:8080/app_dev.php](http://localhost:8080/app_dev.php)

# Dockerized php + dockerized nginx
Start docker-compose with production config
```
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d --force-recreate --remove-orphans
```
Check results [http://localhost:8080/app_dev.php](http://localhost:8080/app_dev.php)
rm
# Results
How long it takes to load Symfony 3.4 default homepage on PHP 7.2 with warm cache.

Dockerized php + dockerized nginx: 1100 ms

Native php + dockerized nginx: 13 ms