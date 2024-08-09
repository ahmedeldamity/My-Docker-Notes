🐳 `What is Docker?`

*Docker was not the inventor of containers, but it made them easier to use with the three steps to creating and running them:*

1.  Images: It aids you in packaging an application (with all its dependencies).
2.  Registries: It helps to distribute that app around to all the places you need to run it.
3.  Containers: It runs that app in a highly reproducible way.
________________

🐳 `Docker Version and Info`

*Checks the installed Docker version on your system*
```bash
docker version
```
*Provides detailed information about your Docker installation, such as number of containers and images*
```bash
docker info
```
_______________

🐳 `Running Containers`

*Runs a Docker container using the default image settings*
```bash
docker container run
```
*Runs the Nginx container and maps port 80 on the host to port 80 on the container, allowing access to the web server*
```bash
docker container run --publish 80:80 nginx
```
*Runs the Nginx container in detached mode (background) with port 80 mapped, so you can continue using the terminal*
```bash
docker container run --publish 80:80 --detach nginx
```
*A shorthand command for running the Nginx container in detached mode*
```bash
docker container run -d nginx
```
*Runs the Nginx container in detached mode with a custom name "webhost" and maps port 80 from the host to port 80 on the container*
```bash
docker container run --publish 80:80 --detach --name webhost nginx
```
*Runs a MySQL container in detached mode, mapping port 3306, and generating a random root password*
```bash
docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
```
_______________

🐳 `Managing Containers`

*Starts a previously stopped container named "mongo"*
```bash
docker start mongo
```
*Stops the running container with ID "690"*
```bash
docker container stop 690
```
*Lists all currently running containers*
```bash
docker container ls
```
*Lists all containers, both running and stopped*
```bash
docker container ls -a
```
*Displays the logs for the container named "webhost"*
```bash
docker container logs webhost
```
*Shows the running processes inside the "webhost" container*
```bash
docker container top webhost
```
*Removes the containers with IDs "63f", "690", and "ode"*
```bash
docker container rm 63f 690 ode
```
*Forcefully removes the container with ID "63f"*
```bash
docker container rm -f 63f
```
*Shows detailed information about the container named "mysql"*
```bash
docker container inspect mysql
```
*Displays live performance statistics for running containers*
```bash
docker container stats
```
____________

🐳 `Interactive Containers`

*Runs the Nginx container named "proxy" interactively, opening a bash shell*
```bash
docker container run -it --name proxy nginx bash
```
*Runs an Ubuntu container named "ubuntu" interactively, opening a bash shell*
```bash
docker container run -it --name ubuntu ubuntu
```
*Starts the "ubuntu" container and attaches the terminal interactively*
```bash
docker container start -ai ubuntu
```
*Executes an interactive bash shell inside the running "mysql" container*
```bash
docker container exec -it mysql bash
```
_____________

🔍 `Difference Between docker run and docker exec:`

*Starts a new container from an image*
```bash
docker run
```
*Runs commands inside an existing, running container*
```bash
docker exec
```
_____________

🔍 `What is a Virtual Network?`

*This is like the internal phone system in the building. It allows the offices (containers) to call each other without using the outside phone lines (the internet). This phone system is only available inside the building, so only the offices can use it.*

🔍 `Why is This Useful??`

- Private Communication: Just like offices can talk to each other privately over the internal phone system, containers can communicate securely over the virtual network without exposing their data to the outside world.

- Controlled Access: You can decide which offices can talk to each other. For example, you might only let the HR office talk to the finance office. Similarly, in Docker, you control which containers can communicate with each other.

- Security: The internal phone system is separate from the outside world, so no one from outside the building can listen in. In Docker, the virtual network is isolated, meaning outsiders can’t easily access it unless you explicitly allow it.









