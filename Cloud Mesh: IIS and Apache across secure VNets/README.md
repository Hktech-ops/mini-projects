## Problem Statement:

Modern enterprises often operate multiple on‑premises data centers connected through high‑availability WAN topologies. To support upcoming cloud migration initiatives, your organization requires a lab environment that accurately reflects the network architecture of its East US data centers, which currently communicate over a fully meshed WAN with unrestricted intersite connectivity.
The objective of this project is to design and deploy an Azure‑based simulation of this topology, validate cross‑site communication, and implement foundational security controls. This lab will serve as a proof‑of‑concept for hybrid connectivity planning, network segmentation strategies, and automated workload deployment.

## Scope of work:

1. Provision the Lab Environment
  - Deploy two isolated virtual networks representing on‑premises data center sites.
  - Create subnets, network interfaces, and virtual machines in each site.
  - Automate web server deployment using:
    - Cloud‑init/UserData for IIS on Windows Server
    - External Bash script for Apache on Linux

2. Configure Local VNet Peering
  - Establish bidirectional VNet peering to simulate a mesh WAN.
  - Validate that address spaces do not overlap.
  - Ensure forwarded traffic and gateway transit settings align with enterprise patterns

3. Test Intersite Connectivity
  - Verify VM‑to‑VM communication across peered VNets.
  - Use tools such as:
  - Test-NetConnection (Windows)
  - curl / ping / wget (Linux)
  - Confirm HTTP access to both web servers from each site.

4. Secure the Virtual Network
  - Implement Network Security Groups (NSGs) at subnet or NIC level.
  - Allow only required inbound ports (HTTP/HTTPS, RDP/SSH).
  - Deny all unnecessary traffic.
  - (Optional) Enable NSG Flow Logs for traffic visibility

5. Architecture Diagram

<img width="940" height="383" alt="image" src="https://github.com/user-attachments/assets/0a1782ef-a325-418c-afff-9acea2940d9f" />

The diagram illustrates two Azure VNets representing on‑premises data centers, each hosting a VM with an automated web server deployment. VNet peering provides full mesh connectivity between the sites.

----------------------------------------------------

## Tasks:

1. Provision Lab Environment:





