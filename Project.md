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

## Architecture Diagram -
![image](https://github.com/user-attachments/assets/1fb4a1fa-6c1c-41a5-a708-5722d28825dc)


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

### Code for app.py
   ```python
    from flask import Flask, request, jsonify, render_template
    import mysql.connector

    app = Flask(__name__)

    # Database connection
    db_connection = mysql.connector.connect(
        host="10.1.1.4",  # Replace with the actual private IP address of dbVM
        user="dbuser",
        password="dbpassword",
        database="user_data_db"  # Removed the trailing space
    )
    db_cursor = db_connection.cursor()

    @app.route('/')
    def home():
        return render_template('index.html')  # Render the index.html template

    @app.route('/register', methods=['POST'])
    def register():
        name = request.form['name']
        email = request.form['email']
        try:
            db_cursor.execute("INSERT INTO users (name, email) VALUES (%s, %s)", (name, email))
            db_connection.commit()
            return jsonify({"message": "Registration successful"}), 201
        except Exception as e:
            return jsonify({"error": str(e)}), 500

    @app.route('/get_users', methods=['GET'])
    def get_users():
        db_cursor.execute("SELECT * FROM users")
        users = db_cursor.fetchall()
        return jsonify(users), 200

    if __name__ == '__main__':
        app.run(host='0.0.0.0', port=80)
   ```

### code for index.html
   ```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registration Page</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(145deg, #f9f9f9, #e3e3e3);
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #333;
        }
        .container {
            background: #ffffff;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 450px;
            text-align: center;
            border: 2px solid #007bff;
            position: relative;
        }
        .container::before {
            content: "";
            position: absolute;
            top: -15px;
            left: 0;
            right: 0;
            height: 10px;
            background: linear-gradient(135deg, #007bff, #0056b3);
            border-radius: 12px 12px 0 0;
        }
        h1 {
            font-size: 32px;
            color: #007bff;
            margin-bottom: 20px;
            font-weight: 600;
        }
        form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        input[type="text"],
        input[type="email"] {
            padding: 14px;
            border-radius: 8px;
            border: 1px solid #ccc;
            font-size: 16px;
            transition: border 0.3s, box-shadow 0.3s;
            outline: none;
        }
        input[type="text"]:focus,
        input[type="email"]:focus {
            border-color: #007bff;
            box-shadow: 0 0 8px rgba(0, 123, 255, 0.2);
        }
        button {
            padding: 14px;
            border: none;
            border-radius: 8px;
            background-color: #007bff;
            color: #fff;
            font-size: 18px;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.2s;
        }
        button:hover {
            background-color: #0056b3;
            transform: translateY(-2px);
        }
        #show-users {
            background-color: #28a745;
            margin-top: 20px; /* Added space between buttons */
        }
        #show-users:hover {
            background-color: #218838;
        }
        .results {
            margin-top: 30px;
            border-radius: 12px;
            padding: 20px;
        }
        .results table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            margin-top: 10px;
        }
        .results th, .results td {
            padding: 12px;
            text-align: left;
            font-size: 16px;
            color: #555;
        }
        .results th {
            background: #007bff;
            color: #fff;
            border-top-left-radius: 12px;
            border-top-right-radius: 12px;
        }
        .results tr:nth-child(even) {
            background: #f1f1f1;
        }
        .results tr:nth-child(odd) {
            background: #ffffff;
        }
        .results tr:hover {
            background: #e9ecef;
        }
        .results td:first-child {
            border-left: 1px solid #ddd;
        }
        .results td:last-child {
            border-right: 1px solid #ddd;
        }
        .results table, .results th, .results td {
            border: 1px solid #ddd;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Register</h1>
        <form id="registration-form" action="/register" method="post">
            <input type="text" name="name" placeholder="Enter your name" required>
            <input type="email" name="email" placeholder="Enter your email" required>
            <button type="submit">Register</button>
        </form>
        <button id="show-users" type="button">Show All Users</button>
        <div class="results" id="results">
            <!-- User data will be displayed here -->
        </div>
    </div>

    <script>
        document.getElementById('show-users').addEventListener('click', function() {
            fetch('/get_users')
                .then(response => response.json())
                .then(data => {
                    const resultsDiv = document.getElementById('results');
                    resultsDiv.innerHTML = '';
                    
                    if (data.length === 0) {
                        resultsDiv.innerHTML = '<p>No users found.</p>';
                        return;
                    }

                    const table = document.createElement('table');
                    const thead = document.createElement('thead');
                    const tbody = document.createElement('tbody');

                    // Create table header
                    const headerRow = document.createElement('tr');
                    const nameHeader = document.createElement('th');
                    nameHeader.textContent = 'Name';
                    const emailHeader = document.createElement('th');
                    emailHeader.textContent = 'Email';
                    headerRow.appendChild(nameHeader);
                    headerRow.appendChild(emailHeader);
                    thead.appendChild(headerRow);
                    
                    // Populate table body with user data
                    data.forEach(user => {
                        const row = document.createElement('tr');
                        const nameCell = document.createElement('td');
                        nameCell.textContent = user[1]; // Assuming the order: id, name, email
                        const emailCell = document.createElement('td');
                        emailCell.textContent = user[2];
                        row.appendChild(nameCell);
                        row.appendChild(emailCell);
                        tbody.appendChild(row);
                    });

                    table.appendChild(thead);
                    table.appendChild(tbody);
                    resultsDiv.appendChild(table);
                })
                .catch(error => {
                    console.error('Error fetching users:', error);
                });
        });
    </script>
</body>
</html>
   ```

## Summary

In this Azure project, we're setting up a well-organized and secure application environment. We create separate virtual networks for the frontend and backend, then deploy virtual machines to host each part. To manage and secure access, we use a jump server, and a load balancer with a public IP handles traffic to the frontend, with autoscaling to adjust to varying demands. We ensure secure connections with VPNs and deploy the app with Azure Hosting services, linking it to a domain with SSL encryption for added security. The whole setup follows industry best practices to keep everything reliable, scalable, and compliant.
