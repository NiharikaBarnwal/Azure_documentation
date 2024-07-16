### Day-15 (16-07-2024)

**Topics Covered:**
- Azure File Sync
- Snapshot
- Swap OS disk

---

### On-Premises Servers/Setup
**Managed by:** Private owner
**Challenges:**
- Limited data capacity
- Server lag

---

### Solution: Syncing Azure Services with On-Premises Servers

**Advantages:**
- **Backup:** Reliable and secure backups.
- **Data Availability:** Ensure data is always accessible.
- **Disaster Recovery:** Quick recovery options in case of data loss or corruption.
- **Centralized Control:** Manage data efficiently from a single point.

**Important Note:**
- This solution is applicable only on Windows servers.
- Frequently accessed data is kept on-premises, while infrequent data is stored on Azure.
- The sync is one-way: data from on-premises is synced to Azure, but not the reverse.

---

### Steps for Azure File Sync

1. **Create a Windows Server:**
   - Set up a Windows server that will serve as the on-premises server.

2. **Attach a Disk to VM and Create a Volume:**
   - Add a disk to your virtual machine (VM) and create a volume out of it for storage.

3. **Create an Azure File Sync:**
   - Set up Azure File Sync service in your Azure portal.

4. **Install the Agent on the VMs:**
   - Install the Azure File Sync agent on your on-premises Windows Server.

5. **Create a Storage Account and a File Share:**
   - In Azure, create a storage account and then create a file share within that storage account.

6. **Configure the Agent:**
   - Sign in with your Azure account credentials and enter the tenant ID to configure the agent on your Windows Server.

7. **Create a Sync Group and Add the Server Endpoint:**
   - In Azure, create a sync group and add your Windows Server as a server endpoint to this group.

---

### Snapshot

**Definition:**
- A snapshot is a point-in-time backup of your data or VM.

**Use Cases:**
- **Migration and Cloning:** Easily migrate data or clone VMs.
- **Backup:** Reliable backup option for data protection.
- **Snapshot Reliability:** Snapshots do not crash, ensuring data integrity.

**Procedure:**
1. **Reference a Disk:** Create a snapshot from an existing disk.
2. **Create a VM from the Snapshot:** Use the snapshot to create a new VM.

---

### Swap OS Disk

**Description:**
- Replacing the OS disk with a backup disk.

**Process:**
1. **Prepare a Backup OS Disk:**
   - Ensure you have a ready-to-use backup disk.

2. **Swap the OS Disk:**
   - Replace the existing OS disk with the backup disk to restore or update the operating system.

---

These notes provide a concise overview of the topics covered and the steps involved in setting up Azure File Sync and utilizing snapshots for backup and disaster recovery.
