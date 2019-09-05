Here are steps for running a Drupal development site using Docker Compose on Mac OS X.

### Step 1 - Install Docker

[Download Docker for Mac here](https://hub.docker.com/?overlay=onboarding)

### Step 2 - Launch the Containers

In the included `docker-compose.yaml` config file, a database container and a web server container are defined.

Launch the containers from the codebase folder with this command:

`docker-compose up`

### Step 3 - View the Drupal Site

You should now be able to view your site in the browser at http://localhost

### Step 4 - Restart the Containers

Exit the Docker Compose session with `CMD-C`.

You can then restart the containers with `docker-compose start`, and stop them with `docker-compose stop`.

Remove the containers with `docker-compose down`.
