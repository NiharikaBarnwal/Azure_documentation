# Internship Final Project

## Aim of the Project
1. Create separate virtual networks for a database (backend) and frontend of the application.
2. Deploy Virtual Machines (VMs) for hosting the front end of the application and database.
3. Connect the setup with a jump VM or server to make changes to the frontend or backend.
4. Apply a load balancer to the frontend servers in the frontend network and attach a public IP to the load balancer only.
5. Enable auto-scaling to manage traffic efficiently.
6. Connect to the VMs through a private path set up by the jump servers using VPN.
7. Deploy the application with Azure Hosting service and map the public IP of the load balancer to the domain name.
8. Perform operations from the frontend as a general user and check the results in the database.
9. Apply an SSL certificate to the domain while it is hosted.

## Steps Followed

### Step 1: Create a Resource Group

- **Name:** Project-RG
- **Region:** Central India

### Step 2: Create Separate Virtual Networks

1. **Frontend VNet Creation:**
    - Create a Virtual Network (VNet) for the frontend, named `frontend-vnet`.
    - Within this VNet, create two subnets:
        - **Public Subnet:** For the Jump VM, which will allow SSH access.
        - **Private Subnet:** For the frontend VMs, which will host the application.
    - Create a Gateway Subnet for establishing the VPN connection.

2. **Backend VNet Creation:**
    - Create a Virtual Network (VNet) for the backend, named `backend-vnet`.
    - Within this VNet, create one subnet:
        - **Private Subnet:** For the backend VMs that will host the database.
    - Create a Gateway Subnet for establishing the VPN connection.

### Step 3: Establish VPN Connection

1. **Set Up Virtual Network Gateways:**
    - Deploy Virtual Network Gateways in both `frontend-vnet` and `backend-vnet`.
    - Establish a VNet-to-VNet VPN connection between these gateways to enable secure communication between the frontend and backend.

2. **Configure the Jump VM:**
    - Use the Jump VM to access the VMs via the VPN tunnel, ensuring secure administration.

### Step 4: Deploy Virtual Machines

1. **Deploy Frontend VMs:**
    - Deploy virtual machines in the Private Subnet of the `frontend-vnet`.
    - Ensure these VMs are properly configured to host the frontend application.

2. **Deploy Backend VM:**
    - Deploy a virtual machine in the Private Subnet of the `backend-vnet`.
    - This VM will host the database for the application.
    - Add an Inbound rule with:
        - **Source:** IP addresses
        - **Source IP address:** Frontend-VM private IP
        - **Source port:** *
        - **Destination:** Any
        - **Service:** MySQL
        - **Destination port:** 3306

3. **Deploy Jump VM:**
    - Deploy a Jump VM in the Public Subnet of the `frontend-vnet`.
    - This VM will be used to access both frontend and backend VMs securely.

### Step 5: Configure the Backend VM
    
  - Connect to the jump-vm using SSH.
  - Connect to the backend-vm using its private IP.
  - Connect to the root user (`sudo su`, then `cd`).
  - Run the following commands:
      ```bash
      apt update
      apt install mysql-server -y
      sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
      ```
    - Change the `bind-address` to `0.0.0.0`.
  - Allow MySQL traffic on port 3306:
      ```bash
      sudo ufw allow 3306
      ```
  - Set up MySQL:
      ```bash
      sudo mysql -u root -p   #(Enter a password)
      ```
      ```mysql
      CREATE DATABASE userdata_db;
      CREATE USER 'dbuser' IDENTIFIED BY 'dbpassword';
      GRANT ALL PRIVILEGES ON userdata_db.* TO 'dbuser';
      FLUSH PRIVILEGES;
      USE userdata_db;
      CREATE TABLE users (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255) NOT NULL, email VARCHAR(255) NOT NULL);
      SELECT host, user FROM mysql.user WHERE user = 'dbuser';
      ```
  - Ensure `%` is listed under the host, and grant the necessary permissions if not.
    - Check UFW status and enable necessary rules:
      ```bash
      sudo ufw status
      sudo ufw enable
      sudo ufw allow ssh
      sudo ufw allow 22/tcp
      sudo ufw allow http
      sudo ufw allow 80/tcp
      sudo systemctl restart mysql
      ```

### Step 6: Configure the Frontend VM

  - Connect to jump-vm using SSH.
  - Connect to frontend-vm using its private IP.
  - Connect to the root user (`sudo su`, then `cd`).
  - Run the following commands:
      ```bash
      apt update
      sudo apt-get install python3-pip -y
      sudo apt install python3.12-venv
      python3 -m venv myenv
      source myenv/bin/activate
      pip3 install flask mysql-connector-python
      sudo apt install apache2 -y
      sudo apt install mysql-client-core-8.0
      mkdir -p ~/myflaskapp
      cd ~/myflaskapp
      ```
  - Create `app.py` and `templates/index.html` files.
  - If port 80 is occupied:
      ```bash
      sudo lsof -i :80
      sudo kill <PID>
      ```
  - Run the following commands:
      ```bash
      sudo systemctl stop apache2
      sudo systemctl disable apache2
      python3 app.py
      ```

### Step 7: Apply Load Balancer

1. **Set Up Load Balancer:**
    - Deploy a Load Balancer in the `frontend-vnet`.
    - Configure the Load Balancer with a Frontend IP (Public IP) and Backend Pool consisting of the frontend VMs.

2. **Attach Public IP:**
    - Ensure the Load Balancer has a Public IP address assigned to handle traffic from external users.
    - Use this IP to access the hosted website.

### Step 8: Create a DNS Zone

1. **Purchase a Domain Name:** Purchase from a Domain Registry.
2. **Create a DNS Zone:** Fill in the required details and accept default settings.
3. **Manage Domain:**
    - Go to the domain registry and manage the domain.
    - Add the 4 name servers generated by Azure (remove the last dot in each name server).
4. **Add Recordsets:**
    - Paste the IP of the VM.
    - Add other details (e.g., names like www, app, etc.).
5. **Access the Hosted Website:** Go to this domain name and view the hosted website.

### Step 9: Enable Autoscaling

1. **Configure Autoscaling:**
    - Enable autoscaling for the frontend VMs in the Load Balancer's backend pool.
    - Set rules for scaling based on CPU usage or other metrics to handle traffic efficiently.

## Summary

In this Azure project, we're setting up a well-organized and secure application environment. We create separate virtual networks for the frontend and backend, then deploy virtual machines to host each part. To manage and secure access, we use a jump server, and a load balancer with a public IP handles traffic to the frontend, with autoscaling to adjust to varying demands. We ensure secure connections with VPNs and deploy the app with Azure Hosting services, linking it to a domain with SSL encryption for added security. The whole setup follows industry best practices to keep everything reliable, scalable, and compliant.