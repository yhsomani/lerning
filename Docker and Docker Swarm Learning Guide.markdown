# Step-by-Step Guide to Learning Docker and Docker Swarm

## **1. Understanding Docker**
Docker is a platform for containerizing applications, enabling developers to build, share, and run applications in isolated environments called containers. Containers are lightweight, portable, and include only the necessary components to run an application, unlike virtual machines that require a full OS.

- **Benefits of Docker**:
  - **Consistency**: Applications run identically across development, testing, and production.
  - **Portability**: Containers work on any system with Docker installed.
  - **Efficiency**: Containers share the host OS kernel, using fewer resources.
  - **Isolation**: Each container runs independently, preventing conflicts.

## **2. Installing Docker**
To use Docker and Docker Swarm, install Docker on your system. Docker Desktop is the easiest option for most users, while Docker Engine is suitable for Linux servers.

- **Docker Desktop**:
  - Supports Windows, macOS, and Linux.
  - Includes Docker Engine, Docker CLI, Docker Compose, and Swarm.
  - Download from [Docker Desktop Installation](https://docs.docker.com/desktop/install/).
  - Follow the setup wizard and verify with `docker --version`.

- **Docker Engine (Linux)**:
  - Lightweight option for servers.
  - For Ubuntu, follow [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/):
    1. Update packages: `sudo apt-get update`.
    2. Install dependencies: `sudo apt-get install apt-transport-https ca-certificates curl gnupg`.
    3. Add Docker’s GPG key and repository.
    4. Install: `sudo apt-get install docker-ce docker-ce-cli containerd.io`.
  - Verify: `docker --version`.

- **Post-Installation**:
  - On Linux, add your user to the `docker` group: `sudo usermod -aG docker $USER`.
  - Test with a sample container: `docker run hello-world`.

## **3. Docker Generic Commands**
Docker provides commands to manage objects like images, containers, and volumes. These commands follow a consistent pattern.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker <object> ls` | Lists all objects of a type. | `docker container ls` |
| `docker <object> inspect <name or id>` | Shows detailed information about an object. | `docker image inspect nginx` |
| `docker <object> rm <name or id>` | Deletes an object. | `docker volume rm my-volume` |
| `docker <object> prune` | Removes unused objects. | `docker container prune` |

## **4. Managing Docker Images**
Images are read-only templates used to create containers. They are stored in registries like [Docker Hub](https://hub.docker.com/), which offers public and private repositories.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker image ls` | Lists local images. | `docker image ls` |
| `docker image pull <image>` | Downloads an image from a registry. | `docker image pull hello-world` |
| `docker image inspect <image>` | Displays image details. | `docker image inspect hello-world` |
| `docker image rm <image>` | Deletes an image. | `docker image rm hello-world` |
| `docker image prune` | Removes unused images. | `docker image prune` |

- **Notes**:
  - Use tags to specify versions (e.g., `nginx:latest`).
  - Images can be public (e.g., `nginx`) or private (hosted by organizations).

## **5. Working with Docker Containers**
Containers are running instances of images. They are ephemeral by default, meaning data is lost when they stop unless persisted.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker container ls` | Lists running containers. | `docker container ls` |
| `docker container ls -a` | Lists all containers (running or stopped). | `docker container ls -a` |
| `docker container create <image>` | Creates a container. | `docker container create hello-world` |
| `docker container start <name or id>` | Starts a container. | `docker container start my-container` |
| `docker container stop <name or id>` | Stops a container. | `docker container stop my-container` |
| `docker container logs <name or id>` | Views container logs. | `docker container logs my-container` |
| `docker container inspect <name or id>` | Shows container details. | `docker container inspect my-container` |
| `docker container rm <name or id>` | Deletes a container. | `docker container rm my-container` |
| `docker container rm -f <name or id>` | Force-deletes a running container. | `docker container rm -f my-container` |
| `docker container prune` | Removes stopped containers. | `docker container prune` |

- **Running Containers**:
  - Run in foreground: `docker container run httpd`.
  - Run in background: `docker container run -d httpd`.
  - Interactive mode with terminal: `docker container run -it httpd bash`.
  - Name a container: `docker container run --name myhttpd httpd`.
  - Map ports: `docker container run -p 8080:80 httpd`.
  - Set environment variables: `docker container run -e MYSQL_ROOT_PASSWORD=root mysql`.
  - Mount volumes: `docker container run -v mysql-volume:/var/lib/mysql mysql`.
  - Example: Run a MySQL container: `docker container run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -v mysql-volume:/var/lib/mysql mysql`.

- **Executing Commands**:
  - Run a command: `docker container exec myhttpd date`.
  - Access a shell: `docker container exec -it myhttpd bash`.

## **6. Building Custom Images**
Custom images are created using a `Dockerfile`, a script that defines the image’s contents.

- **Dockerfile Instructions**:
  - `FROM`: Base image (e.g., `FROM ubuntu:20.04`).
  - `COPY`: Copies files to the image (e.g., `COPY . /app`).
  - `EXPOSE`: Declares exposed ports (e.g., `EXPOSE 80`).
  - `RUN`: Runs commands during build (e.g., `RUN apt-get install python3`).
  - `CMD`: Specifies the default command (e.g., `CMD ["apache2", "-D", "FOREGROUND"]`).
  - `WORKDIR`: Sets the working directory (e.g., `WORKDIR /app`).
  - `ENV`: Sets environment variables (e.g., `ENV PORT=80`).

- **Example Dockerfile**:
  ```dockerfile
  FROM httpd:latest
  COPY ./website /usr/local/apache2/htdocs/
  EXPOSE 80
  CMD ["httpd-foreground"]
  ```

- **Building and Sharing**:
  - Build: `docker image build -t mywebsite .`.
  - Tag for Docker Hub: `docker image tag mywebsite myusername/mywebsite`.
  - Log in: `docker login`.
  - Push: `docker image push myusername/mywebsite`.

## **7. Managing Docker Volumes**
Volumes persist data outside containers, ensuring it survives container removal.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker volume ls` | Lists volumes. | `docker volume ls` |
| `docker volume create <name>` | Creates a volume. | `docker volume create mysql-volume` |
| `docker volume rm <name>` | Deletes a volume. | `docker volume rm mysql-volume` |
| `docker volume prune` | Removes unused volumes. | `docker volume prune` |

- **Usage**:
  - Mount a volume: `docker container run -v mysql-volume:/var/lib/mysql mysql`.

## **8. Introduction to Docker Swarm**
Docker Swarm turns multiple Docker hosts into a single cluster, enabling scalable and resilient services.

- **Key Concepts**:
  - **Swarm**: A cluster of Docker nodes.
  - **Nodes**: Hosts in the Swarm (managers or workers).
  - **Services**: Tasks defining how containers are deployed (e.g., run 5 replicas of an `httpd` container).

## **9. Managing a Docker Swarm**
Set up and manage a Swarm to orchestrate services across multiple nodes.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker system info | grep Swarm` | Checks if Swarm is active. | `docker system info | grep Swarm` |
| `docker swarm init` | Initializes a Swarm. | `docker swarm init` |
| `docker swarm join-token worker` | Generates a token for workers to join. | `docker swarm join-token worker` |
| `docker swarm join-token manager` | Generates a token for managers to join. | `docker swarm join-token manager` |
| `docker swarm leave --force` | Stops the Swarm (run on leader). | `docker swarm leave --force` |

- **Monitoring**:
  - Run commands periodically: `watch -n 1 docker container ls`.

## **10. Managing Swarm Nodes**
Nodes are the machines in a Swarm, either managers (control the Swarm) or workers (run tasks).

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker node ls` | Lists nodes in the Swarm. | `docker node ls` |
| `docker node inspect <node id>` | Shows node details. | `docker node inspect node-123` |
| `docker node rm <node id>` | Removes a node. | `docker node rm node-123` |
| `docker node promote <node id>` | Promotes a worker to manager. | `docker node promote worker-123` |
| `docker node demote <node id>` | Demotes a manager to worker. | `docker node demote manager-123` |

## **11. Managing Swarm Services**
Services define how containers are deployed across the Swarm, including replicas and port mappings.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker service ls` | Lists services. | `docker service ls` |
| `docker service create` | Creates a service. | `docker service create --name httpd -p 9090:80 --replicas 5 httpd` |
| `docker service inspect <name>` | Shows service details. | `docker service inspect httpd` |
| `docker service ps <name>` | Lists containers in a service. | `docker service ps httpd` |
| `docker service scale <name>=<count>` | Scales a service. | `docker service scale httpd=5` |
| `docker service rm <name>` | Deletes a service. | `docker service rm httpd` |

- **Example**:
  - Deploy a web server: `docker service create --name httpd -p 9090:80 --replicas 5 httpd`.

## **12. Additional Resources**
- [Docker Documentation](https://docs.docker.com/): Official guides and references.
- [Docker Hub](https://hub.docker.com/): Explore images and repositories.
- [Docker Swarm Documentation](https://docs.docker.com/engine/swarm/): Advanced orchestration details.
- [Docker Get Started](https://www.docker.com/get-started/): Beginner tutorials.