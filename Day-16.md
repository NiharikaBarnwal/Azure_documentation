# Day-16 (17-07-2024) : Azure Persistent Disk CDN

## Table of Contents
  - [Persistent Disk](#persistent-disk)
    - [Types of Disks](#types-of-disks)
    - [Specifications](#specifications)
    - [Key Concepts](#key-concepts)
    - [Redundancy Support](#redundancy-support)
    - [Shared Volume Support](#shared-volume-support)
    - [Usability as OS disk](#usability-as-os-disk)
    - [Diagram](#diagram)
  - [CDN (Content Delivery Network)](#cdn-content-delivery-network)
    - [AWS Equivalent](#aws-equivalent)
    - [Direct Benefits](#direct-benefits)
    - [Indirect Benefits](#indirect-benefits)
    - [Steps to Implement CDN](#steps-to-implement-cdn)
    - [Diagram](#diagram-1)
  - [App Services](#app-services)
    - [Examples](#examples)
    - [Requirements](#requirements)
    - [Benefits](#benefits)
    - [Steps to Implement App Services](#steps-to-implement-app-services)
    - [Diagram](#diagram-2)
  - [Azure DNS](#azure-dns)
    - [Domain Registries](#domain-registries)
    - [AWS Equivalent](#aws-equivalent-1)
    - [Types of Records](#types-of-records)
    - [Steps to Configure Azure DNS](#steps-to-configure-azure-dns)
    - [Diagram](#diagram-3)
---

## Persistent Disk
Azure Persistent Disks provide block-level storage volumes that are used with Azure Virtual Machines (VMs). Disks in Azure are virtualized and can be managed as either Managed Disks or Unmanaged Disks.

### Types of Disks:

1. **Managed Disk:**
   Managed Disks simplify storage management by handling the storage account for you. Azure manages the storage, making scaling and management easier.
    - **Categories:** 
        - Standard HDD :
          - Cost-effective storage for infrequently accessed data.
          - Scenario: Backup, non-critical, infrequent access
        - Standard SSD :
          -  Better performance than HDD, suitable for web servers and lightly used applications.
          - Scenario: Web servers, lightly used enterprise applications and dev/test
        - Premium SSD :
          - High-performance storage for mission-critical applications.
          - Scenario: Production and performance sensitive workloads
        - Ultra Disk :
          - Ultra-high performance for data-intensive workloads.
          - Scenario: 	IO-intensive workloads such as SAP HANA, top tier databases (for example, SQL, Oracle), and other transaction-heavy workloads.

2. **Unmanaged Disk:**
   Unmanaged Disks require you to handle the storage accounts and the VHD files used by VMs. They provide more control but require more effort to manage.
    - **Categories:**
        - Standard HDD : Similar to managed Standard HDD but requires manual management.
        - Standard SSD : Similar to managed Standard SSD but requires manual management.

### Specifications:
```
+------------------------------------------------------------------------------------------+ 
|                    |                 Managed Disk                    | Unmanaged Disk    |
|--------------------|-------------------------------------------------|-------------------|
|                    | Std HDD  | Std SSD   | Prem SSD  | Ultra Disk   | Std HDD | Std SSD |
|   Min Size         | 1 GB     | 1 GB      | 1 GB      | 4 GB         | 1 GB    | 1 GB    |
|   Max Size         | 32,767 GB| 32,767 GB | 32,767 GB | 64 TB        | 4 TB    | 4 TB    |
|   IOPS Min         | 500 MB   | 120 MB    | 120 MB    | 100 MB       | 500 MB  | 500 MB  |
|   IOPS Max         | 2,000 MB | 6,000 MB  | 20,000 MB | 1,600,000 MB | 500 MB  | 750 MB  |
|   Throughput Min   |          | 25 MB     | 255 MB    | 25 MB        | 60 MB   | 100 MB  |
|   Throughput Max   | 500 MB   | 750 MB    | 900 MB    | 2,000 MB     |         | 250 MB  |
+------------------------------------------------------------------------------------------+
```

### Key Concepts:

- **IOPS (Input/Output Operations Per Second):** Qualitative measure indicating how many read/write operations can be performed per second.
- **Throughput:** Quantitative measure indicating the amount of data (in MB/KB) that can be read or written per second.

### Redundancy Support:
- **LRS (Locally Redundant Storage):** Supports all managed disk types.
- **ZRS (Zone Redundant Storage):** Supports only Standard SSD and Premium SSD.

### Shared Volume Support:
- Only Premium SSD and Ultra Disk support shared volumes.

### Usability as OS disk
- Ultra disk cannot be used as OS disk

### Diagram
```
+---------------------+
|     Managed Disk    |
|  +---------------+  |
|  | Standard HDD  |  |
|  | Standard SSD  |  |
|  | Premium SSD   |  |
|  | Ultra Disk    |  |
+---------------------+

+---------------------+
|   Unmanaged Disk    |
|  +---------------+  |
|  | Standard HDD  |  |
|  | Standard SSD  |  |
+---------------------+
```

---

## CDN (Content Delivery Network)
Azure CDN helps reduce latency by creating Points of Presence (POPs) or Edge Locations closer to end-users. These store cached content, minimizing the distance data needs to travel.
### AWS Equivalent:
- **CloudFront**

### Direct Benefits:
- **Reduced Latency:** By reducing the number of hops, latency decreases. POP (Point of Presence) edge locations store cached content, thus reducing latency.

### Indirect Benefits:
- **Load Reduction:** Reduces the load on the origin server.
- **Increased Security:** Enhances security by distributing content.
- **Higher Uptime:** Improves the overall uptime of the service.

### Steps to Implement CDN:
1. **Create a Resource Group.**
2. **Create a Storage Account:**
    - Fill in the required details.
    - Enable anonymous access and accept default settings.
3. **Create a Container in the Storage Account:**
    - Upload the files to the container.
4. **Create a CDN Profile:**
    - Fill in the required details and accept default settings.
5. **Create a Front Door Profile:**
    - Fill in the required details and accept default settings.
6. **Endpoint Hostname:**
    - The generated endpoint hostname is provided to the on-premise service provider/developer.

### Diagram
```
+---------------------+
|     CDN Profile     |
|  +---------------+  |
|  |  Front Door   |  |
|  +-------+-------+  |
|          |          |
|  +-------+-------+  |
|  |  Storage Acc  |  |
|  +-------+-------+  |
|  |  Container    |  |
|  +---------------+  |
+---------------------+
```

---

## App Services
Azure App Services provide a PaaS environment for deploying and scaling web applications. It simplifies infrastructure management and reduces costs for small-scale deployments.
**Platform as a Service (PaaS) for Small Businesses and Small Scale Deployments**

### Examples:
- Portfolios
- Resumes

### Requirements:
- Define the tech stack.
- Define the database server.
- Source code.
- Docker image.

### Benefits:
- Provides a DNS for web/app server access.
- Cost-effective solution.

### Steps to Implement App Services:
1. **Create a GitHub Repository and Upload Files.**
2. **Create a Resource Group.**
3. **Create a Static Web App:**
    - Log in to GitHub.
    - Fill in the required details.
    - Select the repository.
    - Choose the build storage.
    - Accept default settings.
4. **Access URL:**
    - The generated URL displays the deployed content.

### Diagram
```
+---------------------+
|   Static Web App    |
|  +---------------+  |
|  |  GitHub Repo  |  |
|  +-------+-------+  |
|          |          |
|  +-------+-------+  |
|  |  Resource Grp |  |
|  +---------------+  |
+---------------------+
```

---

## Azure DNS

**Configures/Connects an IP with a Domain Name**

### Domain Registries:
They are the websites where we can purchase domain names.
- GoDaddy
- Amazon
- BidRock
- Hostinger
- NameCheap
- Dynadot
- Hover
- Bluehost

### AWS Equivalent:
- **Route 53**

### Types of Records:
- **NS (Name Server):** Changes the domain name configuration.
- **SOA (Start of Authority):** Authorizes the domain name.
- **A (Alias):** Maps the IPv4 with the domain name.
- **AAAA:** Maps the IPv6 with the domain name.
- **CNAME:** Provides a certification to the website.
- **MX (Mail Exchange):** Supports email services.

### Steps to Configure Azure DNS:
1. **Purchase a Domain Name from a Domain Registry.**
2. **Create a Resource Group.**
3. **Create a VM:**
    - Configure the VM to deploy a web server.
4. **Create a DNS Zone:**
    - Fill in the required details and accept default settings.
5. **Manage Domain:**
    - Go to the domain registry and manage the domain.
    - Add the 4 name servers generated by Azure (remove the last dot in each name server).
6. **Add Recordsets:**
    - Paste the IP of the VM.
    - Add other details (e.g., names like www, app, etc.).

### Diagram
```
+---------------------+
|     Domain Name     |
|  +---------------+  |
|  |  DNS Zone     |  |
|  +-------+-------+  |
|          |          |
|  +-------+-------+  |
|  |  VM (Web Srv) |  |
|  +---------------+  |
+---------------------+
```
