# Day 8: Azure Site-to-Site VPN and Azure IPs

## Table of Contents

1. [Overview](#overview)
2. [Understanding Site-to-Site (S2S) VPN in Azure](#understanding-site-to-site-s2s-vpn-in-azure)
   - [Working Mechanism](#working-mechanism)
   - [Essential Components](#essential-components)
   - [Use Case: Office Network Connection](#use-case-office-network-connection)
   - [Use Case: Home Network Connection](#use-case-home-network-connection)
   - [Comparison: P2S vs S2S VPN](#comparison-p2s-vs-s2s-vpn)
3. [IP Address Classification](#ip-address-classification)
   - [Fixed IP Address](#fixed-ip-address)
   - [Flexible IP Address](#flexible-ip-address)
4. [Azure SKU Types](#azure-sku-types)
   - [Definition and Significance](#definition-and-significance)
   - [Standard SKU](#standard-sku)
   - [Basic SKU](#basic-sku)
5. [IPv4 vs IPv6](#ipv4-vs-ipv6)
   - [IPv4 Fundamentals](#ipv4-fundamentals)
   - [IPv6 Innovations](#ipv6-innovations)
   - [Migration and Compatibility](#migration-and-compatibility)
6. [Azure Public IPs](#azure-public-ips)
   - [Regional Public IP](#regional-public-ip)
   - [Global Public IP](#global-public-ip)
   - [Real-World Applications](#real-world-applications)

## Overview

This guide explores Azure’s Site-to-Site (S2S) VPN setup, various IP address types, SKU classifications, and the transition from IPv4 to IPv6. It also explains different Azure public IP configurations and their applications.

## Understanding Site-to-Site (S2S) VPN in Azure

A Site-to-Site (S2S) VPN facilitates a secure, continuous link between an on-premises network and an Azure Virtual Network (VNet). It is commonly employed in hybrid cloud scenarios to integrate corporate resources seamlessly.

### Working Mechanism

- **Always-On Connection:** S2S VPN remains active without requiring manual initiation.
- **Gateway-Enabled Communication:** A dedicated VPN gateway establishes secure tunnels between networks.
- **Encryption for Security:** Data transmitted across the tunnel is encrypted to ensure confidentiality.

### Essential Components

- **Corporate VPN Device:** An on-premises firewall or VPN appliance that connects to Azure.
- **Azure VPN Gateway:** The entry point for network traffic within the Azure VNet.

### Use Case: Office Network Connection

#### Scenario
A company, "CloudWorks," operates an internal office network that needs secure access to Azure-hosted resources like databases and virtual machines.

#### Implementation Steps

1. **Deploy a VNet in Azure**
   - Define an address range (e.g., 10.2.0.0/16) and relevant subnets.

2. **Set Up an Azure VPN Gateway**
   - Attach the gateway to the Azure VNet and configure a public IP.

3. **Define a Local Network Gateway**
   - Register the office network's IP range (e.g., 192.168.2.0/24) and its VPN device’s public IP.

4. **Establish the VPN Connection**
   - Secure the link using a pre-shared key and IPsec/IKE configurations.

5. **Configure On-Premises VPN Device**
   - Match the Azure VPN Gateway settings on the office firewall/router.

6. **Verify Connectivity**
   - Test access to Azure-hosted resources from the corporate network.

### Comparison: P2S vs S2S VPN

| Feature | Point-to-Site (P2S) | Site-to-Site (S2S) |
|---------|---------------------|---------------------|
| Connection Type | Individual client to Azure | Entire network to Azure |
| Usage | Remote workers | Office-to-cloud connectivity |
| Scalability | Limited to users | Suitable for enterprise-wide use |
| Tunnel Type | SSL VPN | IPsec VPN |

## IP Address Classification

### Fixed IP Address
A manually assigned IP address that remains unchanged unless modified by an administrator.

### Flexible IP Address
A dynamically assigned IP that can change over time, managed by a DHCP server.

## Azure SKU Types

### Definition and Significance
Azure SKUs (Stock Keeping Units) define performance levels and pricing for Azure resources.

### Standard SKU
- Offers enhanced security, availability, and scalability.
- Recommended for production and mission-critical workloads.

### Basic SKU
- Provides cost-effective solutions with fundamental features.
- Ideal for testing and development environments.

## IPv4 vs IPv6

### IPv4 Fundamentals
- Uses 32-bit addressing, allowing ~4.3 billion unique IPs.
- Example: 192.168.0.1
- Experiencing address exhaustion due to increasing demand.

### IPv6 Innovations
- Implements 128-bit addresses, vastly expanding available IPs.
- Example: 2001:db8::ff00:42:8329
- Enhances routing efficiency and security.

### Migration and Compatibility
- **Dual Stack:** Supports both IPv4 and IPv6 simultaneously.
- **Tunneling:** Encapsulates IPv6 traffic within IPv4 packets.
- **Translation:** Enables direct communication between different protocols.

## Azure Public IPs

Azure assigns public IPs to resources based on network requirements.

### Regional Public IP
- Tied to a specific Azure region.
- Suitable for applications restricted to a single region.

### Global Public IP
- Not bound to any region.
- Facilitates worldwide access across multiple regions.

### Real-World Applications

| Scenario | Recommended IP Type |
|----------|--------------------|
| Web application with regional access | Regional Public IP |
| Global content delivery system | Global Public IP |
| Database access within a single region | Regional Public IP |

---

## Configuring S2S VPN and Azure Public IPs

### Setting Up a Site-to-Site VPN

1. **Create a VNet** in the Azure portal and assign an address range.
2. **Deploy a Virtual Network Gateway** with a chosen SKU (e.g., VpnGw1).
3. **Register a Local Network Gateway** with the on-premises network’s details.
4. **Establish a VPN Connection** by linking the VPN Gateway and Local Network Gateway.
5. **Configure the On-Premises Firewall/Router** to match Azure's VPN settings.
6. **Verify Tunnel Status** using Azure’s network monitoring tools.

### Assigning an Azure Public IP

1. **Navigate to Public IP Addresses** in the Azure portal.
2. **Create a New Public IP**, specifying its SKU (Basic or Standard) and type (Static or Dynamic).
3. **Associate the Public IP** with a virtual machine, load balancer, or other Azure resource.
4. **Validate the Configuration** to ensure external accessibility.

---

This document provides a structured approach to setting up a Site-to-Site VPN, differentiating between IP address types, understanding SKU levels, and configuring public IPs in Azure.

