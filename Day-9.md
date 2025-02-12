# Day 9: Understanding Network Security Groups (NSGs) in Azure

## Table of Contents
1. [Overview](#overview)
2. [Core Concepts](#core-concepts)
3. [NSG Components](#nsg-components)
4. [Traffic Flow Control](#traffic-flow-control)
5. [Role of Ports in NSGs](#role-of-ports-in-nsgs)
6. [Step-by-Step NSG Creation](#step-by-step-nsg-creation)
7. [Practical Scenarios](#practical-scenarios)
8. [Final Thoughts](#final-thoughts)

---

## Overview
Network Security Groups (NSGs) in Azure serve as essential security tools to control and filter network traffic to and from Azure resources. Acting as virtual firewalls, NSGs regulate access using predefined security rules that determine whether traffic is permitted or denied.

## Core Concepts
NSGs can be applied at different levels within Azure:
- **Network Interface Level**: Bound to a Virtual Machine's (VM) Network Interface Card (NIC) to control traffic specific to that VM.
- **Subnet Level**: Applied to an entire subnet, affecting all resources within it.
- **Stateful Mechanism**: Automatically allows return traffic for permitted inbound or outbound requests.
- **Rule Prioritization**: Rules are evaluated based on assigned priority numbers, where a lower number holds higher precedence.

## NSG Components
1. **Inbound Rules**: Define policies for incoming traffic.
2. **Outbound Rules**: Govern outgoing network traffic.
3. **Priority System**: Lower values have higher precedence in rule execution.
4. **Source & Destination Control**: Specifies permitted IP ranges.
5. **Protocol Specification**: Allows or denies traffic based on TCP, UDP, ICMP, or any protocol.
6. **Port Management**: Defines specific ports or port ranges for filtering.
7. **Action Assignment**: Rules enforce either 'Allow' or 'Deny' actions on traffic.

## Traffic Flow Control
### Inbound Rules
Manage incoming network requests to Azure resources:
- **Example**: Allow SSH (TCP, port 22) access to a VM from a specific IP range.
- **Key Factors**:
  - Source IP or IP range
  - Destination VM or subnet
  - Traffic protocol
  - Action (Allow/Deny)

### Outbound Rules
Regulate outgoing traffic from Azure resources:
- **Example**: Permit HTTP traffic (TCP, port 80) from a VM to the internet.
- **Key Factors**:
  - Source resource (VM or subnet)
  - Destination IP or domain
  - Port range
  - Protocol
  - Action (Allow/Deny)

## Role of Ports in NSGs
Ports serve as communication channels between applications and services:
- **Common Port Assignments**:
  - **80**: HTTP traffic
  - **443**: Secure HTTPS traffic
  - **22**: SSH access
  - **3389**: Remote Desktop Protocol (RDP)
- **Port Management in NSGs**:
  - Define access rules based on inbound or outbound needs.
  - Restrict unnecessary open ports to enhance security.

## Step-by-Step NSG Creation
1. **Create an NSG**:
   - Navigate to the Azure portal.
   - Select **Create a resource** and search for "Network Security Group".
   - Define NSG properties such as name and region.
   - Click **Create**.

2. **Configure Rules**:
   - Open the created NSG and navigate to **Inbound security rules** or **Outbound security rules**.
   - Click **Add** to create a new rule.
   - Define:
     - Priority (lower values = higher precedence)
     - Source and destination (IP ranges, subnets, or individual VMs)
     - Protocol (TCP/UDP/ICMP/Any)
     - Port range
     - Action (Allow/Deny)

3. **Associate NSG with a Resource**:
   - Attach NSG at either the **Subnet** or **VM NIC** level.
   - For **Subnet Level**:
     - Navigate to the subnet settings in Azure portal.
     - Assign the created NSG to enforce rules on all subnet resources.
   - For **VM NIC Level**:
     - Navigate to the VM's networking settings.
     - Attach the NSG to the NIC for resource-specific security.

## Practical Scenarios
### Scenario 1: Managing Inbound Traffic
- **Challenge**: Restrict SSH access to an Azure VM to only specific IPs.
- **Solution**: Define an inbound rule allowing TCP traffic on port 22 from a specific trusted IP range.

### Scenario 2: Controlling Outbound Traffic
- **Challenge**: Prevent a VM from accessing the internet while allowing internal communication.
- **Solution**: Create an outbound rule denying internet-bound traffic but allowing internal VNet communication.

### Scenario 3: Prioritizing Rules
- **Challenge**: Conflicting rules—one allowing HTTP traffic (priority 200) and another denying it (priority 100).
- **Solution**: The deny rule (lower priority number) takes precedence, blocking HTTP traffic.

### Scenario 4: Private and Public IP Interactions
- **Challenge**: Allow database VM (private IP) to be accessible from a jump server but not a public web server.
- **Solution**: Set inbound rules permitting access from the jump server while blocking the web server's private IP.

## Final Thoughts
Understanding and configuring NSGs effectively enhances security posture in Azure environments. By carefully defining inbound and outbound rules, utilizing proper prioritization, and managing ports, organizations can ensure robust network protection while maintaining operational efficiency.

---

This document provides a structured and refined approach to Network Security Groups in Azure, integrating security best practices and real-world applications.
