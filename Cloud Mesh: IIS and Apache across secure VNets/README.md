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

<img width="1462" height="351" alt="image" src="https://github.com/user-attachments/assets/3e43367a-e221-485e-a2a9-eec42f84d020" />
<img width="446" height="320" alt="image" src="https://github.com/user-attachments/assets/70840c43-e31c-4569-bf43-435f822f1cd6" />
<img width="420" height="318" alt="image" src="https://github.com/user-attachments/assets/16b8523e-616e-4a75-8655-2541690a814c" />

*** Created 2 RGs and Deployed VNets and Subnets ***


<img width="1405" height="346" alt="image" src="https://github.com/user-attachments/assets/e19665fb-ae2d-4d2c-9fb7-24ce123aef8c" />
<img width="490" height="461" alt="image" src="https://github.com/user-attachments/assets/c921cc0d-47fd-4ed6-9690-cd1cd9a906b2" />

*** Provisioned storage account and added a container ****

- Why Public storage account?
  - Public network access is enabled on the storage account to allow the VM Custom Script Extension to retrieve the IIS deployment script. Since the storage account contains no sensitive data and is used solely for automation artifacts, this configuration is appropriate for a lab environment.


- <img width="848" height="562" alt="image" src="https://github.com/user-attachments/assets/24420614-b3b2-4429-8d0a-7093a49b0553" />

*** Uploaded PowerShell script to the container ***


