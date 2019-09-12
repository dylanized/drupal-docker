## drupal-docker

This repo contains documentation and example tooling for running Drupal with Docker on OS X.

### Files & Folders

  - `docker-compose.yaml` - sample Docker Compose config file
  - `docker/drupal/Dockerfile` - Dockerfile for `drupal` container
  - `docker/init` - folder for MySQL auto-import
  - `package.json` - NPM scripts for managing Docker Compose and MySQL

  - `DOCKER-COMPOSE.md` - instructions for running with Docker Compose
  - `DOCKER-RUN.md` - instructions for running with barebones Docker Run commands

### NPM Scripts

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

### Connect to Database

To connect to the database via SQL Pro (or other app), create a new connection with these values:

  - host: 127.0.0.1
  - username: `drupal`
  - password: `drupal`
  - database: `drupal`
  - port: 33060
