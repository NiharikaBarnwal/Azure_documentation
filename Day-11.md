### Day-11 (10-07-2024)

---

#### Network Security Group (NSG)

**NSG Attachment:**
- **NSG can be attached at two levels:**
  - **VM Level:** Directly attached to the Network Interface Card (NIC) of a VM.
  - **Subnet Level:** Applied to all VMs within the subnet.

**NSG and NIC Relationship:**
- **NSG is attached to NIC:** The NIC is then attached to the VM.
- **Single NIC:** A single NIC can be attached to only one VM at a time, but a VM can have multiple NICs.

**Examples:**
- **VM Level:** An NSG attached to a NIC of a VM controls inbound and outbound traffic for that specific VM.
- **Subnet Level:** An NSG applied to a subnet controls traffic for all VMs within that subnet.

**Detailed Example:**

1. **VM Level NSG:**
   - **Scenario:** You have a VM hosting a web application that should only be accessible via HTTP (port 80) and HTTPS (port 443) but needs to block all other traffic.
   - **Steps:**
     1. Create an NSG.
     2. Add inbound security rules to allow traffic on ports 80 and 443.
     3. Attach the NSG to the NIC of the VM.
  
2. **Subnet Level NSG:**
   - **Scenario:** You have a subnet with multiple VMs, and you want to apply a uniform security policy that allows only SSH (port 22) and RDP (port 3389) traffic.
   - **Steps:**
     1. Create an NSG.
     2. Add inbound security rules to allow traffic on ports 22 and 3389.
     3. Attach the NSG to the subnet.

**Diagram:**

```plaintext
+------------------------------------------+          +------------------------------------------+      
|       Subnet                             |          |       Subnet                             |
|  +---------------+    +---------------+  |          |  +---------------+                       |
|  |     NSG       |    |     NSG       |  |          |  |      VM  1    |----------+            |
|  +-------+-------+    +-------+-------+  |          |  +-------+-------+          |            |
|          |                    |          |          |                             |            |
|  +-------+-------+    +-------+-------+  |          |  +-------+-------+          |            |     +---------------+     +---------------+
|  |      NIC      |    |      NIC      |  |          |  |      VM  2    |----------+------------|-----|       NIC     |-----|       NSG     |
|  +-------+-------+    +-------+-------+  |          |  +-------+-------+          |            |     +-------+-------+     +-------+-------+
|          |                    |          |          |                             |            |
|  +-------+-------+    +-------+-------+  |          |  +-------+-------+          |            |
|  |      VM  1    |    |      VM  2    |  |          |  |      VM  3    |----------+            |
|  +---------------+    +---------------+  |          |  +---------------+                       |
+------------------------------------------+          +------------------------------------------+
                 VM level                                                                Subnet level

```

---

#### Standard Load Balancer (LB)

**Requirements:**
- **VM SKU:** The VMs must have a Standard SKU.
- **Static IP:** The VMs must have a static IP address.

**Example:**
- **Standard SKU:** VMs with Standard_D2s_v3 SKU.
- **Static IP:** Assigning a static IP to each VM to ensure consistent network configuration.

**Detailed Example:**

1. **Standard Load Balancer Setup:**
   - **Scenario:** You want to set up a load balancer to distribute HTTP traffic across multiple VMs hosting a web application.
   - **Steps:**
     1. Ensure all VMs have a Standard SKU and static IP addresses.
     2. Create a Standard Load Balancer.
     3. Configure a frontend IP configuration for the load balancer.
     4. Define a backend pool consisting of the VMs.
     5. Set up health probes to monitor the status of VMs.
     6. Create load balancing rules to distribute traffic on port 80.

**Diagram:**

```plaintext
                            +---------------------+
                            |    Load Balancer    |
                            |    (Public IP)      |
                            +---------+-----------+
                                      |
                    +-----------------+-----------------+
                    |                                   |
             +------+-----+                     +-------+-----+
             |    VM 1    |                     |    VM 2     |
             | (Standard  |                     | (Standard   |
             |    SKU,    |                     |    SKU,     |
             |  Static IP)|                     |  Static IP) |
             +------------+                     +-------------+
```

---

**Notes:**

- **NSG Rules:**
  - **Inbound Security Rules:** Define the allowed inbound traffic. Example: Allow HTTP (port 80) and HTTPS (port 443) traffic.
  - **Outbound Security Rules:** Define the allowed outbound traffic. Example: Allow all outbound internet traffic.

- **NSG Best Practices:**
  - **Least Privilege Principle:** Only allow the necessary ports and IP ranges.
  - **Monitoring:** Use Azure Monitor and Network Watcher to monitor NSG traffic.

- **Standard Load Balancer Features:**
  - **High Availability:** Distributes traffic across multiple VMs for reliability.
  - **Health Probes:** Continuously checks the status of VMs to ensure traffic is only sent to healthy instances.
  - **Cross-Zone Load Balancing:** Distributes traffic across VMs in different availability zones for higher resilience.

---

By understanding and properly configuring NSGs and Standard Load Balancers, you can significantly enhance the security and reliability of your Azure infrastructure.
