Docker was not the inventor of containers, but it made them easier to use with the three steps to creating and running them:

1.  Images: It aids you in packaging an application (with all its dependencies).
2.  Registries: It helps to distribute that app around to all the places you need to run it.
3.  Containers: It runs that app in a highly reproducible way.
________________

Checks the installed Docker version on your system.
- docker version

Provides detailed information about your Docker installation, such as number of containers and images.
- docker info

_______________

Runs a Docker container using the default image settings.
- docker container run

Runs the Nginx container and maps port 80 on the host to port 80 on the container, allowing access to the web server.
- docker container run --publish 80:80 nginx

Runs the Nginx container in detached mode (background) with port 80 mapped, so you can continue using the terminal.
- docker container run --publish 80:80 --detach nginx

A shorthand command for running the Nginx container in detached mode.
- docker container run -d nginx

Runs the Nginx container in detached mode with a custom name "webhost" and maps port 80 from the host to port 80 on the container.
- docker container run --publish 80:80 --detach --name webhost nginx

Runs a MySQL container in detached mode, mapping port 3306, and generating a random root password.
- docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql

_______________

Starts a previously stopped container named "mongo".
- docker start mongo

Stops the running container with ID "690".
- docker container stop 690

Lists all currently running containers.
- docker container ls

Lists all containers, both running and stopped.
- docker container ls -a

Displays the logs for the container named "webhost".
- docker container logs webhost

Shows the running processes inside the "webhost" container.
- docker container top webhost

Removes the containers with IDs "63f", "690", and "ode".
- docker container rm 63f 690 ode

Forcefully removes the container with ID "63f".
- docker container rm -f 63f

Shows detailed information about the container named "mysql".
- docker container inspect mysql

Displays live performance statistics for running containers.
- docker container stats
