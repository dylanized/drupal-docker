Here are steps for running a Drupal development site by running separate Docker containers on Mac OS X.

### Step 1 - Install Docker

[Download Docker for Mac here](https://hub.docker.com/?overlay=onboarding)

### Step 2 - Launch the Database Container

Run this command to launch a MySQL database container:

`docker run -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=drupal8 -e MYSQL_USER=drupal8 -e MYSQL_PASSWORD=drupal8 -d --name mariadb mariadb`

Customize the `-e` environment variables as needed.

### Step 3 - Import your Database

If you are recreating an existing Drupal instance, import your database like this:

`*TODO*`

### Step 4 - Edit Database Settings

If you using an existing Drupal codebase, edit the Drupal config file at `sites/default/settings.php` to match your database credentials from Step 1.

To install a fresh instance of Drupal from your local code, delete `settings.php`. During the install process, be sure to set the database host to `mysql`.

### Step 5 - Launch the Drupal Container

Run this command to launch a container that runs an Apache web server & PHP, and serves your current local folder on port 80:

`docker run --name drupal8 --link mariadb:mysql -p 8000:80 -v $PWD:/var/www/html -d drupal:latest`

`$PWD` can also be an absolute path to the host folder, i.e. `/host/path`. You may need to add the folder to the File Sharing list in Docker Desktop's preferences.

Replace `8000` with desired port.

### Step 5 (Alternate) - Launch a Fresh Drupal Container

To launch an untouched version of Drupal for debugging purposes, omit the `-v` volume sharing:

`docker run --name drupal8 --link mariadb:mysql -p 8000:80 -d drupal:latest`

During the install process, be sure to set the database host to `mysql`.

Replace `drupal:latest` with the desired [Drupal version](https://hub.docker.com/_/drupal?tab=tags).

### Step 6 - View the Drupal Site

You should now be able to view your site in the browser at http://localhost

### Step 7 - Launch a Terminal

Launch an interactive terminal for your Drupal container by running with `-it`:

`docker run --name drupal8it --link mariadb:mysql -p 8000:80 -v $PWD:/var/www/html -it drupal:latest /bin/bash`

(Note: web server does not run during terminal session.)

### Container Diagnostics

- To view currently running containers, run `docker ps`.
- To stop a container, run `docker stop container_name_or_id`.
- To restart a container that's been stopped, run `docker start container_name_or_id`.
- To remove a container, run `docker rm container_name_or_id -f`
- To remove a container automatically, add `--rm` to the launch command

### Database Diagnostics

After launching the database container, you can run database commands:

- To see databases, run `docker exec mariadb mysql --user="drupal8" --password="drupal8" --database="drupal8" --execute="show databases;"`
- To see tables, run `docker exec mariadb mysql --user="drupal8" --password="drupal8" --database="drupal8" --execute="use drupal8; show tables;"`

### Todos
- run import
- compose import
- connecting with https
- installing Drush
