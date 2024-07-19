## Day-10 (08-07-2024) : Azure Basic Load Balancer

### Table of Content:-
- [Load_Balancer](#load-balancer)
- [Terminologies](#terminologies)
- [Types](#load-balancer-types)
- [Additional_Details](#additional-details)
- [Diagram](#diagram)
---

#### Load Balancer

When there is traffic on a server, two scaling methods are used to manage the load:
- **Increasing VM Size (Vertical Scaling)**:
   - Upgrading the existing VM to a larger size with more resources (CPU, memory, etc.).
   - Example: Upgrading a VM from Standard_D2s_v3 (2 vCPUs, 8 GB RAM) to Standard_D4s_v3 (4 vCPUs, 16 GB RAM) to handle more load.
- **Replicating VM (Horizontal Scaling)**:
  - Adding more VMs to distribute the load.
  - Example: Deploying additional instances of a web server to handle increased user requests during a sale event.

**Replication is done using a Load Balancer (LB)**. It distributes the traffic among the VMs. The LB has a public IP, allowing all VMs to be accessed from this common IP using different ports.

```plaintext

      Backend Pool
     +-----------------------------------------------------------+
     |    Availability Set                                       |
     |   +---------------------------------------------------+   |
     |   |   +-----------+   +-----------+   +-----------+   |   |
     |   |   |    VM 1   |   |    VM 2   |   |    VM 3   |   |   |
     |   |   +-----------+   +-----------+   +-----------+   |   |
     |   +---------------------------------------------------+   |
     +-----------------------------+-----------------------------+
                                   |
                                   |
                     +-------------+-----------+                 +-----------------+    Hit Public IP
                     |     LOAD BALANCER       | <-------------> |  Frontend Pool  | <----------------- User/Client
                     +-------------------------+                 +-----------------+

```

---

### Terminologies:
- **Scale Out**: Increasing the number of VMs.
  - **Example**: Adding more VMs to handle increased traffic during peak hours.
- **Scale In**: Decreasing the number of VMs.
  - **Example**: Reducing the number of VMs during off-peak hours to save costs.
- **Internet Facing**: If internet traffic is involved, a Public Load Balancer (PLB) is used.
  - **Example**: A web application accessible to users over the internet.
- **Internal Facing**: If internal traffic is involved, a Private Load Balancer (ILB) is used.
  - **Example**: An internal application used within an organization's network.

### Load Balancer Types:
- **Public Load Balancer (PLB)**: Distributes incoming internet traffic to VMs.
  - **Example**: A website hosted on multiple VMs behind a PLB.
- **Private Load Balancer (ILB)**: Distributes traffic within a virtual network.
  - **Example**: An internal business application used by employees.

---

#### Additional Details

**Health Probes:** Load balancers use health probes to check the availability of VMs. If a VM is down, the load balancer stops sending traffic to it.
- **Example**: HTTP health probe checks if the web server on a VM returns a 200 OK response.

**Load Balancing Rules:** Define how traffic is distributed based on ports and protocols.
- **Example**: A rule that distributes HTTP traffic (port 80) among all VMs.

**Session Persistence:** Ensures that a user's session is consistently routed to the same VM.
- **Example**: A user shopping on an e-commerce site continues to interact with the same VM during their session.

---

#### Diagram

Here's an enhanced diagram to illustrate the Load Balancer and scaling methods:

```plaintext
                  +---------------------+
                  |     Load Balancer   |
                  |     (Public IP)     |
                  +---------+-----------+
                            |
          +-----------------+-----------------+
          |                 |                 |
  +-------+-------+ +-------+-------+ +-------+-------+
  |      VM 1     | |      VM 2     | |      VM 3     |
  | (Web Server)  | | (Web Server)  | | (Web Server)  |
  +-------+-------+ +-------+-------+ +-------+-------+
          |                 |                 |
  +-------+-------+ +-------+-------+ +-------+-------+
  |   Health      | |   Health      | |   Health      |
  |   Probe       | |   Probe       | |   Probe       |
  +---------------+ +---------------+ +---------------+

Vertical Scaling: Increase VM size (e.g., VM 1 -> Larger VM)
Horizontal Scaling: Add more VMs (e.g., VM 4, VM 5)
```

---

This diagram includes the health probes associated with each VM to indicate the health monitoring aspect of load balancing. This ensures that only healthy VMs receive traffic, maintaining high availability and reliability of the services.
