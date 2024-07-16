### Day-13 (14-07-2024)

#### Azure Storage Services

**Blob and File Storage:**
- **Blob Storage**: Used for storing unstructured data like images, videos, and backups. Commonly used for VMs and PCs to store large amounts of data.
  - **Example**: Storing VM disk images, media files, and logs.
- **File Storage**: Provides fully managed file shares in the cloud that are accessible via the SMB protocol.
  - **Example**: File shares for lift-and-shift applications, shared storage for applications running on VMs.

**Table and Queue Storage:**
- **Table Storage**: A NoSQL store for schemaless storage of structured data. Ideal for development scenarios requiring fast access to large amounts of data.
  - **Example**: Storing user profiles, product information, and other metadata.
- **Queue Storage**: Used for storing large numbers of messages that can be accessed from anywhere in the world. Useful for decoupling application components.
  - **Example**: Managing tasks in a distributed system, processing background jobs.

#### Limitations of Mounting a Container

- **Not Persistent**: After rebooting, the mounting is not retained.
  - **Example**: If you mount a container to a VM and then reboot the VM, the mount will need to be re-established.
- **Size/Volume Cannot Be Increased**: The size or volume of the container cannot be increased once it is created.
  - **Example**: If you initially allocate 100GB to a container, you cannot increase it to 200GB later without creating a new container.

#### Diagram

Here's a simple diagram to illustrate the Azure Storage Services:

```plaintext
+---------------------+       +---------------------+
|     Blob Storage    |       |     File Storage    |
|  - VM Disk Images   |       |  - File Shares      |
|  - Media Files      |       |  - Lift-and-Shift   |
|  - Backups          |       |    Applications     |
+---------------------+       +---------------------+

+---------------------+       +---------------------+
|    Table Storage    |       |    Queue Storage    |
|  - User Profiles    |       |  - Task Management  |
|  - Product Info     |       |  - Background Jobs  |
|  - Metadata         |       |                     |
+---------------------+       +---------------------+
```
