Here are steps for running a Drupal development site using Docker Compose on Mac OS X.

### Step 1 - Install Docker

[Download Docker for Mac here](https://hub.docker.com/?overlay=onboarding)

### Step 2 - Launch the Containers

In the included `docker-compose.yaml` config file, a database container and a web server container are defined.

Navigate to the codebase folder and launch these containers with `docker-compose up`.

The database will automatically import `.sql` files in your `/data` subdirectory.

### Step 3 - View the Drupal Site

You should now be able to view your site in the browser at http://localhost:8000

You can connect to the database at http://localhost:33060

### Step 4 - Stop and Restart the Containers

Exit the Docker Compose session with `CMD-C`.

You can then restart the containers with `docker-compose start`, and stop them with `docker-compose stop`.

Remove the containers with `docker-compose down`.

### Database Helpers

After launching the containers, you can run database commands:

- To see databases, run `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="show databases;"`
- To see tables: `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="use drupal; show tables;"`
- To empty database: `docker exec mysql mysql --user="drupal" --password="drupal" --database="drupal" --execute="drop database drupal; create database drupal"`
- To run MySQL commands on your database, launch a terminal within a second container instance: `docker run -it --network drupal --rm mariadb mysql -hmysql -udrupal -p`
