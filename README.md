# IP Addressing for Small Network Configuration

This project contains notes and examples related to **IPv4 addressing**, aimed at the configuration of small networks. The goal is to explain the basic concepts of **IPv4**, **network masks**, **subnets**, and more.

## Table of Contents

- [IP Addressing for Small Network Configuration](#ip-addressing-for-small-network-configuration)
	- [Table of Contents](#table-of-contents)
	- [IPv4 Addressing](#ipv4-addressing)
		- [IPv4 Address Classes](#ipv4-address-classes)
		- [IP Groups](#ip-groups)
		- [Network Masks](#network-masks)
		- [CIDR Notation](#cidr-notation)
		- [Private IP Addresses](#private-ip-addresses)
		- [Reserved IP Addresses](#reserved-ip-addresses)
	- [Key Concepts](#key-concepts)
		- [TCP (Tranfer Control Protocol)](#tcp-tranfer-control-protocol)
		- [Network Overlap](#network-overlap)
		- [Subnets](#subnets)
		- [Network Devices: Switch and Router](#network-devices-switch-and-router)

---

## IPv4 Addressing

The IPv4 protocol uses 32-bit addresses, typically represented as four octets in dotted decimal notation, such as **192.168.0.0**.

### IPv4 Address Classes

IPv4 addresses are organized into classes, depending on the value of the first octet:

- **Class A**: Addresses from `0` to `127`
  - The first byte defines the **network**, and the other three define the **hosts**.
- **Class B**: Addresses from `128` to `191`
  - The first two bytes define the **network**, and the last two define the **hosts**.
- **Class C**: Addresses from `192` to `223`
  - The first three bytes define the **network**, and the last byte defines the **hosts**.
- **Class D**: Addresses from `224` to `239` (used for **multicasting**)
  - These addresses are not divided between network and host parts, as they are used for multicast transmissions.
- **Class E**: Addresses from `240` to `255` (reserved for experimental purposes).

### IP Groups

IP addresses can be classified into three categories:

- **Network**: The first possible IP in a network, which identifies the network itself.
- **Host**: IP addresses assigned to devices within a network.
- **Broadcast**: The last possible address within a network, used to send messages to all hosts on the network.

### Network Masks

A network mask is used to separate the **network** part from the **host** part of an IP address. It is a 32-bit value indicating how many bits are used for the network and how many are used for the hosts.

Examples of network masks:

- **Class A**: `255.0.0.0` (binary: `11111111.00000000.00000000.00000000`)
- **Class B**: `255.255.0.0`
- **Class C**: `255.255.255.0`

The network mask helps determine which network an IP address belongs to.

### CIDR Notation

In **CIDR (Classless Inter-Domain Routing) notation**, a network mask is represented by the number of consecutive 1 bits. For example:

- `255.0.0.0` is represented as `/8`.
- `255.255.0.0` as `/16`.
- `255.255.255.0` as `/24`.

The network mask does not need to match the class of the address. When it follows the class-based pattern, it is called a **default mask**.

### Private IP Addresses

Private IP addresses are used in local networks and are not routable on the public Internet. They are defined in **RFC 1918**:

- **Class A**: `10.0.0.0` to `10.255.255.255`
- **Class B**: `172.16.0.0` to `172.31.255.255`
- **Class C**: `192.168.0.0` to `192.168.255.255`

Private IP addresses are widely used in home and corporate networks.

### Reserved IP Addresses

Reserved addresses have specific purposes:

- **Loopback**: `127.0.0.0` to `127.255.255.255` (e.g., `127.0.0.1`)
- **Link-local**: `169.254.0.0` to `169.254.255.255` (used when there is no DHCP)
- **Multicast**: `224.0.0.0` to `239.255.255.255`
- **Experimental**: `240.0.0.0` to `255.255.255.255`

These addresses are not used for common devices on the public Internet.

---

## Key Concepts

### TCP (Tranfer Control Protocol)

Imagine TCP as a super-reliable delivery service for the Internet. When you send a message or data, TCP guarantees that:

1. **Connection Established**: Before anything else, the two computers shake hands (make a connection) to ensure that they are both ready to talk.
2. **Data Splitting**: The large message is divided into smaller packages, as if they were several boxes of a delivery.
3. **Sending and Receiving**: Each package is sent one by one, and the recipient confirms the arrival of each one, like a delivery receipt.
4. **Resending Lost Packets**: If a packet is lost on the way, TCP asks to resend it, ensuring that nothing is lost.
5. **Packet reassembly**: When all the packets have arrived, TCP puts everything back together in the original message, as if it were assembling a jigsaw puzzle.

This ensures that the message arrives complete, in the right order and without errors, providing reliable communication between devices on the network.

### Network Overlap

**Overlap** occurs when two or more IP address ranges overlap, causing issues such as:

- **Routing confusion**: Routers may not know where to send packets.
- **IP conflicts**: Devices may end up with the same IP address, leading to connectivity problems.
- **Security**: Traffic might be routed unexpectedly.

### Subnets

A **subnet** divides a large network into smaller, more manageable networks. Example of subnet calculation:

For the IP **192.168.0.20/26**, the subnet mask is `255.255.255.192`, which has a step size of `64`:

256 - 192 = 64

Thus, the subnet interval is:

- **192.168.0.0**
- **192.168.0.63**
 
 The **192.168.0.0** is the Network IP.  
 The **192.168.0.63** is the Broadcasting IP.  
 All the other ones are Hosts.  

### Network Devices: Switch and Router

- **Switch**: Necessary for connecting multiple devices on a **local network (LAN)**.
- **Router**: Connects different networks. It must avoid **overlap**, as connecting networks with overlapping IP addresses can cause routing conflicts.
