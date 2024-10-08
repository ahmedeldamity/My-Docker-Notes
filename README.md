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

🔍 `Why is This Useful?`

- Private Communication: Just like offices can talk to each other privately over the internal phone system, containers can communicate securely over the virtual network without exposing their data to the outside world.

- Controlled Access: You can decide which offices can talk to each other. For example, you might only let the HR office talk to the finance office. Similarly, in Docker, you control which containers can communicate with each other.

- Security: The internal phone system is separate from the outside world, so no one from outside the building can listen in. In Docker, the virtual network is isolated, meaning outsiders can’t easily access it unless you explicitly allow it.
______________

🔍 `What is NAT (Network Address Translation)?`

*Imagine the building has only one public address (like 123 Main St.) but many rooms inside it. When a room wants to send a letter outside the building, the main door (NAT) helps by marking the letter with the building’s public address.*

🔍 `How It Works?`

*Sending Messages Outside the Building:*

- If Room 101 wants to send a letter to someone outside the building (like a client or a website), it gives the letter to the main door.
The main door (NAT) puts a return address (the building’s public address) on the letter and sends it out.
When a reply comes back, the main door knows which room (container) the letter belongs to and delivers it accordingly.

*Security and Management:*

- The main door (NAT) also acts like a gatekeeper, managing which letters (packets) can leave or enter the building. This helps in controlling and securing access.

*Visual Summary:*

- Containers = Rooms in the building.
- NAT = Main door with a return address.
______________

🔍 `What is --net=host?`

*When you run a container with the --net=host option, it tells Docker to skip creating a separate network namespace for the container. Instead, the container will share the host's network stack, meaning it will use the host's IP address and network interfaces directly. This can result in improved network performance but can also expose the host to security risks since the container has direct access to the host's network.*

🔍 `Two Scenarios:`

*Without `--net=host`:*

- The guest house (container) has its own separate address.
- If you want to talk from the guest house to the main house, you have to use the phone line (network communication).

*With `--net=host`:*

- The guest house doesn’t have its own separate address anymore.
- Instead, it shares the main house’s address. It's like the guest house is gone, and the people (programs) in the guest house move directly into the main house.
- Now, these programs don’t need to use the phone line (network connection) to talk; they can just walk into any room in the main house because they’re already inside.

________________

🔍 `What is the Docker Network Drivers`

*Docker network drivers are mechanisms that allow Docker containers to communicate with each other and the outside world. When you create a Docker network, you choose a driver to define how the network operates and how the containers connected to it interact.*

🔍 `Built-In Docker Network Drivers`

*1- Bridge Network Driver (Default)*
-  Containers on the same bridge network can communicate with each other, but they're isolated from containers on different networks.

*2- Host Network Driver*
- When you use the host network driver, the container uses the Docker host’s network stack directly.
- The container uses the host’s IP address directly instead of using Docker's NAT.
- No network isolation; containers share the host's IP address and ports.
- Useful for scenarios where performance is critical and network isolation is not needed.

*3. Overlay Network Driver*
-  Used to connect containers across multiple Docker hosts (machines), typically in a Docker Swarm or Kubernetes cluster.
-  Allows containers on different hosts to communicate as if they were on the same network.
-  deal for distributed applications, microservices, and multi-host deployments.

*4. None Network Driver*
- it has no network interfaces.
- Completely isolates the container from any network.
- If you’re running a container that performs calculations and doesn’t need any network access, using the none driver ensures it’s fully isolated.

🔍 `3rd Party Docker Network Drivers`

*are additional tools created by other developers or companies to enhance Docker’s networking features. Docker itself comes with a few basic network drivers, but third-party drivers add more options for how containers can connect to each other and the outside world.*

*Examples of Third-Party Docker Network Drivers*

- Weave
- Calico
- Flannel
- Cilium

_____________________

🐳 `Docker Networks: CLI Management of Virtual Networks`

*Displays the port mappings between the host and the `webhost` container.*
```bash
docker container port webhost
```
*Retrieves the IP address of the `webhost` container.*
```bash
docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost
```
*Lists all Docker networks on the system.*
```bash
docker network ls
```
*Shows detailed information about the default `bridge` network.*
```bash
docker network inspect bridge
```
*Creates a new Docker network named `my_app_net`.*
```bash
docker network create my_app_net
```
*Runs a `new nginx` container named `new_nginx` on the `my_app_net` network in detached mode.*
```bash
docker container run -d --name new_nginx --network my_app_net nginx
```
*Provides detailed information about the `my_app_net` network.*
```bash
docker network inspect my_app_net
```
*Connects the `webhost` container to the `my_app_net` network.*
```bash
docker network connect my_app_net webhost
```
*Disconnects the `webhost` container to the `my_app_net` network.*
```bash
docker container disconnect my_app_net webhost
```
*Executes the `ping` command inside the `new_nginx` container to test network connectivity to a container named `my_nginx`.*
```bash
docker container exec -it new_nginx ping my_nginx
```

_____________________

🐳 `Docker Networks: DNS and How Containers Find Each Other`

*Creates a new Docker network named `dude`.*
```bash
docker network create dude
```
**NOW I Run Two Containers With The Same Alias Name And Will Explain How DNS Dealing With It.**

**The First:**

*Runs an `elasticsearch` container with the alias `search` on the `dude` network in detached mode.*
```bash
docker container run -d --net dude --net-alias search elasticsearch:2
```
**The Second:**

*Runs an `elasticsearch` container with the alias `search` on the `dude` network in detached mode.*
```bash
docker container run -d --net dude --net-alias search elasticsearch:2
```
**So When We Search on On Alias Name `Search` It Will Bting all Exist**

*Runs an `alpine` container to perform a DNS lookup for the alias `search` on the `dude` network, then removes the container after the command completes.*
```bash
docker container run --rm --net dude alpine nslookup search
```

**But It Exist Another Way (DNS Round-Robin)**

*DNS Round-Robin: This means that when you request search, Docker’s internal DNS service will resolve the alias to one of the IP addresses of the containers with that alias, essentially picking one of them randomly.*

*Runs a `centos` container to make a silent HTTP request to search:9200 on the `dude` network, then removes the container after the command completes.*
```bash
docker container run --rm --net dude centos curl -s search:9200
```

___________________________

🐳 `Image Layers:`

**Imagine building a sandwich 🥪. Each ingredient you add (like bread, lettuce, cheese, tomato) is like a layer in a Docker image.**

Layers in Docker: When you create a Docker image, each step in the recipe (like adding lettuce, then cheese) adds a new layer. For example:

- Step 1: You add a base (like bread).
- Step 2: You add cheese on top of the bread.
- Step 3: You add lettuce on top of the cheese.

These steps are like commands in a Dockerfile (FROM, RUN, COPY), and each creates a new layer. Each layer builds on the one below it.

Why layers Important: If you want to change the lettuce, you don’t need to rebuild the whole sandwich. You only change the lettuce layer. This makes updating images faster because Docker only rebuilds the layers that changed.

___________________________

🐳 `Union File System (UnionFS)`

**UnionFS is like a magic trick where all the sandwich layers (ingredients) look like one single sandwich when you eat it. Even though you added ingredients separately, UnionFS combines them so that you only see the final sandwich.**

How it works:

- The layers are stacked, but you interact with them as one single unit.
- When you create a container from an image, Docker uses UnionFS to combine all the image layers (the pre-made parts) with the new writable layer into a single, unified file system.
- Even though these layers are separate, UnionFS makes them look like one complete system, so when you interact with the container, you don't have to worry about the layers being separate.
- Read-Only Layers: The original image layers are read-only, meaning they can’t be changed. UnionFS keeps them as they are but makes sure they’re accessible as part of the container’s file system.
- Writable Layer: UnionFS adds a writable layer on top of the read-only layers. This is where any changes you make while the container is running (like installing new software or creating files) are stored.
- If you modify a file that exists in one of the read-only layers, UnionFS doesn’t actually change that original layer. Instead, it makes a copy of the file in the writable layer and then applies your changes there. This is called Copy-on-Write.
- This process ensures that the original image layers remain untouched, and only the changes you make are stored in the writable layer.

_______________________

🐳 `When you create, run and delete a Docker container`

**1. Container Creation:**

*Think of creating a container as making a sandwich from a recipe (Docker image) you already have.*

- Base Image Layers: Docker starts with the base image layers (the sandwich ingredients), which are read-only. This means you can look at and use these layers, but you can't change them. They're like the pre-made parts of the sandwich.
- New Writable Layer: On top of these read-only layers, Docker adds a new, writable layer (container layer). This layer is where all your changes go, like adding ketchup or mustard to your sandwich. If you make changes, they only affect this top layer, not the original ingredients.

**2. Running the Container:**

*When the container runs, it uses the combined layers as its file system:*

- Reading Files: If you read a file (like tasting the sandwich), Docker checks from the top layer down. If the file is in the writable layer, it uses that one. If not, it looks in the lower read-only layers.
- Writing Files: If you write or change a file (like adding or removing ingredients), it happens in the writable layer. The lower layers stay unchanged, which keeps the original image intact.

**3. Deleting the Container:**

- When you delete the container, Docker removes the writable layer. The base image layers remain untouched, so you can create a new container from the same image without losing anything.
