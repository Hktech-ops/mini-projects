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
- Scale Set includes 2 VM instances to begin with
  - VM1 : Route to default + product web page
  - VM2 : Route to offers + payments web page

- For implemetation, I captured two golden images, for each VM with their respective configurations and deployed them in scale set 
