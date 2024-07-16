### Day-12 (13-07-2024)

### Azure Storage Services

#### Storage Account (e.g., Google Drive)
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

#### Storage Account Manages:
1. **BLOB (Binary Large Object):**
   - **Definition:** Large objects stored in binary format.
   - **Also Called:** Container.
   - **AWS Equivalent:** S3 (Simple Storage Service).
   - **Usage:** Stores items like source code, images, videos, and text.
   - **Types:**
     - **Block Blob:** Optimized for streaming and storing cloud objects.
     - **Page Blob:** Used for random read/write operations and virtual machine disks.
     - **Append Blob:** Optimized for append operations, such as logging.

2. **FILE:**
   - **Definition:** Fully managed file shares.
   - **Examples:** SharePoint, NFS (Network File System) for Linux, SMB for Windows.
   - **AWS Equivalent:** EFS (Elastic File System).
   - **Usage:** Provides shared storage for applications using standard file system protocols.

3. **TABLE:**
   - **Type:** NoSQL.
   - **Structure:** Key-Value pair.
   - **Feature:** Serverless, scalable storage for structured data.
   - **Examples:** Used for IoT data, metadata storage.

4. **QUEUE:**
   - **Function:** Stores messages in a queue to be processed asynchronously.
   - **Usage:** Implements producer-consumer and publisher-subscriber patterns.
   - **AWS Equivalent:** SQS (Simple Queue Service).

#### Hierarchy in Azure:
```
Tenant
   └── Subscription
         └── Resource Group (RG)
               └── Storage Account
```

#### Redundancy:
**Definition:** Making multiple copies of data to avoid loss during failures.

**Types of Redundant Storage:**
1. **LRS (Locally Redundant Storage):**
   - Three replicas in the same data center.
2. **GRS (Geo-Redundant Storage):**
   - Three replicas in different data centers within the same region.
3. **ZRS (Zone-Redundant Storage):**
   - Three replicas in different zones within the same region.
4. **GZRS (Geo-Zone-Redundant Storage):**
   - Replicas in different zones across different regions.

**Note:**
- **RA (Read Access):** Prefix used for types of redundancy that allow read access to the secondary location.

**Replication Types:**
- **Synchronous:** Updates changes immediately across replicas.
- **Asynchronous:** Updates changes after some time.

#### Erroneous Deletion:
- **Definition:** Deletion by mistake or misunderstanding.
- **Solution:** Soft delete is enabled to recover data from accidental deletions.

#### Access Tiers:
**Definition:** Different levels of accessibility and cost for stored data.

**Types (in decreasing order of accessibility):**
1. **Hot:** Frequently accessed data (e.g., code files).
2. **Cool:** Infrequently accessed data (e.g., photos).
3. **Cold:** Rarely accessed data.
4. **Archive:** Data accessed once in a century (e.g., historical records).

#### Snapshot:
- **Definition:** A copy of a blob at a specific point in time.
- **Usage:** Enables backup and recovery operations.
  
---

### Diagram: Azure Storage Hierarchy and Redundancy

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

#### Security and Compliance

- **Encryption:** Provides at-rest and in-transit encryption.
- **Access Control:** Implements RBAC, ACLs, and SAS for granular access control.
- **Compliance:** Meets standards such as GDPR, HIPAA, and ISO for data protection.

---

This refined overview provides a comprehensive yet concise explanation of Azure Storage Services, focusing on key features, redundancy options, data management capabilities, and security considerations.
