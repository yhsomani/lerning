# Step-by-Step Guide to Learning Docker

## **1. What is Docker?**
Docker is a platform that enables developers to build, ship, and run applications inside containers. Containers are lightweight, standalone packages that include an application’s code, runtime, system tools, libraries, and settings. Unlike virtual machines, containers share the host system’s operating system kernel, making them more efficient and portable.

- **Why Use Docker?**
  - **Consistency**: Ensures applications run the same way in development, testing, and production environments.
  - **Portability**: Containers can run on any system with Docker installed, regardless of the underlying OS.
  - **Efficiency**: Containers use fewer resources than virtual machines.
  - **Scalability**: Easily scale applications by running multiple containers.
  - **Isolation**: Containers are isolated from each other, reducing conflicts between applications.

Docker solves the “it works on my machine” problem by standardizing the application environment, making it a popular choice for developers and DevOps professionals.

## **2. Installing Docker**
Before using Docker, you need to install it on your system. Docker provides two main options: Docker Desktop (recommended for most users) and Docker Engine (for Linux users who prefer a lightweight setup).

- **Docker Desktop**
  - Available for Windows, macOS, and Linux.
  - Includes Docker Engine, Docker CLI, and Docker Compose.
  - Download and install from [Docker Desktop Installation](https://docs.docker.com/desktop/install/).
  - Follow the setup wizard to complete the installation.
  - Verify installation by running `docker --version` in a terminal.

- **Docker Engine on Linux**
  - Ideal for server environments or users who don’t need a graphical interface.
  - Instructions vary by Linux distribution. For Ubuntu, follow [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/).
  - General steps:
    1. Update the package index: `sudo apt-get update`.
    2. Install prerequisites: `sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release`.
    3. Add Docker’s GPG key and repository.
    4. Install Docker Engine: `sudo apt-get install docker-ce docker-ce-cli containerd.io`.
    5. Verify with `docker --version`.

- **Post-Installation**
  - On Linux, add your user to the `docker` group to run Docker without `sudo`: `sudo usermod -aG docker $USER`.
  - Test Docker by running a sample container: `docker run hello-world`.

## **3. Basic Docker Commands**
Docker uses a command-line interface (CLI) to manage its objects, such as images, containers, and volumes. Understanding these commands is essential for working with Docker.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker <object> ls` | Lists all objects of a specific type (e.g., images, containers). | `docker image ls` |
| `docker <object> inspect <name or id>` | Displays detailed information about an object. | `docker container inspect my-container` |
| `docker <object> rm <name or id>` | Removes an object. | `docker container rm my-container` |
| `docker <object> prune` | Removes all unused objects of a type. | `docker image prune` |

- **Additional Commands**:
  - Check Docker version: `docker --version`.
  - View system-wide information: `docker info`.
  - Get help: `docker --help`.

## **4. Working with Docker Images**
Docker images are read-only templates used to create containers. They are stored in registries, such as [Docker Hub](https://hub.docker.com/), which hosts both public and private images.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker image ls` | Lists all images on the system. | `docker image ls` |
| `docker image pull <image name>` | Downloads an image from a registry. | `docker image pull nginx:latest` |
| `docker image inspect <image name>` | Displays detailed image information. | `docker image inspect nginx` |
| `docker image rm <image name or id>` | Removes an image. | `docker image rm nginx` |
| `docker image prune` | Removes all unused images. | `docker image prune` |

- **Tips**:
  - Specify a tag when pulling images (e.g., `nginx:latest` for the latest version).
  - Use `docker image ls -a` to see all images, including intermediate ones.

## **5. Creating and Managing Containers**
Containers are running instances of images. They are ephemeral by default, meaning data is lost when they stop unless persisted.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker container ls` | Lists running containers. | `docker container ls` |
| `docker container ls -a` | Lists all containers (running and stopped). | `docker container ls -a` |
| `docker container create <image>` | Creates a container from an image. | `docker container create nginx` |
| `docker container start <name or id>` | Starts a stopped container. | `docker container start my-container` |
| `docker container stop <name or id>` | Stops a running container. | `docker container stop my-container` |
| `docker container exec <name or id> <command>` | Runs a command inside a container. | `docker container exec -it my-container bash` |
| `docker container rm <name or id>` | Removes a container. | `docker container rm my-container` |
| `docker container prune` | Removes all stopped containers. | `docker container prune` |

- **Running Containers**:
  - Run in detached mode: `docker container run -d nginx`.
  - Map ports: `docker container run -p 8080:80 nginx` (maps host port 8080 to container port 80).
  - Set environment variables: `docker container run -e MY_VAR=value nginx`.
  - Mount volumes: `docker container run -v my-volume:/app nginx`.
  - Force remove running containers: `docker container rm -f my-container`.

## **6. Building Custom Images with Dockerfiles**
Dockerfiles are scripts that define how to build custom images. They allow you to customize images for your applications.

- **Key Dockerfile Instructions**:
  - `FROM`: Specifies the base image (e.g., `FROM node:16`).
  - `COPY`: Copies files from the host to the image (e.g., `COPY . /app`).
  - `EXPOSE`: Declares ports the container will use (e.g., `EXPOSE 3000`).
  - `RUN`: Executes commands during the build (e.g., `RUN npm install`).
  - `CMD`: Specifies the default command to run when the container starts (e.g., `CMD ["node", "app.js"]`).
  - `WORKDIR`: Sets the working directory (e.g., `WORKDIR /app`).
  - `ENV`: Sets environment variables (e.g., `ENV PORT=3000`).

- **Example Dockerfile**:
  ```dockerfile
  FROM node:16
  WORKDIR /app
  COPY . .
  RUN npm install
  EXPOSE 3000
  CMD ["node", "app.js"]
  ```

- **Building and Managing Images**:
  - Build an image: `docker image build -t my-app .`.
  - Tag an image: `docker image tag my-app my-username/my-app:latest`.
  - Push to Docker Hub:
    1. Log in: `docker login`.
    2. Push: `docker image push my-username/my-app:latest`.

## **7. Managing Data with Volumes**
Volumes allow data to persist outside containers, ensuring it’s not lost when containers are removed.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `docker volume ls` | Lists all volumes. | `docker volume ls` |
| `docker volume create <name>` | Creates a volume. | `docker volume create my-data` |
| `docker volume rm <name>` | Removes a volume. | `docker volume rm my-data` |
| `docker volume prune` | Removes all unused volumes. | `docker volume prune` |

- **Using Volumes**:
  - Mount a volume: `docker container run -v my-data:/app/data my-app`.
  - Example: Persist database data in a volume for a MySQL container: `docker container run -v mysql-data:/var/lib/mysql mysql`.

## **8. Orchestrating Containers with Docker Compose**
Docker Compose is a tool for defining and running multi-container applications using a YAML file (`docker-compose.yml`). It simplifies managing complex applications with multiple services.

- **Why Use Docker Compose?**:
  - Manages multiple containers as a single application.
  - Ensures consistent environments across development, testing, and production.
  - Simplifies configuration with a declarative YAML file.

- **Example `docker-compose.yml`**:
  ```yaml
  version: '3'
  services:
    web:
      build: .
      ports:
        - "5000:5000"
    redis:
      image: "redis:alpine"
  ```

- **Key Commands**:
  - Start services: `docker compose up` (add `-d` for detached mode).
  - Stop services: `docker compose down`.
  - List services: `docker compose ps`.
  - View logs: `docker compose logs`.

- **Installation**:
  - Docker Compose is included with Docker Desktop.
  - For standalone installation on Linux, follow [Docker Compose Installation](https://docs.docker.com/compose/install/).

## **9. Scaling with Docker Swarm**
Docker Swarm is a native orchestration tool for managing a cluster of Docker hosts, enabling scalability and high availability.

- **Key Concepts**:
  - **Swarm**: A group of Docker hosts acting as a single system.
  - **Nodes**: Individual hosts in the Swarm (managers or workers).
  - **Services**: Definitions of tasks to run on the Swarm (e.g., a web server with multiple replicas).

- **Swarm Management Commands**:
  - Initialize a Swarm: `docker swarm init`.
  - Check Swarm status: `docker system info | grep Swarm`.
  - Generate join tokens: `docker swarm join-token worker` or `docker swarm join-token manager`.
  - Leave Swarm (on leader): `docker swarm leave --force`.

- **Node Management Commands**:
  - List nodes: `docker node ls`.
  - Inspect a node: `docker node inspect <node id>`.
  - Remove a node: `docker node rm <node id>`.
  - Promote a worker to manager: `docker node promote <worker id>`.
  - Demote a manager: `docker node demote <manager id>`.

- **Service Management Commands**:
  - Create a service: `docker service create --name <service name> -p <source port>:<container port> --replicas <count> <image>`
    - Example: `docker service create --name httpd -p 9090:80 --replicas 5 httpd`.
  - List services: `docker service ls`.
  - Inspect a service: `docker service inspect <service name>`.
  - View service containers: `docker service ps <service name>`.
  - Scale a service: `docker service scale <service name>=<count>`
    - Example: `docker service scale httpd=5`.
  - Remove a service: `docker service rm <service name>`.

- **Monitoring**:
  - Use `watch -n 1 <command>` to monitor changes (e.g., `watch -n 1 docker service ls`).

## **10. Additional Resources**
To deepen your Docker knowledge, explore these resources:
- [Docker Documentation](https://docs.docker.com/): Comprehensive guides and references.
- [Docker Tutorials](https://docs.docker.com/get-started/): Hands-on tutorials for beginners.
- [Docker Compose Documentation](https://docs.docker.com/compose/): Detailed Compose usage.
- [Docker Swarm Documentation](https://docs.docker.com/engine/swarm/): Advanced orchestration techniques.