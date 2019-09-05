Here are steps for running a Drupal development site by running separate Docker containers on Mac OS X.

### Step 1 - Install Docker

[Download Docker for Mac here](https://hub.docker.com/?overlay=onboarding)

### Step 2 - Launch the Database Container

Run this command to launch a MySQL database container, using [Mariadb](https://hub.docker.com/_/mariadb):

`docker run --name mysql -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=drupal -e MYSQL_USER=drupal -e MYSQL_PASSWORD=drupal -v $PWD/data:/docker-entrypoint-initdb.d -d mariadb`

This command will automatically import SQL files in the `data` subdirectory of the current folder.

Customize the `-e` environment variables as needed.

### Step 3 - Import your Database

If you are recreating an existing Drupal instance, place a `staging.sql` file in your codebase folder and import database like this:

`docker exec -i mysql sh -c 'exec mysql -udrupal -p"drupal" drupal' < staging.sql`

### Step 4 - Edit Database Settings

If you using an existing Drupal codebase, edit the Drupal config file at `sites/default/settings.php` to match your database credentials from Step 1.

To install a fresh instance of Drupal from your local code, delete `settings.php`. During the install process, be sure to set the database host to `mysql`.

### Step 5 - Launch the Drupal Container

Run this command to launch a [Drupal container](https://hub.docker.com/_/drupal) that runs an Apache web server & PHP, and serves your current local folder on port 80:

`docker run --name drupal --link mysql:mysql -p 8000:80 -v $PWD:/var/www/html -d drupal:latest`

`$PWD` can also be an absolute path to the host folder, i.e. `/host/path`. You may need to add the folder to the File Sharing list in Docker Desktop's preferences.

Replace `8000` with desired port.

### Step 5 (Alternate) - Launch a Fresh Drupal Container

To launch an untouched version of Drupal for debugging purposes, omit the `-v` volume sharing:

`docker run --name drupal --link mysql:mysql -p 8000:80 -d drupal:latest`

During the install process, be sure to set the database host to `mysql`.

Replace `drupal:latest` with the desired [Drupal version](https://hub.docker.com/_/drupal?tab=tags).

### Step 6 - View the Drupal Site

You should now be able to view your site in the browser at http://localhost

### Step 7 - Launch a Terminal

Launch an interactive terminal for your Drupal container by running with `-it`:

`docker run --name drupalit --link mysql:mysql -p 8000:80 -v $PWD:/var/www/html -it drupal:latest /bin/bash`

(Note: web server does not run during terminal session.)

### Container Diagnostics

- To view currently running containers, run `docker ps`.
- To stop a container, run `docker stop container_name_or_id`.
- To restart a container that's been stopped, run `docker start container_name_or_id`.
- To remove a container, run `docker rm container_name_or_id -f`
- To remove a container automatically, add `--rm` to the launch command

### Database Diagnostics

After launching the database container, you can run database commands:

- To see databases, run `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="show databases;"`
- To see tables, run `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="use drupal; show tables;"`
- To empty database, run `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="drop database drupal; create database drupal"`
- To run MySQL commands on your database, launch a terminal within a second container instance: `docker run -it --link mysql:mysql --rm mariadb mysql -hmysql -udrupal -p`

### Todos
- connecting with https
- installing Drush
