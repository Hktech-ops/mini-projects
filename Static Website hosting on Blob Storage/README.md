## Static Website Hosting on Azure Blob Storage



****

Get back to this one with CDN and Front Door to make it enterprise grade!

****

This project demonstrates how to host a static website using blob storage. It is a cost-optimized, serverless way to publish a personal portfolio or landing page.  


## Architecture Diagram

<img width="1307" height="599" alt="image" src="https://github.com/user-attachments/assets/340646c5-ec0f-4ed7-bc49-70b5ba3d02c6" />

- Architecture Overview:
  -  GPv2 storage account - with web hosting enabled
  -  Storage account access restricted to only adminVM's subnet
  -  Secure website management via adminVM
  -  $web container stores site files
  -  Public https endpoint with custom domain


-----------------------------------------------------------------

## Demonstration


# Task 1: Resource Group, Storage account & Web container



