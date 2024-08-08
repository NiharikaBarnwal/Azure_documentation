# Day-1 (26-06-2024) : Introduction to cloud computing and Azure

## Table of Content:-
1. [Cloud Computing](#cloud-computing)
2. [Client-Server Model](#client-server-model)
3. [Web Server](#web-server)
4. [Getting IP Address](#getting-ip-address)
5. [Load Balancer (LB)](#load-balancer-lb)
6. [Problems with On-Premise Servers](#problems-with-on-premise-servers)
7. [NIST](#nist)
8. [Hypervisor](#hypervisor)
9. [Cloud Computing](#cloud-computing)
10. [Datacenters](#datacenters)
11. [Top Benefits of Cloud](#top-benefits-of-cloud)
12. [Cloud Service Models](#cloud-service-models)
    - [Diagram](#diagram)
13. [Types of Cloud Deployment](#types-of-cloud-deployment)
14. [IT Process Management](#it-process-management)
15. [Roles in Software Projects](#roles-in-software-projects)
16. [Automating Processes](#automating-processes)


## Cloud Computing:
- **Definition**: Cloud computing is the delivery of computing services over the internet ("the cloud") to offer faster innovation, flexible resources, and economies of scale.
- **Examples**: Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform (GCP), Oracle Cloud Infrastructure (OCI).

## Client-Server Model:
- **Client**: The device or application that makes requests to the server.
- **Server**: The device or application that responds to the client's requests.

## Web Server:
- **IP Address**: Unique address that identifies a device on the internet.
- **Domain Name**: Human-readable address that is mapped to an IP address.
- **Process**: When a domain name is entered in a browser, it gets converted to the corresponding IP address using DNS, and the request is sent to the server at that IP.

## Getting IP Address:
- **Command**: `ping google.com`
  - **Example**: 
    ```bash
    ping google.com
    ```
  - This command sends packets to google.com and retrieves its IP address.

## Load Balancer (LB):
- **Purpose**: Distributes incoming network traffic across multiple servers to ensure no single server becomes overwhelmed, improving responsiveness and availability.
- **Example**: AWS Elastic Load Balancer (ELB).

## Problems with On-Premise Servers:
- **Issues**:
  - Websites stop responding during high traffic.
  - Harder to maintain due to physical infrastructure.
  - Many unused resources lead to inefficiency.
  - Higher costs due to infrastructure and maintenance.

## NIST:
- **Role**: National Institute of Standards and Technology helps define cloud computing standards.
- **Resource Renting**: Allows renting of idle computing resources from distant locations, though accessibility can be an issue if resources are far away.

## Hypervisor:
- **Definition**: Software that creates and runs virtual machines (VMs) by converting physical resources into virtual ones.
- **Types**: Type 1 (Bare-metal), Type 2 (Hosted).

## Cloud Computing:
- **Concept**: Access computing resources over the internet, enabling global access and scalability.

## Datacenters:
- **Definition**: Facilities that house multiple servers and networking devices.
- **Function**: Virtualize physical systems for efficient resource use.

## Top Benefits of Cloud:
- **Cost**: Pay-as-you-go model reduces capital expenditure.
- **Speed**: Rapid provisioning of resources, including auto-scaling.
- **Global Scale**: Reduced latency and enhanced performance due to geographically distributed datacenters.
- **Productivity**: Offloads server management, allowing focus on core business tasks.
- **Performance**: Enhanced performance due to optimized resource use and reduced latency.
- **Reliability**: High reliability with robust security compliances and redundancy.

## Cloud Service Models:
- **IaaS (Infrastructure as a Service)**: Provides virtualized computing resources over the internet.
  - **Example**: AWS EC2, Azure VMs.
- **PaaS (Platform as a Service)**: Offers hardware and software tools over the internet.
  - **Example**: Google App Engine, Azure App Service.
- **SaaS (Software as a Service)**: Delivers software applications over the internet.
  - **Example**: Salesforce, Microsoft Office 365.
 
### Diagram:

```
+---------------+-------------+------+---------+------------+-----+----------------+---------+---------+------------+
| Service Model | Application | Data | Runtime | Middleware | O/S | Virtualization | Servers | Storage | Networking |
+---------------+-------------+------+---------+------------+-----+----------------+---------+---------+------------+
|  On-Premises  |      x      |   x  |    x    |      x     |  x  |        x       |    x    |    x    |      x     |
|     IAAS      |      x      |   x  |    x    |      x     |  x  |        ✓       |    ✓   |    ✓    |      ✓     |
|     PAAS      |      x      |   x  |    ✓    |      ✓    |  ✓  |        ✓       |    ✓   |    ✓    |      ✓     |
|     SAAS      |      ✓      |  ✓  |    ✓    |      ✓    |  ✓  |        ✓       |    ✓   |    ✓    |      ✓     |
+---------------+-------------+------+---------+------------+-----+----------------+---------+---------+------------+

x - Subscriber/Resource owner
✓ - Service Provider

```

## Types of Cloud Deployment:
- **Public Cloud**: Services offered over the public internet and available to anyone.
  - **Examples**: AWS, Azure, GCP.
- **Private Cloud**: Cloud infrastructure operated solely for a single organization.
  - **Example**: On-premise private datacenters.
- **Hybrid Cloud**: Combines public and private clouds, allowing data and applications to be shared between them.
  - **Example**: A company uses both on-premise resources and cloud services.

## IT Process Management:
- **Pipeline**: Develop → Test → Build → Quality Test → Production.
- **Continuous Integration/Continuous Deployment (CI/CD)**: Automates and streamlines the software development process.

## Roles in Software Projects:
- **Developers**: Write and maintain code.
- **Desktop Support Engineers**: Provide technical support for software issues.
- **System Administrators**: Manage and maintain IT infrastructure.
- **Testers**: Ensure the software meets quality standards.
- **Builders**: Compile and build the software.
- **DevOps**: Automate processes and manage the development lifecycle.

## Automating Processes:
- **Version Control**: Git/GitHub.
  - **Example**: 
    ```bash
    git init
    git add .
    git commit -m "Initial commit"
    git push origin main
    ```
- **Testing**: SonarQube for static code analysis.
- **Build**: Maven for build automation.
- **Quality Testing**: Ansible for configuration management.
- **Auto Scaling**: Docker for containerization.
- **Container Management**: Kubernetes for orchestrating containers.
- **Automation**: Jenkins for CI/CD.
- **Monitoring**: Dynatrace, Grafana, Datadog for resource monitoring.
