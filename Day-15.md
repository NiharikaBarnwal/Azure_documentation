### Day-15 (16-07-2024)

**Topics Covered:**
- Azure File Sync
- Snapshot
- Swap OS Disk

---

### On-Premises Servers/Setup

**Managed by:** Private owner

**Challenges:**
- **Limited Data Capacity:** Physical servers have finite storage limits.
- **Server Lag:** Performance issues due to hardware limitations or high demand.

---

### Solution: Syncing Azure Services with On-Premises Servers

**Advantages:**
- **Backup:** Reliable and secure backups.
  - **Example:** Regularly scheduled backups to Azure ensure data safety.
- **Data Availability:** Ensure data is always accessible.
  - **Example:** Accessing files stored in Azure from any location.
- **Disaster Recovery:** Quick recovery options in case of data loss or corruption.
  - **Example:** Restoring data from Azure backups after a hardware failure.
- **Centralized Control:** Manage data efficiently from a single point.
  - **Example:** Using Azure Portal to monitor and manage all storage resources.

**Important Note:**
- This solution is applicable only on Windows servers.
- Frequently accessed data is kept on-premises, while infrequent data is stored on Azure.
- The sync is one-way: data from on-premises is synced to Azure, but not the reverse.

**Diagram: On-Premises and Azure Sync Setup**
```plaintext
+-------------------+       +-------------------+
| On-Premises       |       | Azure             |
| Windows Server    |       | Storage Account   |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| Frequently Accessed|       | Infrequently Accessed|
| Data               |       | Data                |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| Azure File Sync   |       | Azure File Sync   |
+-------------------+       +-------------------+
```

---

### Steps for Azure File Sync

1. **Create a Windows Server:**
   - Set up a Windows server that will serve as the on-premises server.
   - **Example:** Install Windows Server 2019 on a physical or virtual machine.

2. **Attach a Disk to VM and Create a Volume:**
   - Add a disk to your virtual machine (VM) and create a volume out of it for storage.
   - **Example:** Attach a 1TB disk to the VM and format it as NTFS.

3. **Create an Azure File Sync:**
   - Set up Azure File Sync service in your Azure portal.
   - **Example:** Navigate to the Azure portal, create a new Azure File Sync resource.

4. **Install the Agent on the VMs:**
   - Install the Azure File Sync agent on your on-premises Windows Server.
   - **Example:** Download and install the agent from the Azure portal.

5. **Create a Storage Account and a File Share:**
   - In Azure, create a storage account and then create a file share within that storage account.
   - **Example:** Create a storage account named `mystorageaccount` and a file share named `myfileshare`.

6. **Configure the Agent:**
   - Sign in with your Azure account credentials and enter the tenant ID to configure the agent on your Windows Server.
   - **Example:** Use PowerShell to configure the agent with your Azure credentials.

7. **Create a Sync Group and Add the Server Endpoint:**
   - In Azure, create a sync group and add your Windows Server as a server endpoint to this group.
   - **Example:** Create a sync group named `mysyncgroup` and add the server endpoint `myserver`.

**Diagram: Azure File Sync Process**
```plaintext
+-------------------+       +-------------------+
| On-Premises       |       | Azure             |
| Windows Server    |       | Storage Account   |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| Azure File Sync   |       | Azure File Sync   |
| Agent             |       | Service           |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| Sync Group        |       | Sync Group        |
+-------------------+       +-------------------+
```

---

### Snapshot

**Definition:**
- A snapshot is a point-in-time backup of your data or VM.

**Use Cases:**
- **Migration and Cloning:** Easily migrate data or clone VMs.
  - **Example:** Create a snapshot of a VM before migrating it to another region.
- **Backup:** Reliable backup option for data protection.
  - **Example:** Take regular snapshots of critical VMs for backup purposes.
- **Snapshot Reliability:** Snapshots do not crash, ensuring data integrity.
  - **Example:** Use snapshots to restore a VM to a previous state without data loss.

**Procedure:**
1. **Reference a Disk:** Create a snapshot from an existing disk.
   - **Example:** Select the disk of a running VM and create a snapshot.
2. **Create a VM from the Snapshot:** Use the snapshot to create a new VM.
   - **Example:** Use the snapshot to deploy a new VM with the same configuration.

**Diagram: Snapshot Process**
```plaintext
+-------------------+       +-------------------+
| Existing Disk     |       | Snapshot          |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| Create Snapshot   |       | New VM            |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| New VM from       |       | Snapshot          |
| Snapshot          |       |                   |
+-------------------+       +-------------------+
```

---

### Swap OS Disk

**Description:**
- Replacing the OS disk with a backup disk.

**Process:**
1. **Prepare a Backup OS Disk:**
   - Ensure you have a ready-to-use backup disk.
   - **Example:** Create a backup of the current OS disk and store it in Azure.

2. **Swap the OS Disk:**
   - Replace the existing OS disk with the backup disk to restore or update the operating system.
   - **Example:** Detach the current OS disk from the VM and attach the backup disk.

**Diagram: Swap OS Disk Process**
```plaintext
+-------------------+       +-------------------+
| Current OS Disk   |       | Backup OS Disk    |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| Detach Current    |       | Attach Backup     |
| OS Disk           |       | OS Disk           |
+-------------------+       +-------------------+
         |                           |
         v                           v
+-------------------+       +-------------------+
| VM with Backup    |       | OS Disk           |
+-------------------+       +-------------------+
```

---

These notes provide a concise overview of the topics covered and the steps involved in setting up Azure File Sync and utilizing snapshots for backup and disaster recovery.
