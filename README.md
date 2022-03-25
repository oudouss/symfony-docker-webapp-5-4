# Symfony Docker Webapp 5.4


## Introduction:

This is a Symfony version 5.4 webapp starter pre-configured to be used with the docker developement environment


## Installing Symfony Project:

After clonning the docker developement environment from [symfony-docker-env](https://github.com/oudouss/symfony-docker-env)

Clone the symfony project into codebase:
```

docker exec -it server bash

git clone https://github.com/oudouss/symfony-docker-webapp-5-4.git .

composer install
```

## Setting up database connection via .env file:

First run this command to create a local .env file

```
docker exec -it server bash
composer dump-env dev
```

You'll probably need to customize the created .env file in codebase according to your database choice:

```
#To use mysql include this line:
DATABASE_URL='mysql://${DB_USER}:${DB_PASS}@db_server:${DB_PORT_INSIDE}/${DB_NAME}?serverVersion=${DB_SERVER_VERSION}&charset=${DB_CHARSET}'


#To use mariadb include this line instead:
DATABASE_URL='mysql://${DB_USER}:${DB_PASS}@db_server:${DB_PORT_INSIDE}/${DB_NAME}?serverVersion=${DB_SERVER}-${DB_SERVER_VERSION}'

#To use postgresql include this line instead:
DATABASE_URL='postgresql://${DB_USER}:${DB_PASS}@db_server:${DB_PORT_INSIDE}/${DB_NAME}?serverVersion=${DB_SERVER_VERSION}&charset=${DB_CHARSET}'


#NOTE: 
By default a connection to mariadb-10.5.9 is already configured in .env file
You should replace ( ${DB_USER} , ${DB_PASS} , ${DB_PORT_INSIDE}, ${DB_NAME} , ${DB_SERVER} , ${DB_SERVER_VERSION} , ${DB_CHARSET} ) by their respective values from .env file in the 'symfony-docker-env' root directory

```


## Run database migrations and load fake data:

NOTE: Every command related to the symfony should be executed in the server container: 
```
docker exec -it server bash
```

Run migrations

```
php bin/console d:m:m --no-interaction 

OR

symfony console d:m:m --no-interaction 
```

Update schema

```
php bin/console d:s:u --force

OR

symfony console d:s:u --force
```

Load fake data

```
php bin/console d:f:l --no-interaction

OR

symfony console d:f:l --no-interaction
```

That's all! 

Go to [http://localhost](http://localhost) to see your app

Happy Hacking!