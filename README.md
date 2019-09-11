## drupal-docker

This repo contains documentation and example tooling for running Drupal with Docker on OS X.

### Files

  - `docker-compose.yaml` - sample Docker Compose config file
  - `DOCKER-COMPOSE.md` - instructions for running with Docker Compose
  - `DOCKER-RUN.md` - instructions for running with barebones Docker Run commands
  - `package.json` - NPM scripts for managing Docker Compose and MySQL

### NPM Scripts

Docker Scripts:

  - `docker:up` - launch Docker Compose containers
  - `docker:start` - restart containers
  - `docker:stop` - stop containers
  - `docker:down` - : remove containers
  - `docker:list` - : list containers

MySQL Scripts:

  - `mysql:dbs` - list mysql databases
  - `mysql:tables` - list drupal tables
  - `mysql:empty` - empty drupal database
  - `mysql:shell` - launch shell in MySQL container

To connect to the database via SQL Pro (or other app), create a new connection with these values:

  - host: 127.0.0.1
  - username: `drupal`
  - password: `drupal`
  - database: `drupal`
  - port: 33060
