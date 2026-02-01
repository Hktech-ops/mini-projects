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


## TASK 1: Provisioning of Resource Group, VNets and Subnets:






