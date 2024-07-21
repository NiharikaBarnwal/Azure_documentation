# Docker Introduction and Basic Setup

## Table of Contents

1. [Introduction to Docker](#introduction-to-docker)
2. [Software Requirements and Specification (SRS)](#software-requirements-and-specification-srs)
3. [Steps to Create an Application](#steps-to-create-an-application)
4. [Understanding Hypervisors and Dependencies](#understanding-hypervisors-and-dependencies)
5. [Benefits of Docker](#benefits-of-docker)
6. [Basic Docker Setup](#basic-docker-setup)
    - [Creating Resources in Azure](#1-creating-resources-in-azure)
    - [Installing Docker on Ubuntu VM](#installing-docker-on-ubuntu-vm)
    - [Working with Docker Containers](#working-with-docker-containers)
    - [Port Mapping and Web Server Configuration](#port-mapping-and-web-server-configuration)
7. [Useful Docker Commands](#useful-docker-commands)
8. [Enhancements and Examples](#enhancements-and-examples)

---

## Introduction to Docker

Docker is an open-source platform that enables developers to create, deploy, and manage applications inside lightweight and portable containers. These containers include everything needed to run an application, making it a more advanced version of virtualization.

**Key Points:**
- Containers are lightweight and portable.
- Docker is free to use.
- Docker engine is installed on the host system to manage containers.
- Docker images are lightweight and efficient.

## Software Requirements and Specification (SRS)

Product managers create a Software Requirements and Specification (SRS) document to outline the requirements and expectations for a new application. This document serves as a guide for developers and other stakeholders throughout the development process.

## Steps to Create an Application

1. **Identifying a Problem and Solution:**
   - Brainstorm and identify a problem that needs solving.
   - Propose a solution and outline its features.

2. **Forming SRS:**
   - Product managers create an SRS document.
   - Include detailed specifications, requirements, and use cases.

3. **Development:**
   - Developers build the application.
   - Version control is managed using GitHub.

4. **Testing:**
   - Perform code testing to ensure functionality and stability.

5. **Building:**
   - Compile the application into the appropriate format (e.g., .apk, .exe).

6. **Quality Assurance (QA):**
   - Conduct thorough testing in two phases.
   - Ensure the application meets all quality standards.

## Understanding Hypervisors and Dependencies

- **Hypervisor:** A software layer that virtualizes physical hardware, allowing multiple virtual machines (VMs) to run on a single physical machine.
- **Dependencies:** External libraries or tools required by an application to function properly.

## Benefits of Docker

- **Consistency:** Ensures applications run the same in all environments.
- **Portability:** Applications can be easily moved across different environments.
- **Efficiency:** Lightweight containers use fewer resources than traditional VMs.
- **Isolation:** Containers isolate applications from each other and the host system.
- **Scalability:** Easy to scale applications by adding more containers.

## Basic Docker Setup

### 1. Creating Resources in Azure

1. **Go to Azure Portal**
2. **Create a Resource Group (RG):**
   - Name: `Docker-RG`

3. **Create a Virtual Network (vnet)**

4. **Create an Ubuntu VM:**
   - Name: `Docker-Vm`
   - Allow all ports
   - Leave other settings as default

### Installing Docker on Ubuntu VM

1. **Connect to the VM using SSH:**
   ```bash
   ssh -i <path_to_private_key> silicon@<VM_IP>
   ```

2. **Switch to root user:**
   ```bash
   sudo su
   cd
   ```

3. **Check Docker installation:**
   ```bash
   docker --version
   ```

4. **If Docker is not installed, run the following commands:**
   ```bash
   apt update
   apt install docker.io -y
   systemctl start docker
   systemctl enable docker
   ```

### Working with Docker Containers

1. **Check for existing Docker containers and images:**
   ```bash
   docker container ls  # Shows only active containers
   docker container ls -a  # Shows all containers, including inactive ones
   docker image ls  # Lists all Docker images
   ```

2. **Download and run an Ubuntu container:**
   ```bash
   docker container run ubuntu
   ```

### Port Mapping and Web Server Configuration

1. **Run a Docker container with port mapping:**
   ```bash
   docker container run -it -p 3600:80 ubuntu /bin/bash
   ```

2. **Install and configure a web server inside the container:**
   ```bash
   apt-get update
   apt-get install apache2 -y
   cd /var/www/html
   echo "I am from container" > index.html
   cat index.html
   service apache2 start
   ```

3. **Configure an inbound rule to access port 3600:**
   - Go to Azure portal and configure the network security group (NSG) associated with the VM to allow inbound traffic on port 3600.

## Useful Docker Commands

- **Lock a user in a container for 60 seconds:**
  ```bash
  docker container run ubuntu sleep 60
  ```

- **Run a container in detached mode for 20 seconds:**
  ```bash
  docker container run -d ubuntu sleep 20
  ```

- **Stop an active container:**
  ```bash
  docker container stop <ID>
  ```

- **Remove a Docker container:**
  ```bash
  docker container rm <ID>  # Only works if the container is stopped
  docker container rm <ID> -f  # Force removes a running container
  docker container rm <ID1> <ID2> <ID3>  # Remove multiple containers at once
  ```

- **Enter a new container:**
  ```bash
  docker container run -it ubuntu /bin/bash
  ```

- **Exit from a container:**
  - Use `Ctrl + p + q`

- **Enter a running container:**
  ```bash
  docker exec -it <ID> /bin/bash
  ```

- **Configure inside a container:**
  ```bash
  apt-get update
  apt-get install apache2 -y
  cd /var/www/html
  echo "Hello container" > index.html
  cat index.html
  ```

- **Note:** The `vi` editor is not installed by default in Docker containers, so using `vi <filename>` will not work without installation.

## Enhancements and Examples

### Example: Running a Simple Web Server in a Docker Container

1. **Pull the official Nginx image:**
   ```bash
   docker pull nginx
   ```

2. **Run the Nginx container with port mapping:**
   ```bash
   docker container run -d -p 8080:80 nginx
   ```

3. **Access the web server:**
   - Open a browser and navigate to `http://<VM_IP>:8080`

### Example: Building a Custom Docker Image

1. **Create a Dockerfile:**
   ```dockerfile
   FROM ubuntu:latest
   RUN apt-get update && apt-get install -y apache2
   COPY ./index.html /var/www/html/index.html
   CMD ["apache2ctl", "-D", "FOREGROUND"]
   ```

2. **Build the Docker image:**
   ```bash
   docker build -t my-apache-server .
   ```

3. **Run the custom Docker image:**
   ```bash
   docker container run -d -p 8080:80 my-apache-server
   ```

4. **Access the web server:**
   - Open a browser and navigate to `http://<VM_IP>:8080`


---

This enhanced guide provides a comprehensive overview of Docker, from its basic setup to advanced usage examples. The inclusion of diagrams and detailed steps ensures a better grasp of Docker's capabilities and applications.
