# docker-symfony
[![Build Status](https://travis-ci.org/jvancoillie/docker-symfony.svg?branch=master)](https://travis-ci.org/jvancoillie/docker-symfony)

A complete development environment to run a Symfony project including 
* [NGINX](https://www.nginx.com)
* [PHP-FPM](https://php-fpm.org)
* [MySQL](https://www.mysql.fr)
* [Redis](https://redis.io)
* ELK (optional)
  * [Elasticsearch](https://www.elastic.co/products/elasticsearch)
  * [Logstash](https://www.elastic.co/products/logstash)
  * [Kibana](https://www.elastic.co/products/kibana)

## Installation

First, clone this repository:
 ```bash
    $ git clone git@github.com:jvancoillie/docker-symfony.git
 ```
 
Create a `.env` from the `.env.dist` fileand change the relevant values for your setup.
 ```bash
    cp .env.dist .env
 ```
 
Run:
 ```bash
     $ docker-compose up -d
 ```
 
## How it works?
 
 Have a look at the `docker-compose.yml` file, here are the `docker-compose` built images:
 
 * `php`: This is the PHP-FPM container based on my [jvancoillie/php-fpm-symfony](https://hub.docker.com/r/jvancoillie/php-fpm-symfony/) docker repository,
 * `db`: This is the MySQL database container,
 * `redis`: This is the Redis in-memory data structure store container,
 * `nginx`: This is the Nginx webserver container based on my [jvancoillie/nginx-symfony](https://hub.docker.com/r/jvancoillie/nginx-symfony/) docker repository,
 * `kibana`: This is the Kibana (Elasticsearch data visualizer) container,
 * `elasticsearch`: This is the Elasticsearch container,
 * `logstash`: This is the logstash server-side data processing pipeline container.
 
 This results in the following running containers:
 
 ```bash
 $ docker-compose ps
          Name                        Command               State                       Ports                      
------------------------------------------------------------------------------------------------------------------
dockersymfony_db_1         docker-entrypoint.sh mysqld      Up      0.0.0.0:3306->3306/tcp                         
dockersymfony_kibana_1     /docker-entrypoint.sh kibana     Up      0.0.0.0:5601->5601/tcp                         
dockersymfony_logstash_1   /docker-entrypoint.sh -f / ...   Up      0.0.0.0:5000->5000/tcp                         
dockersymfony_nginx_1      /bin/sh -c /usr/bin/create ...   Up      443/tcp, 0.0.0.0:80->80/tcp                    
dockersymfony_php_1        php-fpm                          Up      0.0.0.0:9000->9000/tcp                         
dockersymfony_redis_1      docker-entrypoint.sh redis ...   Up      0.0.0.0:6379->6379/tcp                         
elasticsearch              /docker-entrypoint.sh elas ...   Up      0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp      
 ```
 
## Useful commands
 
 ```bash
 # bash commands
 $ docker-compose exec php bash
 
 # Composer (e.g. composer update)
 $ docker-compose exec php composer update
 
 # MySQL commands
 $ docker-compose exec db mysql -uroot -p"root"
 ```
