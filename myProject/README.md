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
  - myScaleSet1 : path to default + product web page
  - myScaleSet2 : path to offers + payments web page

- For implemetation, I captured two golden images, for each VM with their respective configurations and deployed them in scale set 
---------------------------------------------------

# Architecture Diagram:

<img width="1063" height="539" alt="image" src="https://github.com/user-attachments/assets/720df0e5-c81d-40a2-b7ed-e334c3844d8f" />

- Inbound flow  :  Internet --> Firewall --> Application Gateway(Standard V2) --> webSubnet (VMSS)

  <img width="223" height="142" alt="image" src="https://github.com/user-attachments/assets/51ebace4-8981-4fa8-b4b1-d0dba59a1c02" />
  
- Outbound flow :  webSubnet --> Firewall --> Internet

  <img width="256" height="143" alt="image" src="https://github.com/user-attachments/assets/ee1a555f-c10a-4477-b901-f85eb851b62d" />
 
*** Inbound + Outbound traffic is centrally controlled : Firewall inspects everything! ***


---------------------------------------------------

## Demonstration:

# Task 1 : Vnets, Subnets & Golden image, Public IPs, Peering


<img width="639" height="141" alt="image" src="https://github.com/user-attachments/assets/7f4d2177-10c0-4231-835a-c61762ca4e32" />

-  mgmtVnet : AzureFirewallSubnet & AzureBastionSubnet

<img width="930" height="140" alt="image" src="https://github.com/user-attachments/assets/a69a4248-9dd8-4cdc-8a57-a714c1b1b3f6" />

- workloadVnet : appGatewaySubnet & webSubnet

<img width="1067" height="165" alt="image" src="https://github.com/user-attachments/assets/2e45240b-6814-46bb-a3e6-c314a324caa5" />

- Captured Images : Apache Servers - VM1 (defult + products page) & VM2 (offers + payments page)

<img width="1032" height="126" alt="image" src="https://github.com/user-attachments/assets/f0f7ec51-f751-4a17-8734-3e0b9186561a" />

- 2 public ips required for this project :
  - firewall-pip
  - bastion-pip
  - appGateway-pip (both private and public IP, however, public IP is NOT exposed to internet, keeping the gateway private)
    - created merely as Standard V2 Application Gateway required to have both public and private IP addresses! 


<img width="930" height="348" alt="image" src="https://github.com/user-attachments/assets/4912d4c2-68e2-41c9-96d7-ca68c2b8d11e" />

- Peering : mgmtVnet <---> workloadVnet

-----------------------------------

# Task 2 : Scale Sets (uniform orchestration) & Custom Auto Scale rules

- Deployed two scale sets in uniform orchestration mode. Why? Identical VMs (except for thier content) in the scale set
- Custom auto scale rules : Scale out & Scale in based on avg. CPU usage
  - Scale out : Avg. CPU usage > 70%
  - Scale in : Avg. CPU uage < 30 for a duration of 5 mins

------------------------------------

<img width="880" height="126" alt="image" src="https://github.com/user-attachments/assets/eb51aaaa-7ec8-4ac5-936b-f719bb7f4090" />

- Deployed 2 VM Scale Sets
  
<img width="1896" height="288" alt="image" src="https://github.com/user-attachments/assets/75f70ee8-f796-435f-abe5-8f9af9a46426" />

- VMSS instances

<img width="839" height="313" alt="image" src="https://github.com/user-attachments/assets/b03fb266-d7ab-42ca-b77f-89203a2f9b48" />

- Scaling rules

---------------------------------------

Task 3 : Firewall, Application Gateway and User-defined Routes


<img width="645" height="239" alt="image" src="https://github.com/user-attachments/assets/89e24460-3251-44f4-b914-1e1ea59044ec" />

- Created myFirewall

<img width="771" height="233" alt="image" src="https://github.com/user-attachments/assets/9a568706-1b3a-4e9f-9478-d5df701166e5" />

- Firewall ip-config


--- app gateway


<img width="832" height="766" alt="image" src="https://github.com/user-attachments/assets/f6a3993d-dbce-4448-ada6-7f027492dd15" />

path based routing rules
allowed from private ip of app gateway --> why? firewall DNAT will translate allowed incoming traffic to app gateway's private ip 


----------------------

<img width="646" height="197" alt="image" src="https://github.com/user-attachments/assets/d2656ee7-ded5-48b9-98a3-575428c97b3d" />

- Queried Private IP address of Firewall


<img width="1089" height="326" alt="image" src="https://github.com/user-attachments/assets/d63b76ff-05cf-4410-9ff2-1305d6058089" />



<img width="1710" height="432" alt="image" src="https://github.com/user-attachments/assets/71340a8a-30f7-47fd-a927-0bf990d3616e" />
**** NSG with inbound from App Gateway ***


<img width="506" height="241" alt="image" src="https://github.com/user-attachments/assets/da8980e8-6adb-41fd-9229-10328fee9b4b" />
*** associated with webSubnet


