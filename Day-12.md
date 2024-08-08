# Day-12 (13-07-2024) : Azure Storage Account and Containers

## Table of Content:-
- [Storage Account](#storage-account)
- [Types of Storage Services](#types-of-storage-services)
  - [BLOB](#blob-binary-large-object)
  - [FILE](#file)
  - [TABLE](#table)
  - [QUEUE](#queue)
- [Redundancy](#redundancy)
- [Replication Types](#replication-types)
- [Erroneous Deletion](#erroneous-deletion)
- [Access Tiers](#access-tiers)
- [Snapshot](#snapshot)
- [Security and Compliance](#security-and-compliance)
  - [Example](#security-and-compliance-example)
- [Steps to configure a Storage Account and BLOB Storage](#steps-to-configure-a-storage-account-and-blob-storage)
---

## Storage Account
**Benefits:**
- **Availability and Accessibility:** Data can be accessed from anywhere with an internet connection.
- **No Fear of Hardware Failure:** Data is stored in the cloud, eliminating concerns about physical hardware failures.
- **Maintenance:** Cloud providers handle maintenance, reducing the burden on users.

**Problems with Physical Storage:**
- **Hardware Management:** Managing physical storage devices can be complex and time-consuming.
- **Data Loss/Disaster Recovery:** Physical storage is susceptible to data loss due to hardware failures or disasters, and recovery can be challenging.
- **Scalability:** Physical storage is not easily scalable. Over-provisioning can lead to high costs if the additional storage is not used.

**Handled by Storage Services:**
- Cloud storage services address these issues by providing scalable, reliable, and easily accessible storage solutions.

## Types of Storage Services:

### BLOB (Binary Large Object):
   - **Definition:** Large objects stored in binary format.
   - **Also Called:** Container.
   - **AWS Equivalent:** S3 (Simple Storage Service).
   - **Usage:** Stores items like source code, images, videos, and text.
   - **Types:**
     - **Block Blob:** Optimized for streaming and storing cloud objects.
     - **Page Blob:** Used for random read/write operations and virtual machine disks.
     - **Append Blob:** Optimized for append operations, such as logging.

### FILE:
   - **Definition:** Fully managed file shares.
   - **Examples:** SharePoint, NFS (Network File System) for Linux, SMB for Windows.
   - **AWS Equivalent:** EFS (Elastic File System).
   - **Usage:** Provides shared storage for applications using standard file system protocols.

### TABLE:
   - **Type:** NoSQL.
   - **Structure:** Key-Value pair.
   - **Feature:** Serverless, scalable storage for structured data.
   - **Examples:** Used for IoT data, metadata storage.

### QUEUE:
   - **Function:** Stores messages in a queue to be processed asynchronously.
   - **Usage:** Implements producer-consumer and publisher-subscriber patterns.
   - **AWS Equivalent:** SQS (Simple Queue Service).

---
**Here’s a diagram illustrating the Azure Storage Services:**
```
+-------------------------+      +---------------------------+
|       Blob Storage      |      |        File Storage       |
|-------------------------|      |---------------------------|
|  - VM Disk Images       |      |  - File Shares            |
|  - Media Files          |      |  - Lift-and-Shift Apps    |
|  - Backups              |      |  - Shared Storage for VMs |
|  - Log Data             |      |                           |
|  Example:               |      |  Example:                 |
|  - Image Hosting        |      |  - Departmental Shares    |
|  - Video Streaming      |      |  - App Configuration      |
+-------------------------+      +---------------------------+

+-------------------------+      +---------------------------+
|      Table Storage      |      |       Queue Storage       |
|-------------------------|      |---------------------------|
|  - User Profiles        |      |  - Task Management        |
|  - Product Info         |      |  - Background Jobs        |
|  - Metadata             |      |  - Message Queues         |
|  - IoT Data             |      |                           |
|  Example:               |      |  Example:                 |
|  - IoT Sensor Data      |      |  - Order Processing System|
|  - User Preferences     |      |  - Job Scheduling         |
+-------------------------+      +---------------------------+

```

---

## Diagram: Azure Storage Hierarchy

```plaintext
Tenant
   └── Subscription
         └── Resource Group (RG)
               └── Storage Account
                     ├── BLOB
                     │    ├── Block Blob
                     │    ├── Page Blob
                     │    └── Append Blob
                     ├── FILE
                     ├── TABLE
                     └── QUEUE
```

---

## Redundancy:
**Definition:** Making multiple copies of data to avoid loss during failures.

**Types of Redundant Storage:**
1. **LRS (Locally Redundant Storage):**
   - Data is replicated three times within a single data center.
   - Suitable for scenarios where data loss is acceptable only if the entire data center is lost.
2. **GRS (Geo-Redundant Storage):**
   - Data is replicated three times within the primary region and asynchronously to another region.
   - Provides higher durability and protection against regional disasters.
3. **ZRS (Zone-Redundant Storage):**
   - Three replicas in different zones within the same region.
4. **GZRS (Geo-Zone-Redundant Storage):**
   - Replicas in different zones across different regions.

**Note:**
- **RA (Read Access):** Prefix used for types of redundancy that allow read access to the secondary location.

```plaintext
Redundancy:
LRS
   ├── Data Center 1
   │    ├── Replica 1
   │    ├── Replica 2
   │    └── Replica 3

GRS
   ├── Primary Region
   │    ├── Data Center 1
   │    │    ├── Replica 1
   │    │    ├── Replica 2
   │    │    └── Replica 3
   │    └── Data Center 2 (secondary region)
   │         ├── Replica 4
   │         ├── Replica 5
   │         └── Replica 6
```

---

### Replication Types:
- **Synchronous:** Updates changes immediately across replicas.
- **Asynchronous:** Updates changes after some time.

### Erroneous Deletion:
- **Definition:** Deletion by mistake or misunderstanding.
- **Solution:** Soft delete is enabled to recover data from accidental deletions.

### Access Tiers:
**Definition:** Different levels of accessibility and cost for stored data.

**Types (in decreasing order of accessibility):**
1. **Hot:** Frequently accessed data (e.g., code files).
2. **Cool:** Infrequently accessed data (e.g., photos).
3. **Cold:** Rarely accessed data.
4. **Archive:** Data accessed once in a century (e.g., historical records).

### Snapshot:
- **Definition:** A copy of a blob at a specific point in time.
- **Usage:** Enables backup and recovery operations.
  
### Security and Compliance

- **Encryption:** Provides at-rest and in-transit encryption.
- **Access Control:** Implements RBAC, ACLs, and SAS for granular access control.
- **Compliance:** Meets standards such as GDPR, HIPAA, and ISO for data protection.

#### Security and Compliance Example
1. **Encryption:**
   - **At-Rest:** Data is encrypted using Azure Storage Service Encryption (SSE).
   - **In-Transit:** Data is encrypted during transfer using HTTPS.

2. **Access Control:**
   - **RBAC:** Assign roles to users, such as Storage Blob Data Contributor.
   - **ACLs:** Set permissions on individual containers and blobs.
   - **SAS (Shared Access Signatures):** Provide limited access to storage account resources.

3. **Compliance:**
   - **GDPR:** Ensures data protection and privacy in the EU.
   - **HIPAA:** Protects sensitive patient data in healthcare.
   - **ISO:** International standards for data security.

```plaintext
Security and Compliance:
   ├── Encryption
   │    ├── At-Rest: SSE
   │    └── In-Transit: HTTPS
   ├── Access Control
   │    ├── RBAC: Role assignments
   │    ├── ACLs: Permissions on resources
   │    └── SAS: Limited access tokens
   └── Compliance
        ├── GDPR
        ├── HIPAA
        └── ISO
```
---

## Steps to configure a Storage Account and BLOB Storage
1. **Create a Resource Group**
    - Navigate to the Azure portal, click on "Create a resource," select "Storage account," and fill in the necessary details.
2. **Create a Storage Account:**
   - Choose the subscription, resource group, storage account name, and region. Select the desired performance (Standard or Premium), redundancy (LRS, GRS, etc.), and access tier (Hot, Cool, etc.).

3. **Create a Container in BLOB Storage:**
   - **Navigate:** Go to the newly created storage account, select "Containers" under the BLOB service section.
   - **Create Container:** Click on "+ Container," enter the name, and set the public access level (Private, Blob, or Container).

4. **Upload a Blob:**
   - **Upload:** Inside the container, click on "Upload," select the file to upload, and click "Upload."

---

This refined overview provides a comprehensive yet concise explanation of Azure Storage Services, focusing on key features, redundancy options, data management capabilities, security considerations, and includes detailed examples and diagrams for better understanding.
This refined overview provides a comprehensive yet concise explanation of Azure Storage Services, focusing on key features, redundancy options, data management capabilities, and security considerations.
