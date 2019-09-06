## drupal-docker

This repo contains documentation and example tooling for running Drupal with Docker on OS X.

### Files

  - `docker-compose.yaml` - sample Docker Compose config file
  - `COMPOSE.md` - instructions for running with Docker Compose
  - `RUN.md` - instructions for running with barebones Docker Run commands
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
