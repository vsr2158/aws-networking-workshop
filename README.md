# Networking Workshop

## This Networking Workshop aims to help customers and partners migrate from VPC peering to Transit Gateway with minimum downtime.

### Prerequisites:
* Hands on working knowledge with AWS
* Foundational knowledge of IP Networking
* Atleast one AWS account with admin privileges

### Modules:
* Module1: Deploy Multi VPC and Multi account networking architecture using VPC peering
* Module2: AWS Transit Gateway deployment and migration from VPC peering 
* Module3: Datacenter Connectivity
* Module4: Transit Gateway Network Manager
* Module5: Network Monitoring
* Module6: Hybrid DNS basic lab1
* Module7  Hybrid DNS Advanced
  
### Core Instructions 

We will begin with a Multi VPC and Multi Account design that is uniqute to this workshop, please discuss and prepare something that resembles sample shown below

AWS Account ID | AWS Region | AWS Region CIDR | Datacenter CIDR|  Autonomous System Number| Student Number | Student Name
------------------|---------|-------------|----------------|-------------------|----------------|-------------
AWS-Account-ID| us-east-1 |  10.0.0.0/16 |192.168.0.0/24 | 64512| 0| Spider Man
AWS-Account-ID| us-east-2 |  10.1.0.0/16 |192.168.1.0/24 | 64513| 1| Captainm America
AWS-Account-ID| us-west-1 |  10.2.0.0/16 |192.168.2.0/24 | 64514| 2| Wonder Women
AWS-Account-ID| us-west-2 |  10.3.0.0/16 |192.168.3.0/24 | 64515| 3| Bat Man

* Download all the CloudFormation templates from the directory `/CloudFormation` and save on your workstation. 

* In each AWS account create a S3 bucket with a unique name (S3 is a global namespace) like `<AWS-Account-ID>-nw-workshop-templates` and upload all the CloudFormation templates you downloaded in previous step.

Your core steps are now complete, please proceed to the next module.

## Module1: Deploy Multi VPC AWS Infrastructure
#### Deploy CloudFormation template
* On AWS console, nagivate to `CloudFormation` service, ensure you are in the right region as allocated part of `Core Instructions`
* Click on `Create Stack` > `Template is ready` > `Upload a template file` > `Chose file` > locate and upload the file named `nw-workshop-master`
*  In `Stack Name` input a meaningful name , under parameters specify the `RegionCIDR` as allocated part of `Core Instructions` and leave the `EnvironemtName` as default.
* Accept defaults in next screen and select `Next`
* Towards the bottom under Capabilities Section accept:
    * `I acknowledge that AWS CloudFormation might create IAM resources with custom names.` 
    * `I acknowledge that AWS CloudFormation might require the following capability: CAPABILITY_AUTO_EXPAND` 
    *  Click `Create Stack`
* Stack creation will commence and will invoke nested stacks as required, you can watch the events  under the `Events Tab` on the console. Wait for the stack deployment to complete.
* Post Stack Deployment following resources are created:

    < Todo: Add a diagram of resources deployed > 
    
* TASK: Explore the deployed resources, test SSH login to all the instances deployed by this CloudFormation stack. Note that instances in private subnet will require SSH from the Bastion host in Public subnet.
* TASK: Test reachability between all EC2 instances. Is there connectivity between EC2 instances within the VPC? Is there connectivity between EC2 instances between the VPCs?
  

## Module2: AWS Transit Gateway deployment and migration from VPC peering 
#### Setup connectivity so the private instances in different VPCs can communicate between each other.
* Task: Identify the two VPCs deployed using CloudFormation, setup VPC peering between them. Is there connectivity between EC2 instances between the VPCs now? Leave the terminal open and Ping running for later tasks.


* Optional Bonus Task: With with a partner who has deployed in a different region and achieve connectivity with that instance
* Optional Bonus Task: What is the max MTU supported between the instances within same Region? What is max MTU supported between instances across regions?

This module is now complete, please proceed to the next module.

#### Migrate from VPC peering to Transit Gateway (TGW) based connectivity with minimum downtime
 
* Task: Deploy Transit Gateway (TGW) in the region. Remember TGW is a regional router and you can connect all VPCs in the same region belonging to this and other accounts to a single TGW

* Task: Create a TGW attachment to the VPC, check the TGW default roue table, what do you see? (A:CIDR from each VPC should be propogated to this route table)
* Task: Notice the Ping responses between the instances continue without any interruption, why? (A: VPC route table still is pointing to the VPC peering connection to route to the other VPC) Now change the VPC Route table to point to the TGW attachment instead of VPC peering connection on both VPCs. How long many ICMP packets were lost? Can you deduct the approximate outage time?
* Optional Bonus Task: In the previous step you enabled routing between two VPCs via TGW. What should you do to allow all communication via TGW? (A: Add a single 10.0.0.0/8 route for all the VPCs pointing towards TGW attachment ) 
* Optional Bonus Task: 

This module is now complete, please proceed to the next module.

## Module3: Datacenter Connectivity

In this module we will simulate a Datacenter deployed on seperate AWS account (This can be the same account in an unused region)
 
#### Deploy CloudFormation template
* On AWS console of account #2, nagivate to `CloudFormation` service, ensure you are in the right region as allocated part of `Core Instructions`
* Click on `Create Stack` > `Template is ready` > `Upload a template file` > `Chose file` > locate and upload the file named `nw-workshop-dc-master`
*  In `Stack Name` input a meaningful name , under parameters specify the `DatacenterCIDR` as allocated part of `Core Instructions` and leave the `EnvironemtName` as default.
* Accept defaults in next screen and select `Next`
* Towards the bottom under Capabilities Section accept:
    * `I acknowledge that AWS CloudFormation might create IAM resources with custom names.` 
    * `I acknowledge that AWS CloudFormation might require the following capability: CAPABILITY_AUTO_EXPAND` 
    *  Click `Create Stack`
* Stack creation will commence, you can watch the events  under the `Events Tab` on the console. Wait for the stack deployment to complete.
* Post Stack Deployment following resources are created:

    < Todo: Add a diagram of resources deployed > 
    
* Task: Explore the deployed resources, test SSH login to all the DC Bastion instances deployed by this CloudFormation stack.

* Task: 