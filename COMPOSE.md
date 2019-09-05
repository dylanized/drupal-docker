Here are steps for running a Drupal development site using separate Docker Compose on Mac OS X.

### Step 1 - Install Docker

[Download Docker for Mac here](https://hub.docker.com/?overlay=onboarding)

### Step 2 - Launch the Containers

In the Docker Compose file there is are database and web server containers defined.

Launch the containers with this command:

`docker-compose up`

### Step 3 - View the Drupal Site

You should now be able to view your site in the browser at http://localhost

### Step 4 - Relaunch the Containers

Exit the Docker Compose session with `CMD-C`.

You can then relaunch the containers with `docker-compose start`.

Remove the containers with `docker-compose down`.
