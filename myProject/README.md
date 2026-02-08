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

<img width="1057" height="534" alt="image" src="https://github.com/user-attachments/assets/1910fc49-244d-4d6c-b99e-6ee287f730cd" />


- Inbound flow  :  Internet --> Firewall --> Application Gateway --> webSubnet (VMSS)
- Outbound flow :  webSubnet --> Firewall --> Internet

---------------------------------------------------

## Demonstration:

# Task 1 : Vnets, Subnets & Golden image, Public IPs, Peering


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


<img width="930" height="348" alt="image" src="https://github.com/user-attachments/assets/4912d4c2-68e2-41c9-96d7-ca68c2b8d11e" />

- Peering : mgmtVnet <---> workloadVnet


# Task 2 : Scale Sets (uniform orchestration), Custom Auto Scale rules User-defined Routes, 

- Deployed two scale sets in uniform orchestration mode. Why? Identical VMs (except for thier content) in the scale set
- Custom auto scale rules : Scale out & Scale in based on avg. CPU usage
  - Scale out : Avg. CPU usage > 70%
  - Scale in : Avg. CPU uage < 30 for a duration of 5 mins

-------------------------------

<img width="880" height="126" alt="image" src="https://github.com/user-attachments/assets/eb51aaaa-7ec8-4ac5-936b-f719bb7f4090" />

- Deployed 2 VM Scale Sets
  
<img width="1896" height="288" alt="image" src="https://github.com/user-attachments/assets/75f70ee8-f796-435f-abe5-8f9af9a46426" />

- VMSS instances

<img width="839" height="313" alt="image" src="https://github.com/user-attachments/assets/b03fb266-d7ab-42ca-b77f-89203a2f9b48" />

- Scaling rules


