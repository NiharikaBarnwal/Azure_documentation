# Day 4: Azure Storage and IP Addressing

## Table of Contents
1. [Azure Disk Storage](#azure-disk-storage)
   - [Introduction](#introduction)
   - [Types of Azure Disks](#types-of-azure-disks)
   - [Creating an Azure Disk](#creating-an-azure-disk)
2. [Dynamic IP Address](#dynamic-ip-address)
   - [What is a Dynamic IP?](#what-is-a-dynamic-ip)
   - [Advantages of Dynamic IPs](#advantages-of-dynamic-ips)
   - [How to Assign a Dynamic IP in Azure](#how-to-assign-a-dynamic-ip-in-azure)
3. [Static IP Address](#static-ip-address)
   - [What is a Static IP?](#what-is-a-static-ip)
   - [Advantages of Static IPs](#advantages-of-static-ips)
   - [How to Assign a Static IP in Azure](#how-to-assign-a-static-ip-in-azure)

---

## Azure Disk Storage

### Introduction
Azure Disk Storage provides high-performance and durable block storage for Azure Virtual Machines (VMs). These disks cater to various workloads by offering different levels of performance and scalability.

### Types of Azure Disks
1. **Standard HDD** - Cost-effective storage for workloads with minimal performance requirements.
2. **Standard SSD** - Better performance and lower latency compared to Standard HDDs.
3. **Premium SSD** - Designed for high-speed and low-latency applications.
4. **Ultra Disk** - Best suited for high-performance computing and data-heavy workloads.

### Creating an Azure Disk
1. **Access the Azure Portal**: Log in to [Azure Portal](https://portal.azure.com).
2. **Navigate to Disks**: Use the search bar to find and select "Disks."
3. **Create a New Disk**: Click on "Create" and enter the required details (name, resource group, region, and disk type).
4. **Attach to a Virtual Machine**: Go to your VM’s "Disks" section and add the newly created disk as a data disk.

---

## Dynamic IP Address

### What is a Dynamic IP?
A Dynamic IP is an IP address that changes each time a VM restarts. Azure dynamically assigns it from a pool of available IP addresses.

### Advantages of Dynamic IPs
- **Cost Savings** - No additional cost as it's automatically assigned by Azure.
- **Efficient Resource Allocation** - Ideal for temporary workloads that do not require a fixed IP.

### How to Assign a Dynamic IP in Azure
1. **Log into the Azure Portal**: Open [Azure Portal](https://portal.azure.com).
2. **Go to Virtual Machines**: Search and select "Virtual Machines."
3. **Select a VM**: Choose the VM for which you want to configure the IP.
4. **Modify Networking Settings**: Navigate to "Networking."
5. **IP Configuration**: Select the network interface’s IP configuration.
6. **Change Assignment Type**: Ensure the assignment is set to "Dynamic."
7. **Apply Changes**: Save your configuration.

---

## Static IP Address

### What is a Static IP?
A Static IP is an IP address that remains fixed, even after VM restarts. It is reserved specifically for your resource unless manually released.

### Advantages of Static IPs
- **Persistent Connectivity** - Useful for DNS records and firewall settings that require a constant IP.
- **Reliable Access** - Ensures a consistent address for applications needing a fixed endpoint.

### How to Assign a Static IP in Azure
1. **Log into the Azure Portal**: Open [Azure Portal](https://portal.azure.com).
2. **Go to Virtual Machines**: Search and select "Virtual Machines."
3. **Select a VM**: Choose the VM that requires a static IP.
4. **Modify Networking Settings**: Navigate to "Networking."
5. **IP Configuration**: Select the network interface’s IP configuration.
6. **Change Assignment Type**: Switch the assignment to "Static."
7. **Enter Desired IP**: Specify the static IP you want to assign.
8. **Save Changes**: Apply the configuration.

---

This guide provides a clear understanding of Azure Disks, Dynamic IPs, and Static IPs, along with step-by-step instructions for configuration. By following these instructions, you can effectively manage storage and networking in Azure.
