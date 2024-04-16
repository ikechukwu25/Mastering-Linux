Docker is a platform for developing, deploying, and running applications in containers. Containers allow a developer to package an application with all the parts it needs, such as libraries and other dependencies, and ship it all out as one package.

A container is a running process that encapsulates everything an application needs to run (and only those things).
Docker makes it easy to install and run software without worrying about setup or dependencies. 

Docker containers are lightweight, self-contained units that encapsulate all the necessary components to run software, including code, runtime, libraries, and system tools. When you run a Docker container, you're essentially launching an isolated process on the host machine.

Virtual Machines and containers provide isolation for running applications, they differ in their architecture, resource overhead, portability, and performance characteristics. The choice between VMs and containers depends on factors such as application requirements, resource constraints, and deployment environments.


**DIFFERENCE BETWEEN A VIRTUAL MACHINE AND A CONTAINER** </br></br>
￼
<img width="944" alt="Pasted Graphic 1" src="https://github.com/ikechukwu25/Mastering-Linux/assets/64879420/06cf3a02-0b29-46b9-bc80-412893402dfa">

Containers and virtual machines (VMs) are both technologies that enable the isolation and execution of applications, but they operate at different levels of abstraction and have distinct characteristics.

- Abstraction Level:
  * Containers: Containers operate at the application level, encapsulating the application and its dependencies. They share the host OS kernel but have their own user space.
  * VMs: Virtual machines operate at the hardware level, providing a complete virtualized environment, including a guest OS, for each instance. Each VM has its own kernel.
- Resource Efficiency:
  * Containers: Containers are more lightweight and efficient in terms of resource usage. They share the host OS kernel, consuming fewer resources compared to VMs.
  * VMs: VMs are more resource-intensive as they require a full OS stack for each instance. VMs consume more memory and disk space.
- Startup Time:
  * Containers: Containers start quickly, often in seconds, as they don't need to boot an entire operating system.
  * VMs: VMs have a longer startup time, typically measured in minutes, as they need to boot a full OS.
 
**PRACTICAL EXAMPLE**

Containers offer a streamlined solution for managing complex software stacks, especially in scenarios like "the matrix hell," where setting up a full stack involves integrating various technologies like Node.js for web servers, MongoDB for databases, Ansible for automation, and others. These technologies often require specific versions of the operating system and compatibility with each other, posing compatibility challenges.

However, containers address these challenges by allowing each application to run in its own isolated environment. By sharing the same host kernel, containers ensure compatibility across different operating systems, eliminating concerns about OS versions. This approach simplifies deployment, as you only need Docker on the target system to run the containerized applications, regardless of the underlying OS.

**DOCKER IMAGES**

Docker images serve as the foundation for containers, offering a consistent and reproducible environment for application execution. They package everything needed for software operation, including code, dependencies, and even the operating system, into a single, distributable unit. Docker images simplify the process of building, sharing, and deploying applications across different environments.

Docker comprises two main editions: Docker Community Edition (CE) and Docker Enterprise Edition (EE). The Docker engine consists of three key components: the Docker Daemon (dockerd), the Docker CLI (Command Line Interface), and a REST API.

### INSTALLING DOCKER

Refer to [Docker's official documentation](https://docs.docker.com/engine/install/ubuntu/) for detailed instructions on installing Docker on Ubuntu. Below are the summarized steps:

\# Update package index </br>
`sudo apt update` </br></br>
\# Uninstall old versions (if any) </br>
`sudo apt remove docker docker.io containerd runc`</br></br>
\# Install required packages </br>
`sudo apt-get install ca-certificates curl gnupg` </br></br>
\# Add Docker’s official GPG signing key </br>
`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -` </br></br>
\# Adding the official docker repository </br>
`sudo echo \` </br>
`  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \`</br>
`  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \`</br>
`  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`</br></br>
\# refreshing the apt cache</br>
`sudo apt update`</br></br>
\# display the content of the file located at /etc/apt/sources.list.d/docker.list in a Linux system. </br>
`cat /etc/apt/sources.list.d/docker.list`</br></br>
\# selecting the docker repository as the default one</br>
`apt-cache policy docker-ce`</br></br>
\# installing docker</br>
`sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`</br></br>
\# checking its status</br>
`sudo systemctl status docker`</br></br>
\# Adding the current user to the docker group to be able to run the docker command</br>
`sudo usermod -aG docker ${USER}`</br>

`cat /etc/apt/sources.list.d/docker.list` - This command is used to display the content of the file located at /etc/apt/sources.list.d/docker.list in a Linux system. This file typically contains information about Docker repositories for the APT package manager.

Explore Docker Hub for pre-built images at [hub.docker.com](https://hub.docker.com/). You can also experiment with Docker using resources like [Play with Docker](https://labs.play-with-docker.com/).


### DOCKER CLIENT

The Docker client, also known as the Docker image and container CLI, interacts with the Docker daemon to manage Docker images and containers. To see information about your Docker installation, you can run docker info.

`docker container run hello-world`: This commandused to run a Docker container that executes the "Hello World" program. This is often used as a simple test to verify that Docker is installed and configured correctly on your system.

* 	Docker Image Pull: If the "hello-world" Docker image is not already available locally, the Docker engine will automatically pull it from the Docker Hub, which is the default registry for Docker images.
* 	Container Execution: Once the image is available, Docker will create and run a container based on that image. The container will execute a simple program that prints a "Hello from Docker!" message along with some information about the Docker installation.
* 	Output Display: The output of the container's execution will be displayed in your terminal. It should include the "Hello from Docker!" message, indicating that the container ran successfully.


### PULLING IMAGES AND RUNNING CONTAINERS

Docker images follow a naming convention of repository/imagename, where the repository or registry hostname precedes the image name. A repository refers to a collection of related Docker images, often organised around a specific application, service, or project.

Below are some important Docker commands:

`docker search mysql`: To search for an image, you can use the command.

`docker images`: This command is used to list Docker images on your local machine. The docker images command is used to list Docker images on your local machine. It provides information about the images, including their repository, tag, image ID, creation date, and size.
`docker image ls`: This command used to list Docker images on your local machine. This command is an alternative to the older docker images command.
N/B: Image tags convey useful information about a specific image version


`docker image pull redis:6.0.20`: The command is used to pull the specific version of the Redis image, tagged as 6.0.20, from a container registry.	
* docker: The Docker command-line tool.
* image: Subcommand for working with Docker images.
* pull: Action to download an image from a registry.
* redis: The name of the Docker image (in this case, the official Redis image).
* 6.0.20: The version or tag of the Redis image to pull.


`docker image pull redis:latest`: This is the same as `docker image pull redis` - This will  pull the latest version of the software.

`docker container run redis`: When you run this command, Docker will attempt to create and start a new container using the specified Redis image. If the image is not already present on your local machine, Docker will automatically pull it from the Docker Hub repository.

`docker container ls`: This command is used to list the currently running Docker containers on your system. This command is an alternative to the older docker ps command. Both commands provide information about active containers, including their container IDs, names, statuses, ports, and more.

Collectively, these commands below demonstrate different approaches to creating and starting Docker containers:

- These set of commands offers more explicit control over container creation and starting
  - `docker container create httpd`: Creates a Docker container based on the httpd image. However, it does not start the container immediately.
  - `docker container ls -a`: Lists all containers, including those that are created but not running. This command is used to check the status of the newly created httpd container.
  - `docker container start httpd`: Starts the httpd container that was previously created but not running.
  - `docker container ls -a`: Lists all containers again to confirm that the httpd container is now running.


- This second command is more concise and convenient.
  - `docker container run httpd`: On the other hand, this command combines both container creation and starting into a single step. It creates a new container based on the httpd image and starts it immediately.

The primary difference is in the number of commands used and the separation of container creation and starting. The first set of commands explicitly creates a container and starts it in separate steps, while the second combines both actions into a single docker container run command. The end result, in terms of a running container, is the same. The second set is often more concise and convenient for starting containers.

`docker container run -P nginx`: This command is used to run a Docker container with port mapping, allowing Docker to automatically assign available ports on the host machine to the exposed ports in the container.


### LAB: RUNNING A WEB SERVER IN A DOCKER CONTAINER

To start a web server in a Docker container, you can use the following command:

`docker container run -d -p 8080:80 --name mysite nginx`

- `-d` (detached mode): This option runs the container in the background, allowing you to continue using the terminal for other commands. Without this option, the container would run in the foreground, and you would see its output in the terminal.
- `-p` 8080:80
    * Host Port (8080): This is the port on the host machine that you want to use to access the service running inside the container. In this case, it's port 8080. You can choose any available port on your host machine.
    * Container Port (80): This is the port exposed by the application or service running inside the container. In this example, it's port 80, which is a common port for web servers. The application inside the container is configured to listen for incoming connections on port 80.
- `--name mysite`: Assigns the name "mysite" to the container for easy identification.
- `nginx`: Specifies the Docker image to use for creating the container. In this case, it's the official Nginx image.
Once the container is running, you can access the web server by navigating to http://localhost:8080 in your web browser.
In this command:


In Docker, the -p and -P options in the docker container run command are used to control the port mapping between the host machine and the container. However, they have different behaviors:
* -p (lowercase):
    * Format: `-p <host-port>:<container-port>`
    * Specifies a specific port mapping where you explicitly define the host and container ports.
    * Example: `-p 8080:80` maps port 8080 on the host to port 80 in the container.
* Eg. `docker container run -p 8080:80 nginx`  
* -P (uppercase):
    * Automatically maps all exposed ports in the container to random ports on the host machine.
    * It's a shorthand for publishing all ports, and it doesn't require you to specify port mappings.
* Eg. `docker container run -P nginx`: In this case, Docker will choose available ports on the host machine and map them to the exposed ports in the container.

A port is a communication endpoint in a computer's operating system that corresponds to a specific process or service. Ports play a crucial role in networking and containerization, allowing communication between different services or applications.

When you run a Docker container, the processes inside the container may expose specific ports to allow communication with the outside world. However, by default, these ports are not accessible from outside the container.

Docker provides the `-p` option to map or publish ports between the host machine and the container. The syntax is `-p <host-port>:<container-port>`

Let's say you have a web application that runs in a Docker container, and it exposes its service on port 80. If you want to run multiple instances of this web application on the same host machine, you need a way to ensure that each instance uses a unique port on the host for its web service.

This is where port mapping comes into play. By using the `-p` option in the docker container run command, you can map the container's port to a specific port on the host. 

For example:</br>
`docker container run -d -p 8081:80 webapp_instance_1`</br></br>
This command maps port 8081 on the host to port 80 in the webapp_instance_1 container. Now, you can access the web application from the host machine at http://localhost:8081.

If you want to run another instance of the web application, you can use a different host port:

For example:</br>
`docker container run -d -p 8082:80 webapp_instance_2` </br></br>
This maps port 8082 on the host to port 80 in the webapp_instance_2 container. Now, you can access the second instance at http://localhost:8082.

In summary, by using different host ports for each container instance, you can run multiple containers that expose services on the same port (in this case, port 80) without conflicts. Each container instance effectively "listens" on a unique port on the host machine, allowing you to run multiple instances of the same service concurrently.

`docker container ls -a` or `docker ps -a`: These commands are equivalent and can be used interchangeably. Both commands provide a list of all containers on your system, including both running and stopped containers.

`docker container ls -a -f status=exited -q`: This command is used to list the IDs of all exited or stopped containers. 
* `docker`: Indicates that you're using the Docker CLI.
* `container ls`: Lists containers.
* `-a`: Shows all containers, including those that are currently running or have exited.
* `-f status=exited`: Filters containers based on their status, specifically targeting containers that have exited.
* `-q`: Displays only the container IDs.


