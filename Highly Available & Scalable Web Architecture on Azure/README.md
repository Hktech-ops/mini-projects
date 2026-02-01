## Highly Available and Scalable Web Architecture on Azure

This project delivers a production-ready, scalable, and secure web architecture built on Microsoft Azure.
The solution uses Virtual Machine Scale Sets for elastic compute, Load Balancer for traffic distribution across healthy instances, and multi-zonal deployment to eliminate single points of failure, providing zone-level redundancy and high availability.

- The environment follow modern cloud architecture practices, including:

  * Hub–Spoke VNet topology 
  * NSGs with least-privilege rules
  * Route tables for forced tunneling
  * Bastion for secure Admin access


---------------------------

Hub and Spoke Network topology:

Hub Vnet: for secure resources : Shared security devices
  Bastion

Spoke Vnet: Application Workload
  VMSS
  Load Balancer
  NSG
  Route tables (flow through public subnet)
