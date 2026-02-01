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


---------------------------


## Architecture Diagram:

<img width="1356" height="742" alt="image" src="https://github.com/user-attachments/assets/640c918d-c101-4491-8b32-31120fc39fd9" />



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


## TASK 2: Deployd zone redundant VM Scale Set(private instance) with Apache, took Golden Image and configured NSG:


<img width="1700" height="613" alt="image" src="https://github.com/user-attachments/assets/c0c8c917-afdb-4189-a7fb-e9f7ebe569db" />
<img width="1119" height="552" alt="image" src="https://github.com/user-attachments/assets/eff6b91a-dd4b-408c-b662-e24f51cf298f" />

*** Scale set with custom auto scale deployed ***

- Scale out : Avg CPU usage > 60
- Scale in : Avg CPU usage < 30
- Passed user data script for installing and configuring Apache Web server


 - Captured a Golden image of VM instance for ease of future deployments



 -

<img width="365" height="110" alt="image" src="https://github.com/user-attachments/assets/68ea0f38-f0c7-4ee2-8411-4299e7394c7a" />
<img width="1899" height="262" alt="image" src="https://github.com/user-attachments/assets/a6032cd0-6ad2-4d9d-b0de-ee4225c7bbb6" />
*** Provisioned NSG rules ***

- Inbound rules :
  - Allow inbound traffic from Load Balacer on port 80
  - Deny all other inbound








