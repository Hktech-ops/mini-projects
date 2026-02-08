## Highly Available, Scalable & Secure Web Architecture on Azure

This project delivers a production-ready, scalable, and secure web architecture built on Microsoft Azure.
The solution uses Virtual Machine Scale Sets for elastic compute, Application Gateway for path based routing to healthy VMs, and multi-zonal deployment to eliminate single points of failure, providing zone-level redundancy and high availability.

- The environment follows modern cloud architecture practices, including:

  - Hub–Spoke VNet topology
  - Firewall for secure flow of traffic
  - User defined Route Table for forced tunneling
  - Bastion for secure Admin access
  - NSG with least-privilege rules
  - Application Gateway for path based routing

- Security features include:

  - Routing + Subnet isolation
  - Block direct outbound (from private VM instances)
 
- Virtual machines are running on Apache server - which is loaded with Static Web pages
- Scale Set includes 2 VM instances to begin with. Custom scale set is configured to sale out to a mazimum of 4 instances (2 for each path) - to handle spike in traffic
  - VM1 : path to default + product web page
  - VM2 : path to offers + payments web page

- For implemetation, I captured two golden images, for each VM with their respective configurations and deployed them in scale set 
---------------------------------------------------

# Architecture Diagram:

<img width="1075" height="550" alt="image" src="https://github.com/user-attachments/assets/be2279b4-fb09-484e-bd1d-564cde277c64" />


- Inbound flow  :  Internet --> Firewall --> Application Gateway --> webSubnet (VMSS)
- Outbound flow :  webSubnet --> Firewall --> Internet

---------------------------------------------------

## Demonstration:

# Task 1 : Vnets, Subnets & Golden image, Public IPs


<img width="639" height="141" alt="image" src="https://github.com/user-attachments/assets/7f4d2177-10c0-4231-835a-c61762ca4e32" />

-  mgmtVnet : AzureFirewallSubnet & AzureBastionSubnet

<img width="930" height="140" alt="image" src="https://github.com/user-attachments/assets/a69a4248-9dd8-4cdc-8a57-a714c1b1b3f6" />

- workloadVnet : appGatewaySubnet & webSubnet

<img width="1067" height="165" alt="image" src="https://github.com/user-attachments/assets/2e45240b-6814-46bb-a3e6-c314a324caa5" />

- Captured Images : Apache Servers - VM1 (defult + products page) & VM2 (offers + payments page)

<img width="1037" height="138" alt="image" src="https://github.com/user-attachments/assets/379c9e86-309b-453b-86e3-32ec1d90c526" />

- 3 public ips required for this project :
  - firewall-pip
  - bastion-pip
  - appGateway-pip 



