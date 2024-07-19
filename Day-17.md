### Day-17 (18-07-2024)

**Topics Covered:**
- Application Gateway
- Azure Active Directory

---

### Application Gateway

**Application Gateway** in Azure acts as a web traffic load balancer, providing various capabilities to manage traffic to your web applications. One key feature is its ability to filter out bot attacks using Web Application Firewall (WAF), as bots typically share the same IP.

#### Types of Application Gateway:
1. **Standard V1 (LB)**: Basic load balancing.
2. **Standard V2 (LB+AS)**: Load balancing with auto-scaling.
3. **WAF V1 (LB+WAF)**: Load balancing with WAF.
4. **WAF V2 (LB+AS+WAF)**: Load balancing, auto-scaling, and WAF.

**Abbreviations**:
- **WAF**: Web Application Firewall
- **LB**: Load Balancing
- **AS**: Auto-scaling

#### Features:
1. **Cookie-based Affinity**: Ensures that a user is always served by the same VM.
2. **Connection Draining**: Allows VMs to be safely removed from the load balancer for maintenance without disrupting active connections.
3. **Multi-site Hosting**: Enables hosting of multiple websites, each with its own domain name, on the same Application Gateway.
4. **SSL Offloading**: Offloads SSL decryption/encryption to the Application Gateway, reducing the workload on backend servers.
5. **HTTP to HTTPS Rerouting**: Automatically redirects HTTP traffic to HTTPS for enhanced security.

#### Steps to Set Up an Application Gateway:
1. **Create a Resource Group (RG)**:
   - Name it `AG-RG`.
2. **Create a Virtual Network (VNet)**:
   - Name it `AG-VNET` with two subnets: `Vm-Subnet` and `Gateway-Subnet`.
3. **Create Two Ubuntu VMs**:
   - Name them `VM-1` and `VM-2` in `Vm-Subnet`.
   - Allow all ports.
   - Configure both VMs as web servers.
     - If `apache2` is not working, use the following commands:
       ```sh
       systemctl enable apache2
       systemctl start apache2
       systemctl status apache2
       ```
4. **Create the Application Gateway**:
   - Select `Standard V2` for the tier.
   - Set minimum and maximum instance count to 1 and 10, respectively.
   - Create a frontend pool.
   - Add a backend pool:
     - Select "No" for adding a backend pool without targets.
     - Select VMs.
   - Add a routing rule:
     - In the backend settings, give a name.

```
+---------------------+
| Application Gateway |
|  +---------------+  |
|  | Frontend Pool |  |
|  +-------+-------+  |
|          |          |
|  +-------+-------+  |
|  | Backend Pool  |  |
|  +-------+-------+  |
|  |   VM-1        |  |
|  |   VM-2        |  |
+---------------------+
```

---

### Azure Active Directory (AD)

**Azure Active Directory** (AD) is a cloud-based identity and access management service that helps employees sign in and access resources. It is utilized by system administrators to manage user identities and secure access to resources.

#### Features:
- **Centralized Authentication**: Stores authentication details centrally.
- **User Management**: Manages usernames, file sharing, printing, and other administrative tasks.
- **Centralized Administration**: All devices are connected to a central AD Domain Services (ADDS) server.

#### Steps to Set Up Azure AD:
1. **Create a Resource Group (RG)**:
   - Name it `AG-RG`.
2. **Create a Windows VM**:
   - Set up the VM as required.
3. **Access the VM**:
   - Connect to the VM using Remote Desktop Protocol (RDP).
4. **Install ADDS**:
   - Go to "Roles and Features" and add Active Directory Domain Services (ADDS).
5. **Configure the Domain**:
   - Go to the File Explorer and add a domain part.
   - Follow the installation steps.
   - The VM will reboot; reconnect after the reboot.
6. **Create Users and Organizational Units**:
   - Go to "Tools" at the top right corner.
   - Select "Active Directory Users and Computers".
   - Navigate to the domain name, right-click, and create a new organizational unit.
   - Right-click on the new organizational unit, select "New", and then "User".
   - Add user details.

```
+---------------------+
|     Azure AD        |
|  +---------------+  |
|  |  Users        |  |
|  +-------+-------+  |
|          |          |
|  +-------+-------+  |
|  |  Devices      |  |
|  +---------------+  |
+---------------------+
```
---

These steps will help to set up and manage an Application Gateway and Azure Active Directory effectively, leveraging their full capabilities for enhanced security and performance.
