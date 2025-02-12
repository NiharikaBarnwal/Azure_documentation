# Day 5: Capturing VM Images and Virtual Network (VNet) Deep Dive

## Table of Contents
1. [Capturing VM Images](#capturing-vm-images)
    - [Introduction](#introduction)
    - [Steps to Capture a VM Image](#steps-to-capture-a-vm-image)
2. [Virtual Network (VNet) Deep Dive](#virtual-network-vnet-deep-dive)
    - [Overview](#overview)
    - [Understanding Subnets](#understanding-subnets)
    - [Network Security Groups (NSGs)](#network-security-groups-nsgs)
    - [VNet Peering](#vnet-peering)
    - [Steps to Set Up and Configure VNets](#steps-to-set-up-and-configure-vnets)

## Capturing VM Images

### Introduction
Capturing a VM image in Azure enables the creation of a reusable template for deploying multiple VMs with the same configurations. This simplifies scaling and ensures uniformity across different environments.

### Steps to Capture a VM Image
1. **Access Azure Portal**: Open [Azure Portal](https://portal.azure.com).
2. **Navigate to Virtual Machines**: Use the search bar to find "Virtual Machines" and select it.
3. **Choose the Target VM**: Select the VM you wish to capture as an image.
4. **Deallocate the VM**: In the "Overview" section, click "Stop" to ensure it is in a deallocated state.
5. **Initiate Image Capture**:
    - Click on "Capture" on the VM’s page.
    - Fill in details such as the image name and resource group.
    - Optionally, choose to delete the original VM post-capture.
    - Click "Create" to generate the image.

## Virtual Network (VNet) Deep Dive

### Overview
A Virtual Network (VNet) in Azure is a foundational element that facilitates secure communication between Azure resources, the internet, and on-premises networks. It allows for flexible network architecture tailored to business needs.

### Understanding Subnets
Subnets divide a VNet into smaller logical segments, improving network organization and security.

#### Example:
A company can allocate different subnets for various departments like HR, IT, and Finance to isolate their traffic efficiently.

### Network Security Groups (NSGs)
NSGs provide rule-based traffic filtering for inbound and outbound connections within a VNet, enhancing security.

#### Example:
An NSG can be configured to permit HTTP and HTTPS traffic to web servers while blocking unauthorized access.

### VNet Peering
VNet Peering enables seamless communication between separate VNets, allowing them to function as a unified network without exposing traffic to the public internet.

#### Example:
Development and production environments in different VNets can be linked for resource sharing without compromising security.

### Steps to Set Up and Configure VNets

#### Creating a VNet
1. **Access Azure Portal**: Open [Azure Portal](https://portal.azure.com).
2. **Navigate to Virtual Networks**: Use the search bar to locate "Virtual Networks" and select it.
3. **Initiate VNet Creation**:
    - Click "Create" and enter necessary details:
      - **Name**: Assign a meaningful name.
      - **Address Space**: Define using CIDR notation (e.g., 10.0.0.0/16).
      - **Resource Group**: Select or create a resource group.
      - **Region**: Pick the appropriate Azure region.

4. **Configure Subnets**:
    - Click "Subnets" within the VNet setup.
    - Add a subnet, specifying its name and address range (e.g., 10.0.1.0/24).

5. **Complete VNet Creation**: Review configurations and click "Create."

---
This guide provides a concise yet thorough explanation of capturing VM images and a detailed breakdown of VNets, including subnets, NSGs, and VNet peering. The steps outlined facilitate easy setup and management in the Azure portal.

