# Docker: Volumes, Dockerfiles, and Private Registries

## Table of Contents
1. [Introduction to Docker](#introduction-to-docker)
2. [Microservices Architecture](#microservices-architecture)
3. [On-Premise Storage with Private Registries](#on-premise-storage-with-private-registries)
4. [Security Compliance](#security-compliance)
5. [Docker Volumes](#docker-volumes)
    - [Hands-On Tasks](#hands-on-tasks)
      - [Task 1: Single Docker Volume Mapped to Two Docker Containers](#task-1-single-docker-volume-mapped-to-two-docker-containers)
      - [Task 2: Two Docker Volumes Mapped to a Single Docker Container](#task-2-two-docker-volumes-mapped-to-a-single-docker-container)
      - [Task 3: Blob Storage Mounted to a Docker Volume](#task-3-blob-storage-mounted-to-a-docker-volume)
    - [Diagram: Docker Volume Mapping](#diagram-docker-volume-mapping)
    - [Steps to Create a Docker Volume](#steps-to-create-a-docker-volume)
    - [Learning More About Docker Volumes](#learning-more-about-docker-volumes)
6. [Dockerfiles: Building Docker Images](#dockerfiles-building-docker-images)
    - [Steps to Create a Dockerfile](#steps-to-create-a-dockerfile)

## Introduction to Docker

Docker is a platform that allows developers to automate the deployment of applications inside lightweight, portable containers. These containers can run on any system with Docker installed, providing consistent environments for development, testing, and production.

### Importance of Docker
- **Resource Utilization:** Docker ensures efficient use of system resources by isolating applications in containers.
- **Environment Isolation:** Each container has its environment, making it easy to manage dependencies and configurations.

## Microservices Architecture

Microservices architecture involves breaking down a large application into smaller, independent services that communicate with each other. Docker plays a crucial role in this architecture.

### Characteristics
- **Small Applications:** Each service focuses on a specific business function.
- **Lightweight Containers:** Docker containers are used to package and deploy these services.
- **Resource Efficiency:** Unlike traditional virtual machines (VMs), Docker containers share the host OS kernel, making them more resource-efficient.
- **Fast Autoscaling:** Docker facilitates rapid scaling of services based on demand.
- **Environment Consistency:** Containers eliminate issues caused by differences in development and production environments.

## On-Premise Storage with Private Registries

For organizations requiring on-premise storage due to security or compliance reasons, private Docker registries are used instead of public ones. These registries allow secure storage and management of Docker images.

## Security Compliance

Ensuring data security in Docker involves several best practices:
- **Data Encryption:** Both data at rest and data in transit should be encrypted.
- **Security Certifications:** Courses like CCSP help DevOps engineers learn secure data storage methods.
- **Compliance Standards:** Follow protocols like SOC1, SOC2, and HIPAA, which are also adhered to by cloud providers like AWS and Azure.

## Docker Volumes

Docker volumes are used to persist data generated by and used by Docker containers. They provide a way to share data between the host and containers, and among multiple containers.

### Key Points
- **Data Persistence:** Volumes retain data even after the container is deleted.
- **Shared Storage:** A volume can be shared among multiple containers.
- **Low Latency:** Volumes reduce data access latency compared to other storage methods.

### Hands-On Tasks

#### Task 1: Single Docker Volume Mapped to Two Docker Containers
  - Docker allows multiple containers to share the same volume, facilitating data sharing and communication between containers.

 **Steps:**
1. Create a Docker volume:
    ```bash
    docker volume create myvolume
    ```
2. Run two containers and map the same volume to both:
    ```bash
    docker run -it -v myvolume:/data --name container1 ubuntu /bin/bash
    docker run -it -v myvolume:/data --name container2 ubuntu /bin/bash
    ```
3. Verify the volume is shared:
    ```bash
    touch /data/file_from_container1  # Inside container1
    ls /data  # Inside container2
    ```

#### Task 2: Two Docker Volumes Mapped to a Single Docker Container
  - A single container can have multiple volumes mapped to it, allowing for organized data storage and separation of concerns within the application.

 **Steps:**
1. Create two Docker volumes:
    ```bash
    docker volume create volume1
    docker volume create volume2
    ```
2. Run a container and map both volumes:
    ```bash
    docker run -it -v volume1:/data1 -v volume2:/data2 --name container ubuntu /bin/bash
    ```
3. Verify both volumes are accessible:
    ```bash
    ls /data1
    ls /data2
    ```

#### Task 3: Blob Storage Mounted to a Docker Volume
   - Blob storage can be mounted to a Docker volume, enabling the container to interact with external storage resources.

 **Steps:**
1. Create and mount blob storage to a volume (requires additional setup and tools like Azure CLI or AWS CLI).
2. Map the volume to a Docker container:
    ```bash
    docker run -it -v blobvolume:/data --name container ubuntu /bin/bash
    ```
3. Verify the data access:
    ```bash
    ls /data
    ```
### Diagram: Docker Volume Mapping
```
+--------------------+       +--------------------+
|   Docker Host      |       |    Docker Host     |
|--------------------|       |--------------------|
|  Container1        |       |  Container2        |
|  /data (myvolume)  |       |  /data (myvolume)  |
|                    |       |                    |
+--------------------+       +--------------------+
            |                        |
            +----------+-------------+
                       |
                 +-----------+
                 | myvolume  |
                 +-----------+
```

### Steps to Create a Docker Volume

1. **Create a Resource Group (RG)**
    
2. **Create a Virtual Network (VNet)**
    
3. **Create an Ubuntu VM and Allow All Ports:**
    - Serve as Docker host.
      
4. **Connect to the VM:**
    ```bash
    ssh -i azureuser@<public-ip-address>
    ```
5. **Connect to Root Administrator:**
    ```bash
    sudo su
    cd
    ```
6. **Install Docker:**
    ```bash
    apt-get update
    apt install docker.io
    docker image ls
    ```
7. **Create a Docker Volume:**
    ```bash
    docker volume create myvolume
    docker volume ls
    ```
8. **Create and Connect to Docker Container:**
    ```bash
    docker inspect myvolume
    cd <path inside volume>
    touch host{1..100}
    cd
    docker run -it -v myvolume:/tmp --name web-server ubuntu /bin/bash
    ls
    cd tmp
    ls  # All 100 touch files are present here
    touch container{1..100}
    ```

## Learning More About Docker Volumes

1. **Check if Newly Created Files Are Synced:**
    ```bash
    Ctrl + p + q
    cd <path inside volume>
    ls  # All newly created files are also here
    ```
2. **Create a New Folder and Mount It as a Volume:**
    ```bash
    mkdir /web
    cd /web
    touch abc{1..100}
    ls
    cd
    docker run -it -v /web:/tmp ubuntu /bin/bash
    ls
    cd /tmp
    ls  # All abc touch files are present
    touch cont{1..100}
    ls
    Ctrl + p + q
    cd /web
    ls  # All cont touch files are also present
    ```
3. **Create a File and Mount It as a Volume:**
    ```bash
    mkdir /web-server
    cd /web-server/
    echo "I am from volume">index.html
    cat index.html
    cd
    docker run -it -p 3600:80 -v /web-server:/var/www/html ubuntu /bin/bash
    cd /var/www/html
    ls
    Install apache2:
    apt-get update
    apt-get install apache2
    service apache2 start
    echo "updated inside container">index.html
    Ctrl + p + q
    ```
4. **Update a Container File from the Host:**
    ```bash
    echo "updated from host">index.html
    ```

---

## Dockerfiles: Building Docker Images

A Dockerfile is a text document that contains all the commands to assemble an image. It automates the process of image creation, ensuring consistency and repeatability.

### ACR Stores Docker Image
- ACR (Azure Container Registry) is used to store Docker images.
- Docker images can be created from Dockerfiles and then stored in ACR or other registries.

### Steps to Create a Dockerfile

1. **Create a Resource Group (RG)**
    
2. **Create a Virtual Network (VNet)**
    
3. **Create an Ubuntu VM and Allow All Ports:**
    - Serve as Docker host.

4. **Connect to the VM:**
    ```bash
    ssh -i azureuser@<public-ip-address>
    ```
5. **Connect to Root Administrator:**
    ```bash
    sudo su
    cd
    ```
6. **Install Docker:**
    ```bash
    apt-get update
    apt install docker.io
    docker image ls
   ```

4. **Create a Docker File**
   ```bash
   vi Dockerfile  # Name should compulsorily be Dockerfile
   ```

5. **Add Instructions to Docker File**
   ```dockerfile
   FROM ubuntu:14.04
   RUN apt-get update
   RUN touch abc
   ```

6. **Build Docker Image**
   ```bash
   docker image build -t myimage .
   docker image ls  # Verify image creation
   ```

7. **Create Container from the Image**
   ```bash
   docker container run -it myimage /bin/bash
   ls  # Verify files
   ```

---

Docker simplifies the process of managing application environments and scaling services. Understanding Docker volumes, Docker files, and private registries enhances efficiency and security in containerized application deployments.