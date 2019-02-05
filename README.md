# About this Repo
This is the Git repo of the Docker [official image](https://docs.docker.com/docker-hub/official_repos/) for [rails] (https://registry.hub.docker.com/_/rails/) and [mysql](https://hub.docker.com/_/mysql/). See these page for the full readme on how to use this Docker image and for information regarding contributing and issues.

## Pre-Requirements
First install `docker`, `docker compose` for your machine and start it. How this is done is very well documented all over the internet.

### Run the project
You need generate the Rails skeleton app using docker-compose run:
```
$ docker-compose up
```
### Enter app container
```
$ docker-compose run app bash
```

### Connect the database
The app is now bootable, but you’re not quite there yet. By default, Rails expects a database to be running on `localhost` - so you need to point it at the `mysql container` instead. You also need to change the database and username to align with the defaults set by the mysql image.

Replace the contents of config/database.yml with the following:
```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: 5
  username: root
  password: "root"
  host: mysql

development:
  <<: *default
  database: demo_development

test:
  <<: *default
  database: demo_test
```

You can now boot the app with:
```
docker-compose up -d
```

Finally, you need to create the database. In another terminal, run:
```
docker-compose run app rake db:create
```

That’s it. Your app should now be running on port 3000 on your Docker daemon. If you’re using Docker Machine, then `docker-machine ip MACHINE_VM` returns the Docker host IP address.
```
$ docker-machine ip default
192.168.99.100
```

http://192.168.99.100:3000/

![rails](https://cloud.githubusercontent.com/assets/5398914/20524938/578c3872-b100-11e6-8a7f-d359f982bd24.png)

To stop container then run following command:
```
$ docker-compose stop
Stopping ror_app_1 ... done
Stopping ror_mysql_1 ... done
```

To start container again then run following command:
```
$ docker-compose start
Starting dbdata ... done
Starting appdata ... done
Starting mysql ... done
Starting app ... done
```
