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

Explore Docker Hub for pre-built images at [hub.docker.com](https://hub.docker.com/). You can also experiment with Docker using resources like [Play with Docker](https://labs.play-with-docker.com/). </br></br>


**IMPORTANT NOTES:**

When building or running Docker containers, they often need to install packages or dependencies from the configured package repositories. If the Docker host or container network has connectivity issues, or if there are misconfigured repository URLs inside the Docker image, you may encounter errors similar to the one mentioned.

In case of an error like the below; </br>
Failed to set locale, defaulting to C.UTF-8  </br>
CentOS Linux 8 - AppStream 863 B/s | 38 B 00:00 </br>
Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist

- Run the following command to comment out the mirrorlist entries in the repository configuration files; 
 - `sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*`
- Replace the mirror base URLs with an alternative source by executing the following command:
 - `sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*`
- After making these changes, proceed to update your packages using the following command:
 - `sudo yum update -y`


### DOCKER CLIENT

The Docker client, also known as the Docker image and container CLI, interacts with the Docker daemon to manage Docker images and containers. To see information about your Docker installation, you can run docker info.

`docker container run hello-world`: This command is used to run a Docker container that executes the "Hello World" program. This is often used as a simple test to verify that Docker is installed and configured correctly on your system.

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

- This set of commands offers more explicit control over container creation and starting
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


### REMOVING IMAGES AND CONTAINERS

To remove a container, you must first stop it and then remove it using the following commands:

`docker container stop CONTAINERID`: to stop the container</br>
`docker container rm CONTAINERID`: to remove the container. </br></br>

OR </br></br>

`docker container rm -f CONTAINERID`: To remove the container forcefully without stopping it.  </br></br>

To remove all the stopped out exited containers, use the command substitution below;</br></br>

`docker container rm $(docker container ls -a -f status=exited -q)`</br></br>

To remove an image, follow these steps:</br></br>

`docker container stop CONTAINERID`: To stop the container if it’s still running. </br>
`docker container rm CONTAINERID`: To remove the container. </br>
`docker image rm IMAGENAME`: To remove the image </br></br>

OR </br></br>

`docker image rm -f IMAGENAME`: To remove the container forcefully without stopping it.  </br></br>

In Docker, "dangling images" refer to images that are not associated with any containers. These images have been created at some point but are not currently being used by any active containers.

`docker image ls -f "dangling=true"`: This command lists Dangling Images.</br>
`docker image prune`: This command is used to remove Dangling Images.</br>
`docker system prune`: Used to clean up the Docker system by removing unused data, including stopped containers, dangling images, and more.</br>
`docker system prune -a`: It’s a powerful Docker command used to free up disk space by removing unused resources.


### GETTING SHELL ACCESS TO A CONTAINER

`docker container run --name=mywebsite -it centos`: This command is used to run a Docker container based on the CentOS image with the specified name "mywebsite" in interactive mode.
 * `docker`: Indicates that you're using the Docker CLI.
 * `container run`: Instructs Docker to run a new container.
 * `--name mywebsite`: Specifies the name "mywebsite" for the container. This provides a human-readable identifier for the running container.
 * `-it`: Combines two options:
 * `-i` (or --interactive): Keeps STDIN open even if not attached, allowing you to interact with the container.
 * `-t` (or --tty): Allocates a pseudo-TTY, which is a terminal emulation. tty = teletypewriter. 
 * `centos`: Specifies the Docker image to use for creating the container. In this case, it's the CentOS base image.

`-it` option: Sets up an interactive terminal within the container, allowing you to interact with the command line.

**Exiting Without Stopping:**

To detach from a running container without stopping it, press `Ctrl + P + Q`. This action allows the container to continue running in the background while you return to your host terminal.

**Exiting Container's Terminal:**

To exit from a container's terminal session, simply type `exit`. This terminates the interactive session within the container without stopping it.

**Executing an Interactive Shell:**

Use the following command to execute an interactive shell (bash) within a running Docker container:
`docker container exec -it 996cc6b47081 bash`: This command is used to execute an interactive shell (bash) within a running Docker container. Note that the ID is the <container_id>. 

- `docker container ls -a`: If a container is listed in the output of this command, indicating that it's not exited or stopped, you can use the following command to return to its pseudo terminal.

Below is a summarized workflow for managing Docker containers:
***********************************
`docker container run debian`: Start a Debian container </br>
`docker container ls -a`: List all containers </br>
`docker container run -it debian`: Run a Debian container interactively </br>
`exit`: Exit the container </br>
`docker container start CONTAINERID`: Start a specific container </br>
`docker container exec -it CONTAINERID bash`: Execute an interactive bash shell within the container </br>
`Ctrl + P+ Q`: Use this shortcut to exit from a running container without stopping it. </br>

### GETTING INFORMATION ABOUT THE RUNNING CONTAINERS

Here`s how to get information about running containers, these commands provide valuable insights into the status and performance of your Docker containers: 

`docker container logs -f mycontainer`: To view the logs of a Docker container named "mysite,"  and If you want to follow the logs in real-time, similar to using tail -f, you can add the -f option
`docker container top mycontainer`: Used to display the running processes of a container.
`docker container stats mycontainer`:  Used to display a live stream of container resource usage statistics, including CPU usage, memory usage, network I/O, and block I/O. This command continuously updates in real-time.
`docker container inspect CONTAINERID`: Used to obtain detailed information about a specific Docker container.



### COMMITTING CONTAINER CHANGES INTO A NEW IMAGE

The below commands shows how to modify a container and save the changes into a new docker image. 

- Start the container, make the changes and exit the container where the changes were made and run the commit command as seen below; 
 - `docker container run --name=container1 -it centos`: run a Docker container based on the CentOS image with the specified name "mywebsite" in interactive mode.
 - `yum install nmap` - install the nmap in the new container
 - `exit` - stop and exit the container
- Run the commit command:
 - `docker commit -m "nmap installed" -a "Ikechukwu O" c7edc ikechukwu11/my_centos:latest`
  * `-m "nmap installed"`: This flag is used to add a commit message. In your case, it indicates that you installed nmap in the container.
  * `-a "Ikechukwu O"`: This flag sets the author or maintainer of the image. It's associated with your name in this case.
  * `c7edc`: This is the container ID or name of the container you want to commit.
  * `ikechukwu/my_centos:latest`: This is the name and tag you're giving to the new image. It follows the format `[username/organization]/[image_name]:[tag]`. In this case, it's `ikechukwu/my_centos:latest`.

After running this command, you'll have a new Docker image named `ikechukwu/my_centos` with the latest tag. This image will represent the state of the container with the ID or name c7edc at the time you executed the docker commit command.
The docker commit command is used to create a new image from a container's changes. It essentially allows you to take a snapshot of the current state of a container and save it as a new Docker image.  

N/B: All images have a repository except the official ones which resides at the root of the Docker Hub


### TAGGING AND PUSHING CUSTOM IMAGES TO DOCKER HUB

To tag and push custom images to Docker Hub, follow these steps:

- Tag an existing image:
 - `docker image tag nginx ikechukwu11/nginx:custom` - Used to create a new tag for an existing image.
  * `nginx`: This is the source image you are tagging. In this case, it's the official nginx image.
  * `ikechukwu11/nginx:custom`: This is the new tag you are giving to the image. It follows the format `[username/organization]/[image_name]:[tag]`. In this case, it's `ikechukwu11/nginx:custom`
- Tag an existing custom image with a new version:
 - `docker image tag ikechukwu11/my_centos:latest ikechukwu11/my_centos:1.0`: Used to create a new tag (1.0) for an existing  custom image.
- Log in to Docker Hub:
 - `docker login` - Used to log in to a Docker registry like Docker Hub. This is necessary before you can push Docker images to a registry or pull private images from it.
- Push the tagged images to Docker Hub:
 - `docker image push ikechukwu11/my_centos:latest`: Used to push a Docker image to a container registry, such as Docker Hub.

After running these commands, your custom images will be available on Docker Hub for others to use.



### IMAGE STRUCTURE AND LAYERS

An image consists of multiple layers. They are read-only and each of them has a unique ID. They are saved on disk only once and can be used by more be used by more than one image. 

Eg. A layer from the ubuntu image can be used by both Nginx and Apache images. This way both disk space and time will be saved when pulling the image. 

Each layer is only a set of differences from the layer before it. The layers are stacked on top of each other. 

When you run a container from an image, a new writable layer is added on top of the image layers. This writable layer is often called the container layer and allows you to make changes to the container since the lower layers in the image are read-only. 

All changes made to the running container are written to this thin writable container layer. When we remove a container, we remove this thin writable container layer. The other layers of the image remain untouched.

To write data in the writeable layer of the container, Docker uses something called storage drivers - eg auxiliary filesystem (aufs), overlay and overlay2. “overlay 2” is the default and the recommended one. 

`docker image inspect IMAGENAME`: To see the storage drivers being used and number of layers usually starting with the sha256. 

**CONTAINER SIZE**

`docker container run -d -P nginx`: Starting a 2 new containers with same image. </br>
`docker container ps -s`: Display the size of the running container. (SIZE is the amount of data on disk that is used for the writable layer of each container while VIRTUAL SIZE is the amount of data use for the read only image layers plus the container’s writeable layer size)  </br> </br>

| CONTAINER ID | IMAGE | COMMAND  | CREATED  | 	STATUS | PORTS 	|					NAMES   |	SIZE |
|---------------------|-----------------|--------------|-----------------|--------------|----------------|---------------------|--------------|
| 72e5c692c70c |  nginx   |  "/docker-entrypoint.\u2026" |  2 minutes ago  | Up 2 minutes |  0.0.0.0:32769->80/tcp, :::32769->80/tcp|   trusting_yalow |  1.09kB (virtual 187MB)|
| 8213704858da  | nginx  |  "/docker-entrypoint.\u2026" |  2 minutes ago |  Up 2 minutes |  0.0.0.0:32768->80/tcp, :::32768->80/tcp   | stoic_khayyam |   1.09kB (virtual 187MB) |

The key difference is that "size" is the actual disk space used by the image on the host system, while "virtual size" includes the theoretical disk space that would be used if all shared layers were counted independently.

Multiple container may share some or all read-only image data and two containers started from the same image like in the example above, share 100% of the read-only data. While 2 containers with different image that have layers in common share only those common layers.




### CREATING CUSTOM IMAGES USING DOCKERFILE

A Dockerfile is a script or configuration file used to build Docker images. It contains a set of instructions that are executed in order to create a Docker image. Dockerfiles are text files that contain instructions for building Docker images.

Each instruction in the Dockerfile adds a new layer to the image. Below are some instructions;

- FROM: Any docker file must begin with the From instruction. Specifies the base image to use for the build. The parent image from which you’re building . This is usually a Linux Distribution. 
- LABEL: This sets the maintainer. 
- ENV: Sets environment variables in the form key=value.
- RUN: Executes commands in a new layer on top of the current image.
- EXPOSE: Informs Docker that the container listens on the specified network ports at runtime.
- CMD: Provides defaults for an executing container. It provides a command that will be run every time you launch a new container from the stated image or every time you restart a stopped container. There can be only one CMD instruction in the docker file. 
- COPY: Copies files or directories from the host machine to the container's file system. Host machine ———> Container’s file system
- WORKDIR: The "working directory" is a directory inside the Docker container where the instructions such as RUN, CMD, ENTRYPOINT, COPY, and ADD will be executed or applied. The WORKDIR instruction is used to set this working directory. By default, the working directory is the root (/) of the file system inside the container.

In a Dockerfile, there are 3 copy instructions that copy 3 scripts that are needed to initialise the web server in a specific way. If you want a custom image, you’ll remove the copy instructions. 

Steps to download a docker file. 
* Visit Docker Hub:
    * Go to the Docker Hub website: https://hub.docker.com/
* Search for Image:
    * Use the search bar to find the Docker image you are interested in. For example, if you are looking for the official NGINX image, search for "nginx."
* Select Image:
    * Click on the relevant image from the search results to view its details.
* View Source Links:
    * Many projects on Docker Hub link to their source code repositories. Look for links to GitHub, GitLab, or other version control systems. These links may be available in the image description or metadata.
* Check GitHub Repository:
    * If a link to the source code repository is available, follow the link to the repository. Once there, you can explore the repository to find the Dockerfile.
* Navigate to the Dockerfile:
    * In the source code repository, the Dockerfile is usually located in the root directory or in a subdirectory named "docker" or similar. Look for files named "Dockerfile" or with a specific name indicating it's a Dockerfile.
* Read and Download:
    * Open the Dockerfile to view its content. You can read the instructions and understand how the image is built. If you want to use this Dockerfile, you can download it from the repository.
 
      
#### CUSTOMIZING AN IMAGE VIA DOCKERFILE; 

In the context of the NGINX web server, the directory /usr/share/nginx/html is the default location where NGINX serves its static web content. This directory typically contains the HTML, CSS, JavaScript, and other static files that make up a website.

- WORKDIR /usr/share/nginx/html 
- COPY page.html index.html: copies the file (page.html) in the current working directory on docker host to  the container’s working directory which had been altered to /usr/share/nginx/html above. 
- Create the file on the host system: `echo “This is the file” > page.html`
- `docker image build -t mynginx`: This will build a Docker image with the tag "mynginx" using the Dockerfile and context in the current directory. This assumes that the Dockerfile is named "Dockerfile" and is present in the current directory.
- `docker image ls`: This will list the docker images in the host system. 
- `docker container run -d -P mynginx:1.0`: To start running a container
- `Ip a`: Obtain the host device’s IP address
- Visit web browser and input IP address:port to open the page. 


### PERSISTENT DATA: VOLUMES

Persistent data is data that survives the lifecycle of individual containers. It is retained even when a container is stopped, removed, or replaced by a new instance.

Docker has two options for the container to store files in the host machine so that the files are persistent even after the container stops - **Volumes and Bind Mounts.** 

In Docker, volumes and bind mounts are both mechanisms to manage persistent data and share files between the host machine and containers.
Volumes are the best way manage to persistent data in Docker. 

Instance where a persistent data is needed: If you upload some pictures, you'd want them to stay in the app even if you stop or restart the container. That's where we use things like "volumes" or "bind mounts" to make sure the data persists, just like saving a file on your computer. 

In Docker, when you create a volume and mount it to a container, you are essentially creating a link between a directory on the host machine (where Docker manages the volume) and a directory inside the container.

Volumes:
* Definition:
    * A volume is a Docker-managed directory that exists outside the container file system.
    * Volumes are managed by Docker and can be easily shared between containers.
* Persistence:
    * Volumes persist even if the container that uses them stops or is removed.
    * Volumes are intended for storing data that should persist across container instances.
* Usage:
    * Volumes are often used for databases, configuration files, and any data that needs to be maintained independently of the container's lifecycle.
* Docker Commands:
    * Create a volume: `docker volume create myvolume`
    * List all volumes: `docker volume ls`
    * To inspect a volume: `docker volume inspect myvolume (You can view the mount point here)`
    * To remove a volume: `docker volume rm myvolume`
    * Mount a volume to a container: `docker run -v myvolume:/path/in/container myimage`
Bind Mounts:
* Definition:
    * A bind mount is a link between a directory on the host machine and a directory in the container.
    * The container has direct access to the host file system.
* Persistence:
    * Bind mounts depend on the existence of the source directory on the host.
    * Changes made in the container are reflected on the host, and vice versa.
* Usage:
    * Bind mounts are useful for development, as they provide direct access to the host file system. Changes in code can be reflected immediately in the container.
* Docker Commands:
    * Mount a bind mount to a container: `docker run -v /host/path:/path/in/container myimage`


    - `docker volume create myvolume`
    - `docker volume inspect myvolume`
    - `docker container run -d -p 80:80 --name=mywebapp -v myvolume:/usr/share/nginx/html nginx`
    - `sudo cp /etc/passwd  /var/lib/docker/volumes/myvolume/_data/index.html`
    - `ip a` 
    - Visit web browser and input IP address:port to open the page.
  
**SUMMARY**: The path /usr/share/nginx/html inside the NGINX container is connected to the myvolume volume on the host machine via `docker container run -d -p 80:80 --name=mywebapp -v myvolume:/usr/share/nginx/html nginx`, while that of apache2 is /usr/local/apache2/htdocs
The path /var/lib/docker/volumes/myvolume/index.html on the host machine represents the actual location where the contents of the myvolume volume are stored.
So, when you copy the /etc/passwd file to /var/lib/docker/volumes/myvolume/index.html, you are essentially placing the contents of /etc/passwd into the myvolume volume, and this data is then accessible to the NGINX container at /usr/share/nginx/html.


To check the IP address of the container and connect to it using SSH and the user you’ve just created. 

After opening the pseudo terminal of the container, run;
 
- Open the pseudo terminal of the container by executing: `docker exec -it containerID bash` 
- Start the SSH service inside the container: `service ssh start`
- Verify the status of the SSH service:: `service ssh status`
- Detach from the container terminal while leaving it running: `Ctrl + P + Q`
- Retrieve the IP address of the container: `docker container inspect containerID | grep -i ip - to get the IP address`
- Use ping to ensure connectivity to the container: `ping IP address`
- Connect to the container via SSH using the username and IP address: `ssh -l username ipaddress`
