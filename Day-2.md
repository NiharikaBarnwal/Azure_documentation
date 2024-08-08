# Day-2 (29-06-2024) : Introduction to Networking, Networking Devices, and Best Industry Practices

## Table of Contents
- [Introduction to Networking](#introduction-to-networking)
- [Cloud Service Providers](#cloud-service-providers)
- [Network Service Providers](#network-service-providers)
- [Benefits of Networking](#benefits-of-networking)
- [Networking Devices](#networking-devices)
  - [Hub](#hub)
  - [Switch](#switch)
  - [Router](#router)
  - [Amplifier](#amplifier)
- [Network Protocols](#network-protocols)
  - [TCP/IP Protocol](#tcpip-protocol)
  - [UDP Protocol](#udp-protocol)
- [Azure vs AWS](#azure-vs-aws)
- [Security Considerations](#security-considerations)
  - [RFP (Request for Proposal)](#rfp-request-for-proposal)
  - [Compliance and Regulations](#compliance-and-regulations)
  - [Data Security (Data at Rest and Data in Transit)](#data-security-data-at-rest-and-data-in-transit)
  - [PCIDSS Compliance](#pcidss-compliance)

## Introduction to Networking

When two or more resources are connected with each other to share resources such as data, hardware, and software, it is said to be in a network. Networking allows efficient communication and resource management across various devices.

## Cloud Service Providers

Cloud service providers offer a variety of services like computing power, storage, databases, and networking over the internet. These providers ensure connectivity through technologies such as fiber optics, satellite communication, and mobile networks. Examples include:

- **AWS (Amazon Web Services)**
- **Azure (Microsoft Azure)**
- **GCP (Google Cloud Platform)**

## Network Service Providers

Network service providers supply bandwidth, volume, and speed for data transfer, enabling internet and communication services. Examples include:

- **Jio**
- **Airtel**
- **Idea**

## Benefits of Networking

Networking offers several advantages, including:

- **Cost Savings**: By sharing resources like printers, files, and internet connections, costs can be reduced.
- **Resource Sharing**: Facilitates the sharing of resources among multiple users.

## Networking Devices

### Hub

- **Hub**: A broadcasting device that connects multiple computers. It is a non-intelligent device that sends data to all connected devices, regardless of the destination.

#### Characteristics:
- **Single Collision Domain**: All devices share the same collision domain, leading to potential data collisions.
- **Privacy Concern**: Since data is broadcasted to all devices, there is no privacy.

### Switch

- **Switch**: An intelligent device that connects multiple computers in a network, ensuring that data is sent only to the intended recipient.

#### Characteristics:
- **Multi Collision Domain**: Each connected device has its own collision domain, reducing data collisions.
- **Privacy**: Data is sent only to the intended device, enhancing privacy.

### Router

- **Router**: A device that connects multiple networks and directs data packets between them. Routers are essential for internet connectivity and managing traffic between networks.

### Amplifier

- **Amplifier**: A device used to strengthen signals in a network, ensuring that data can travel over longer distances without degradation.

## Network Protocols

Protocols are sets of rules that ensure proper communication between devices in a network.

### TCP/IP Protocol

- **TCP (Transmission Control Protocol)**: Breaks down a message into smaller packets before transmission. These packets are sent independently and reassembled at the destination.
- **IP (Internet Protocol)**: Handles addressing and routing of packets to ensure they reach the correct destination.

#### Example:
When you send an email, TCP breaks it down into packets, and IP ensures each packet is delivered to the recipient's server, where TCP reassembles the email.

### UDP Protocol

- **UDP (User Datagram Protocol)**: Sends the entire message as a single packet without breaking it down. It is faster but less reliable than TCP, as it does not ensure the message's arrival.

#### Example:
Streaming services like Netflix often use UDP for faster data transfer, even if some data packets are lost.


## Azure vs AWS

### Azure:

- **Resource Group Management**: Azure's Resource Groups allow users to manage resources for different projects more efficiently.
- **Resource Handling**: Easier and more integrated with other Microsoft services.
- **Popularity**: More popular in regions like the Middle East.
- **Database Management**: Managed SQL services are more user-friendly.

### AWS:

- **EC2 Instances**: Well-known for robust and flexible virtual computing environments.
- **Fame**: AWS is highly regarded in the Data Engineering community.

## Security Considerations

### RFP (Request for Proposal)

Companies issue RFPs outlining requirements, and vendors submit proposals. The best proposal is selected based on compliance with requirements.

### Compliance and Regulations

Every country has specific norms that companies must adhere to, ensuring legal and ethical operations.

### Data Security (Data at Rest and Data in Transit)

- **Data at Rest**: Data stored on a device or server. Must be encrypted to prevent unauthorized access.
- **Data in Transit**: Data being transferred over a network. Must be secured using encryption protocols like TLS (Transport Layer Security).

### PCIDSS Compliance

- **PCIDSS (Payment Card Industry Data Security Standard)**: A set of security standards designed to ensure that all companies accepting, processing, storing, or transmitting credit card information maintain a secure environment.
