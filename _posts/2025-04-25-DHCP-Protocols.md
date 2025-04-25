---
layout: post
title: DHCP Protocol
date: 25-04-2025
categories: [IT]
tags: [networking, computer science, dhcp, protocols, english]
---

<b>The DHCP Protocol can be very nifty. It is a network protocol that automates the assignment of IP addresses and other network configuration parameters to devices on a network. This eliminates the need for manual configuration, making network administration much easier.</b>

# What on earth is DHCP?
Dynamic Host Configuration Protocol is a network management protocol that allows you to connect a DHCP client to a DHCP server and automatically assign an IP address to the client from the server without having the need to configure it manually.<br>
This protocol uses the Client-Server architecture.

> **⚠ Important Information ⚠**<br>
> IP stands for Internet Protocol and it evolves around the OSI-Layer 3 (Network Layer).
> There are two types of IP addresses. One is the IPv4 and IPv6. IPv4 addresses are **32 Bit** long, meaning every octet has 8 Bit. It looks like this: 172.16.30.128
> 
> IPv6 addresses are **128 Bit long**. The IPv6 is built out of two parts: One is the **Prefix**, the other is the **Interface Identifier**. The Prefix shows, which network the address belongs to or what type of address it is. The Interface Identifier identifies the device currently holding the address, which is why every Interface Identifier is unique. The Prefix and the Interface Identifier are both 64 Bit long. This is how one looks like:  Prefix <--- fe80:0bd0:0000:0000|:cd00:000d:0ad0:2423 ---> Interface Identifier

# Now what does DHCP actually do?
Well, to be specific: A DHCP server distributes network parameters to DHCP clients. By network parameters, I mean stuff like IP Address, Subnet Mask, Default Gateway and the DNS Server. In some cases, it also sends Lease Duration aswell, for an example how long this specific address should be assigned to the client.

## DORA Principle
To understand what DHCP really does, let's concentrate on the specific events that happen between the DHCP server and DHCP client:<br>

<img src="/_posts/_assets/Dora_Principle.png" alt="Graphical View of the DORA Principle" width="254" height="354"><br>

- Weg-Zeit-Diagramm (German) means Path-time diagram.

### Discover
The client sends a DHCP discover message to the network to search for an available DHCP server. As the client does not yet have an IP address at this point, the message is sent as a broadcast so that all devices in the network can receive it.

### Offer
The DHCP server receives the DHCP Discover message and responds with a DHCP Offer message. In this message, the server suggests an IP address for the client to use. The DHCP server also contains other network information, such as the Subnet Mask, the Default Gateway (router) and the Lease Time (duration for which the IP address remains valid).

### Request
The client receives the offer and sends a DHCP request message back to the server to accept the offer and request the proposed IP address. This message confirms that the client wants to use the offered IP address.

### Acknowledge
The DHCP server receives the DHCP Request message and sends a DHCP Ack message back to the client. This message confirms the assignment of the IP address and contains the final network information that the client needs to fully integrate into the network. From this point on, the client uses the assigned IP address.