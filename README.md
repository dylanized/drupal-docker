# Drupal Docker

This repo contains documentation and example tooling for running Drupal with Docker on OS X.

## Files & Folders

  - `docker-compose.yaml` - sample Docker Compose config file
  - `docker/drupal/Dockerfile` - Dockerfile for `drupal` container
  - `docker/init` - folder for MySQL auto-import
  - `package.json` - NPM scripts for managing Docker Compose and MySQL
  - `DOCKER-RUN.md` - instructions for running with barebones Docker Run commands

## Setup

Here are steps for running a Drupal development site using Docker Compose on Mac OS X. (To use `docker running` commands, see other file).

### Step 1 - Install Docker

[Download Docker for Mac here](https://hub.docker.com/?overlay=onboarding)

Start the Docker Desktop daemon before proceeding.

### Step 2 - Launch the Containers

In the included `docker-compose.yaml` config file, a `mysql` database container and a `drupal` web server container are defined. The drupal container is further configured in `/docker/drupal/Dockerfile`.

Navigate to the codebase folder and launch the app containers with `docker-compose up`.

The database will automatically import `.sql` files in your `/docker/init` folder.

### Step 3 - View the Drupal Site

You should now be able to view your site in the browser at http://localhost:8000

You can connect to the database at http://localhost:33060

### Step 4 - Stop and Restart the Containers

Exit the Docker Compose session with `CMD-C`.

You can then restart the containers with `docker-compose start`, and stop them with `docker-compose stop`.

Remove the containers with `docker-compose down`.

For more utilities see the included NPM Scripts.  

## NPM Scripts

Docker Run:

  - `docker:up` - launch Docker Compose containers
  - `docker:start` - restart app containers
  - `docker:stop` - stop app containers
  - `docker:down` - remove app containers
  - `docker:reload` - remove and launch app containers
  - `docker:kill` - stop and remove all containers

Docker Utils:

  - `docker:list` - list containers
  - `docker:logs` - display logs from app containers

Docker Images:

  - `docker:images` - list images
  - `docker:build` - regenerate custom images
  - `docker:rebuild` - remove all containers, build images and relaunch app containers
  - `docker:rmi` - remove all images

Drush Utils:

  - `drush:help` - show Drush commands
  - `drush:status` - show Drupal installation info
  - `drush:login` - generate one-time Drupal admin login URL
  - `drush:modules` - display info on Drupal modules

Bash Shell:

  - `shell:drupal` - bash shell for `drupal` container
  - `shell:mysql` - bash shell for `mysql` container

MySQL Utils:

  - `mysql:dbs` - list mysql databases
  - `mysql:tables` - list Drupal tables
  - `mysql:empty` - empty Drupal database
  - `mysql:shell` - launch MySQL shell

## Database Helpers

After launching the containers, you can run database commands:

- To see databases, run `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="show databases;"`
- To see tables: `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="use drupal; show tables;"`
- To empty database: `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="drop database drupal; create database drupal"`
- To run MySQL commands on your database, launch a terminal within a second container instance: `docker run -it --network drupal --rm mariadb mysql -hmysql -udrupal -p`


## Connect to Database

To connect to the database via SQL Pro (or other app), create a new connection with these values:

  - host: 127.0.0.1
  - username: `drupal`
  - password: `drupal`
  - database: `drupal`
  - port: 33060
