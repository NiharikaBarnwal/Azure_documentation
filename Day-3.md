# Day 3: Azure Student Subscription & Virtual Machines Overview

## Table of Contents
1. [Setting Up an Azure Student Account](#setting-up-an-azure-student-account)
2. [Understanding Virtual Machines](#understanding-virtual-machines)
   - [What is a Virtual Machine?](#what-is-a-virtual-machine)
   - [Core Components](#core-components)
   - [Steps to Deploy a Virtual Machine](#steps-to-deploy-a-virtual-machine)
   - [Managing & Monitoring VMs](#managing-&-monitoring-vms)

---

## Setting Up an Azure Student Account

### How to Register for Azure for Students

1. **Access the Azure Student Portal**  
   - Visit the [Azure for Students page](https://azure.microsoft.com/en-us/free/students/).
   - Click **"Activate now"** to start the registration process.

2. **Verify Student Status**  
   - Log in using your educational institution’s email address.
   - If you lack a school email, you may need to provide additional verification (e.g., student ID or enrollment proof).

3. **Identity Verification**  
   - Enter required details such as name, email, and institution name.
   - Confirm your identity using the verification method provided.

4. **No Payment Details Needed**  
   - No credit card is required for registration.
   - You will receive $100 in free credits valid for 12 months along with access to essential Azure services.

5. **Complete Setup & Access Azure**  
   - Once verification is successful, finalize your registration.
   - You can now log into the Azure portal and begin using cloud services.

---

## Understanding Virtual Machines

### What is a Virtual Machine?
A Virtual Machine (VM) is a software-based simulation of a physical computer that runs an operating system and applications independently. VMs allow multiple OS environments to coexist on a single physical machine, making them highly flexible and efficient.

**Example Scenario:**  
Suppose you own a Windows laptop but need a Linux environment for a project. Instead of purchasing a new device, you can create a Linux VM on your laptop, running both operating systems side by side. Similarly, in Azure, you can deploy VMs to run different workloads without managing the physical infrastructure.

### Core Components of an Azure VM

1. **Resource Group**  
   - A logical container to manage related resources.
   - Example: `StudentProjectResourceGroup`.

2. **Virtual Network (VNet)**  
   - Provides network isolation for your VM.
   - Example: `MyVNet` with an address range of `10.0.0.0/16`.

3. **Subnet**  
   - A segment within a virtual network to manage IP addressing.
   - Example: `MySubnet` (Address Range: `10.0.0.0/24`).

4. **Network Interface Card (NIC)**  
   - Connects the VM to the VNet for communication.
   - Example: `VM-NIC-1`.

5. **Public IP Address**  
   - Enables internet connectivity for the VM.
   - Example: `MyPublicIP`.

6. **Network Security Group (NSG)**  
   - Controls inbound and outbound traffic for security.
   - Example: `MyNSG` with rules for SSH (port 22) and RDP (port 3389).

---

## Steps to Deploy a Virtual Machine

1. **Sign in to the Azure Portal**  
   - Go to [Azure Portal](https://portal.azure.com/) and log in.

2. **Create a Resource Group**  
   - Navigate to **"Resource Groups"** > **"Create"**.
   - Define a unique name and select a region.
   - Click **"Review + Create"** > **"Create"**.

3. **Set Up a Virtual Machine**  
   - Go to **"Virtual Machines"** > **"Create"**.
   - Select your subscription and resource group.
   - Enter a VM name, region, and choose an OS (e.g., Ubuntu Server).
   - Pick a suitable VM size (based on workload needs).

4. **Configure Authentication**  
   - Define a username and either set a password or SSH key for secure access.

5. **Networking Setup**  
   - Choose an existing VNet or create a new one.
   - Assign a subnet and public IP address.
   - Link a Network Security Group to control access.

6. **Finalize & Deploy**  
   - Review all settings carefully.
   - Click **"Review + Create"** > **"Create"**.
   - Wait for Azure to deploy your VM.

7. **Access Your VM**  
   - After deployment, find the VM in the portal.
   - Copy the public IP and use:
     - SSH (for Linux) or RDP (for Windows) to connect.

---

## Managing & Monitoring VMs

1. **Basic Operations**  
   - Start, stop, or restart VMs using the Azure portal.

2. **Scaling Resources**  
   - Adjust VM size based on processing needs.
   - Upgrade CPU, memory, or disk space if required.

3. **Performance Monitoring**  
   - Use Azure Monitor to track resource usage and set up alerts.

4. **Backup & Disaster Recovery**  
   - Configure Azure Backup for periodic snapshots.
   - Restore VMs from backups when needed.

5. **Security Best Practices**  
   - Keep OS and software updated.
   - Apply NSGs and Azure Firewall to restrict access.
   - Utilize Azure Bastion for secure SSH/RDP connections.

By following these guidelines, you can efficiently set up and manage Azure Virtual Machines, leveraging cloud computing for enhanced performance and scalability.
