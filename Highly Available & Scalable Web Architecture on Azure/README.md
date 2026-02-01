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

-






