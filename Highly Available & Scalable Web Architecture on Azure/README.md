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

<img width="365" height="110" alt="image" src="https://github.com/user-attachments/assets/68ea0f38-f0c7-4ee2-8411-4299e7394c7a" />
<img width="1899" height="262" alt="image" src="https://github.com/user-attachments/assets/a6032cd0-6ad2-4d9d-b0de-ee4225c7bbb6" />
*** Provisioned NSG rules ***

- Inbound rules :
  - Allow inbound traffic from Load Balacer on port 80
  - Deny all other inbound



<img width="1885" height="250" alt="image" src="https://github.com/user-attachments/assets/c2e6240d-6b27-4c63-8dc5-72ec3b19f8f4" />
*** Associated NSG with NIC ***

---------------------------


## TASK 3: Deployed Bastion Host for secure access to private VMs and configured bi-directional peering b/w the two VNets:

- I have already provisioned a dedicated AzureBastionSubnet in hubVNet
- Allocated a standard, static public IP address for Bastion

<img width="552" height="184" alt="image" src="https://github.com/user-attachments/assets/4d220cfb-29b7-4ce0-aa51-0b88933a1364" />
<img width="1335" height="548" alt="image" src="https://github.com/user-attachments/assets/c609ff5c-39a7-4dcf-b764-962c37d89575" />

*** Bastion public ip and deployment ***

- 

<img width="1878" height="214" alt="image" src="https://github.com/user-attachments/assets/c5823ec6-2f64-4146-b423-bedc66472a6e" />
*** NSG rule to allow Bastion access to VMs ***

------------------------------

<img width="1403" height="562" alt="image" src="https://github.com/user-attachments/assets/3380174e-1d1f-49bb-85c6-3f11ece90317" />

*** Hub to spoke peering ***

<img width="1409" height="339" alt="image" src="https://github.com/user-attachments/assets/7d5d5022-9edf-4211-9846-a2f7384824d8" />

*** Spoke to Hub peering ***


## TASK 4: Configured and Deployed Load Balancer






