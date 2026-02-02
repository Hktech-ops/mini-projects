## Highly Available, Scalable & Secure Web Architecture on Azure

This project delivers a production-ready, scalable, and secure web architecture built on Microsoft Azure.
The solution uses Virtual Machine Scale Sets for elastic compute, Load Balancer for traffic distribution across healthy instances, and multi-zonal deployment to eliminate single points of failure, providing zone-level redundancy and high availability.

- The environment follows modern cloud architecture practices, including:

  - Hub–Spoke VNet topology
  - Bastion for secure Admin access
  - NSGs with least-privilege rules
  - Route tables for forced tunneling

- Security features include:

  - Simple DMZ-like public subnet
  - Routing + Subnet isolation
  - Block direct outbound (from private VM instances)




- stateless web tier (apache and all web servers)
- which is good for VMSS in uniform mode! fit these two in!
---------------------------


## Architecture Diagram:

<img width="1316" height="740" alt="image" src="https://github.com/user-attachments/assets/bb7e9909-2f96-476d-9471-3709ed31ae9c" />



* Inbound flow : Internet → Load Balancer → VMSS NICs (private subnet)
* Outbound flow : VMSS (private subnet) → Public Subnet → Internet


-------------------------

## IMPLEMENTATION:


## TASK 1: Provisioning of Resource Group, VNets, Subnets, Route Tables and Routes:

<img width="1463" height="371" alt="image" src="https://github.com/user-attachments/assets/28f6f3b0-a59a-4f6d-84ef-842e56c166ce" />

*** Vnets and Subnets ***

- 

<img width="1319" height="156" alt="image" src="https://github.com/user-attachments/assets/344ef5d9-43a7-479e-9efa-cffc3d55726c" />

*** 2 Route tables & their routes ***

-

<img width="1049" height="466" alt="image" src="https://github.com/user-attachments/assets/a38699a5-a23a-4777-a5f9-2f8824efc210" />
*** Public Route table routes ***

-

<img width="1091" height="467" alt="image" src="https://github.com/user-attachments/assets/4db76ab9-3447-4ac1-b273-43436af3e38f" />

*** Private Route table routes ***

-

<img width="1128" height="322" alt="image" src="https://github.com/user-attachments/assets/62c4790e-cfa5-4f5b-b661-0a92393ca3c2" />

*** Listed all routes ***


## TASK 2: Deployed a stand alone VM with user data script (Apache + Web Page) to capture its Golden image and then attached to VM Scale set and configured NSG

- Captured a Golden image of a VM for ease of future deployments

<img width="1623" height="530" alt="image" src="https://github.com/user-attachments/assets/e733ba82-ce39-4dfa-bae4-45eb0338803b" />

------------------------------

<img width="1700" height="613" alt="image" src="https://github.com/user-attachments/assets/c0c8c917-afdb-4189-a7fb-e9f7ebe569db" />
<img width="1119" height="552" alt="image" src="https://github.com/user-attachments/assets/eff6b91a-dd4b-408c-b662-e24f51cf298f" />

*** Scale set with custom auto scale deployed ***

- Scale out : Avg CPU usage > 60
- Scale in : Avg CPU usage < 30
- Passed user data script for installing and configuring Apache Web server



 -----------------------

<img width="1828" height="415" alt="image" src="https://github.com/user-attachments/assets/3adc3b8a-87de-4486-87b9-793caf2676ea" />
<img width="1855" height="413" alt="image" src="https://github.com/user-attachments/assets/fbcb4707-76e5-46cf-8d9b-aa44321961d7" />
<img width="1890" height="430" alt="image" src="https://github.com/user-attachments/assets/8430af40-18a0-4188-a364-a6a9d73243f2" />

*** Provisioned NSG rules ***

-

<img width="1844" height="302" alt="image" src="https://github.com/user-attachments/assets/55a45cc2-d960-40d2-866c-e08400812d3a" />


- Inbound rules :
  - Allow inbound from Load Balacer on port 80
  - Allow inbound from Bastion on port 22 
  - Deny all other inbound



<img width="1401" height="225" alt="image" src="https://github.com/user-attachments/assets/2bed98af-3128-44f0-9d82-b9e209ed45dd" />

*** Associated NSG with privateSubnet ***
- Why associate NSG with privateSubnet ?
  -  VMSS --> Uniform mode. Since Azure treats entire scale set as a homogeneous pool identical instances, it has to be applied at the subnet              level

---------------------------


## TASK 3: Deployed Bastion Host for secure access to private VMs and configured bi-directional peering b/w the two VNets:

- I have already provisioned a dedicated AzureBastionSubnet in hubVNet
- Allocated a standard, static public IP address for Bastion

<img width="552" height="184" alt="image" src="https://github.com/user-attachments/assets/4d220cfb-29b7-4ce0-aa51-0b88933a1364" />
<img width="1335" height="548" alt="image" src="https://github.com/user-attachments/assets/c609ff5c-39a7-4dcf-b764-962c37d89575" />

*** Bastion public ip and deployment ***


------------------------------

<img width="1403" height="562" alt="image" src="https://github.com/user-attachments/assets/3380174e-1d1f-49bb-85c6-3f11ece90317" />

*** Hub to spoke peering ***

<img width="1409" height="339" alt="image" src="https://github.com/user-attachments/assets/7d5d5022-9edf-4211-9846-a2f7384824d8" />

*** Spoke to Hub peering ***


## TASK 4: Configured and Deployed Load Balancer






