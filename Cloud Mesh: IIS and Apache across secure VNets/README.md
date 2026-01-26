## Problem Statement:

Modern enterprises often operate multiple on‑premises data centers connected through high‑availability WAN topologies. To support upcoming cloud migration initiatives, your organization requires a lab environment that accurately reflects the network architecture of its East US data centers, which currently communicate over a fully meshed WAN with unrestricted intersite connectivity.
The objective of this project is to design and deploy an Azure‑based simulation of this topology, validate cross‑site communication, and implement foundational security controls. This lab will serve as a proof‑of‑concept for hybrid connectivity planning, network segmentation strategies, and automated workload deployment.

## Scope of work:

1. Provision the Lab Environment
  - Deploy two isolated virtual networks representing on‑premises data center sites.
  - Create subnets, network interfaces, and virtual machines in each site.
  - Automate web server deployment using:
    - Custom script extension for IIS on Windows Server
    - User Data script for Apache on Linux

2.  Configure bi-directional VNet Peering:
  - Establish bidirectional VNet peering to simulate a mesh WAN.

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
<img width="400" height="319" alt="image" src="https://github.com/user-attachments/assets/b0455e57-86e3-4a37-b8d0-24e945cf7453" />
<img width="386" height="198" alt="image" src="https://github.com/user-attachments/assets/28610fe0-57b7-428c-a513-b291e0d4744a" />

*** Created 2 RGs and Deployed VNets and Subnets ***


<img width="1405" height="346" alt="image" src="https://github.com/user-attachments/assets/e19665fb-ae2d-4d2c-9fb7-24ce123aef8c" />
<img width="490" height="461" alt="image" src="https://github.com/user-attachments/assets/c921cc0d-47fd-4ed6-9690-cd1cd9a906b2" />

*** Provisioned storage account and added a container ****

- Why Public storage account?
  - Public network access is enabled on the storage account to allow the VM Custom Script Extension to retrieve the IIS deployment script. Since the storage account contains no sensitive data and is used solely for automation artifacts, this configuration is appropriate for a lab environment.


- <img width="848" height="562" alt="image" src="https://github.com/user-attachments/assets/24420614-b3b2-4429-8d0a-7093a49b0553" />

*** Uploaded PowerShell script to the container ***


<img width="783" height="372" alt="image" src="https://github.com/user-attachments/assets/336d178f-931e-4edb-a6c8-f8b0f661ae1b" />

https://iisdeploymentstorage.blob.core.windows.net/scripts/install-iis.ps1
*** Extracted script url ***

<img width="1635" height="618" alt="image" src="https://github.com/user-attachments/assets/44e388af-d9a2-4fbf-a7d5-b9735cacdfad" />

*** Deployed Private Windows server with custom IIS installation script ***
*** Private IP of vm-1 : 10.0.0.4 ***

<img width="1560" height="622" alt="image" src="https://github.com/user-attachments/assets/8f35c1ad-9af0-4afa-9201-ae32b0ec3d35" />

*** Deployed Private Ubuntu VM with user data, containing Apache installation script ***
*** Private IP of vm-2 : 10.1.0.4 ***

2. Configure bi-directional VNet Peering:

<img width="1288" height="102" alt="image" src="https://github.com/user-attachments/assets/1966842d-9ea6-460c-9065-4af2e05083d8" />

*** Queried ids of both the VNets ***

<img width="1445" height="287" alt="image" src="https://github.com/user-attachments/assets/0688aa6a-6f43-4cb2-8c20-bde22c5a5059" />

*** Peering from VNet-1 to VNet-2 ***

<img width="1541" height="344" alt="image" src="https://github.com/user-attachments/assets/51c40a6e-fa8e-46ee-9a3c-d3b09d183a0a" />

*** Peering from VNet-2 to VNet-1 ***

<img width="1011" height="430" alt="image" src="https://github.com/user-attachments/assets/d49bbe8c-54bb-48a1-8bbc-930277922c81" />
<img width="1092" height="447" alt="image" src="https://github.com/user-attachments/assets/1f644ada-60e4-4a25-a723-f9e1b6f52637" />

*** Verified both peerings in portal ***


3. Test Intersite (End to End) Connectivity

a. Layer 3 - Basic Network Reachability

<img width="1358" height="839" alt="image" src="https://github.com/user-attachments/assets/f3e4d328-ea66-4180-b076-28ae6bc369df" />

*** Successfully pinged vm-2 from vm-1 ***

b. Layer 4 - Port level connectivity (TCP)

<img width="1501" height="350" alt="image" src="https://github.com/user-attachments/assets/3e5cc4cc-eb1a-4be7-ba9d-b598ec46dbb6" />
<img width="405" height="406" alt="image" src="https://github.com/user-attachments/assets/9515b03f-6049-430b-b6d0-bf2569b0a8a6" />


*** Successfully validated port level connectivity b/w two VMs ***

c. Layer 7 - Application level connectivity

<img width="1285" height="828" alt="image" src="https://github.com/user-attachments/assets/cb4eebee-d65e-491e-95de-bc8a12995798" />
<img width="949" height="641" alt="image" src="https://github.com/user-attachments/assets/eede3be7-5f39-4bef-bd5b-ad8888165f92" />

