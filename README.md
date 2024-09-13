This project demonstrates the deployment of a 3-tier architecture on AWS using Terraform as the Infrastructure as Code (IaC) tool. The architecture consists of public and private subnets across two availability zones (AZs), ensuring high availability and fault tolerance. Below is an overview of the setup:
![VPC 3 Tier Framed](https://github.com/user-attachments/assets/25b8194e-e403-4430-8b44-a9a5e6c5c22f)

VPC (Virtual Private Cloud):
  The project begins with the creation of a custom VPC to host all resources securely. This isolated virtual network allows for fine-grained control over the resources' access.

Subnets:

  Public Subnets: These subnets, located in both AZs, are attached to an Internet Gateway, allowing instances within them to communicate with the internet. Resources like NAT Gateways are deployed here.

  Private Subnets: Both AZs have private subnets dedicated to hosting EC2 instances and databases. These subnets do not have direct internet access for enhanced security.

Internet Gateway:
  An Internet Gateway is deployed to enable outbound communication from the public subnets, providing public instances the ability to connect to the internet.

NAT Gateway:
  In each availability zone, a NAT Gateway is provisioned within the public subnets to enable instances in private subnets to access the internet for updates and patches, without exposing them to inbound internet traffic.

Elastic IP Addresses:
  Each NAT Gateway is associated with an Elastic IP address, allowing consistent communication with external networks.

Route Tables:
  The public subnets are associated with route tables that route internet-bound traffic via the Internet Gateway. Private subnets have route tables that route internet-bound traffic through the NAT Gateway, securing the instances while allowing outbound connections.

Tiered Services:

  Web Tier: Hosted in public subnets, it handles all internet-facing services.

  Application Tier: EC2 instances in the private subnet manage business logic and communicate with the database layer.

  Database Tier: Dedicated private subnets ensure secure and isolated database operations.

By leveraging Terraform, the entire infrastructure is automated and can be provisioned with minimal manual intervention, improving efficiency and scalability. The design ensures high availability, security, and flexibility, critical for production environments.
