# Day-14 (15-07-2024) : Azure Static Website Hosting Storage Explorer

## Table of Contents
 - [Static Website Hosting](#static-website-hosting)
     - [VM Configuration as a Web Server](#vm-configuration-as-a-web-server)
     - [Advantages of Static Website Hosting](#advantages-of-static-website-hosting)
     - [Diagram: Static Website Hosting Setup](#diagram-static-website-hosting-setup)
 - [Azure Storage Explorer](#azure-storage-explorer)
     - [Use Cases](#use-cases)
     - [Diagram: Azure Storage Explorer Use Cases](#diagram-azure-storage-explorer-use-cases)
 - [Types of Test Storage](#types-of-test-storage)
     - [Managed Disk](#managed-disk)
     - [Unmanaged Disk](#unmanaged-disk)
     - [Diagram: Managed vs. Unmanaged Disks](#diagram-managed-vs-unmanaged-disks)

---

## Static Website Hosting

### VM Configuration as a Web Server:
- **Windows:** Internet Information Services (IIS)
  - **Example:** Hosting a company’s internal documentation site.
- **Linux:** Apache2
  - **Example:** Hosting a personal blog or portfolio.

### Advantages of Static Website Hosting:
- **Ease of Use:** Provides a URL, HTTPS, and certificate automatically.
  - **Example:** Azure Static Web Apps automatically configures HTTPS for your custom domain.
- **Cost-Effective:** Cheaper and easier to manage compared to dynamic websites.
  - **Example:** Hosting a static site on Azure Blob Storage is more cost-effective than using a full-fledged web server.
- **Simplified Management:** Requires less maintenance and management.
  - **Example:** No need to manage server-side code or databases.

### Diagram: Static Website Hosting Setup
```plaintext
+-------------------+
| Static Website    |
| (HTML, CSS, JS)   |
+-------------------+
         |
         v
+-------------------+
| Azure Blob Storage|
+-------------------+
         |
         v
+-------------------+
| HTTPS/URL         |
+-------------------+
```

## Azure Storage Explorer

### Use Cases:
1. **Replicating a VM to Another VM:**
   - **Example:** Creating a backup of a production VM to a test environment.
2. **Replicating from One Tenant to Another Tenant:**
   - **Example:** Migrating data from a development tenant to a production tenant for deployment.

### Diagram: Azure Storage Explorer Use Cases
```plaintext
+-------------------+       +-------------------+
| VM in Tenant A    |       | VM in Tenant B    |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| Azure Storage     |       | Azure Storage     |
| Explorer          |       | Explorer          |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| Replication       |       | Replication       |
+-------------------+       +-------------------+
```

## Types of Test Storage

### Managed Disk:
- **Management:** Managed by Azure.
  - **Example:** Azure Premium SSD Managed Disks.
- **Ease of Use:** Simplifies management with built-in features.
  - **Example:** Automatic snapshots and backups.
- **Scalability:** Automatically scalable to meet demands.
  - **Example:** Scale up storage capacity without downtime.
- **Availability:** Azure handles availability checks and ensures redundancy.
  - **Example:** Built-in high availability and disaster recovery.
- **Backup:** Integrated backup solutions.
  - **Example:** Azure Backup service.
- **Cost:** Higher cost due to additional features and management.

### Unmanaged Disk:
- **Management:** Managed by the user.
  - **Example:** Manually attaching and managing VHD files.
- **Simplicity:** Simpler setup and configuration.
  - **Example:** Directly managing disk storage without Azure's automated features.
- **Use Case:** Suitable for low-level applications and environments where cost is a critical factor.
  - **Example:** Development environments with tight budgets.
- **Cost:** Lower cost, but requires more manual management and monitoring.

### Diagram: Managed vs. Unmanaged Disks
```plaintext
+-------------------+       +-------------------+
| Managed Disk      |       | Unmanaged Disk    |
+-------------------+       +-------------------+
| Managed by Azure  |       | Managed by User   |
| Automatic Scaling |       | Manual Scaling    |
| High Availability |       | User-Managed HA   |
| Integrated Backup |       | Manual Backup     |
+-------------------+       +-------------------+
```

---

These notes provide a comprehensive overview of the topics covered, highlighting the key points and benefits of each technology.
