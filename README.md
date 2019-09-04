Here are steps for running a Drupal development site using separate Docker containers on Mac OS X.

### Step 1 - Install Docker

[https://hub.docker.com/?overlay=onboarding](Download Docker for Mac here)

### Step 2 - Launch the Database Container

Run this command to launch a MySQL database container:

`docker run -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=drupal8 -e MYSQL_USER=drupal8 -e MYSQL_PASSWORD=drupal8 -v mariadb:/var/lib/mysql -d --name mariadb mariadb`

Customize the `-e` environment variables as needed.

### Step 3 - Edit Database Settings

To run an existing Drupal instance, edit the Drupal config file at `sites/default/settings.php` to match your database credentials from Step 1.

To install a fresh version of Drupal from your local code, delete `settings.php`.

### Step 4 - Launch the Drupal Container

Run this command to launch a container that runs an Apache web server & PHP, and serves your local codebase on port 80:

`docker run --name drupal8 --link mariadb:mysql -p 80:80 -d drupal:latest -v /local/path:/var/www/html/`

*NOT WORKING YET*

Change the local path as needed.

To launch an untouched version of Drupal for debugging purposes, omit the `-v` volume sharing:

`docker run --name drupal8 --link mariadb:mysql -p 80:80 -d drupal:latest`

### Step 5 - View the Drupal Site

You should now be able to view your site in the browser at http://localhost

### Step 6 - Launch a Terminal

Launch an interactive terminal for your container by running with `-it`:

`docker run --name drupal8it --link mariadb:mysql -p 80:80 -it drupal:latest /bin/bash`

### Diagnostics

To view currently running containers, run `docker ps`.

To stop a container, run `docker stop $container_name_or_id -f`.

To restart a container that's been stopped, run `docker start $container_name_or_id -f`.

To remove a container, run `docker rm $container_name_or_id`.

### Todos

- different drupal versions
- different ports
- connecting with https
- automating with docker compose
- installing Drush
