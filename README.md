Once all the containers are up, our services are available at:  
    Symfony app: http://symfony.dev:80  
    Mysql server: symfony.dev:3306  
    Redis: symfony.dev:6379  
    Log files location: logs/nginx and logs/symfony  
    Of course when localhost -> symfony.dev in hosts, otherwise access via localhost  

Remember to setup db connection in Symfony .env file:
    DATABASE_URL=mysql://symfony_user:symfony_password@mysql:3306/symfony_db

For JWT authentication don't forget to change permissions in Docker to something readable from outside, in my case for local:  

    docker-compose exec php chmod -R 777 config/jwt


In case of problems with alcaeus/mongodb add
  --ignore-platform-reqs
to composer commands. To be fixed later.  

Fix:  
    composer config "platform.ext-mongo" "1.6.16" && composer require alcaeus/mongo-php-adapter

Full setup:
    cp .env.dist .env  
    cd symfony-app && cp .env.dist .env  
    docker-compose build  
    docker-compose up -d  
    docker ps -a  

For Mongo and cache the following needs to be done:  
    chown www-data:www-data var/cache/
    chmod -R 777 var/cache/