# Networking Workshop

## This Networking Workshop aims to help customers and partners migrate from VPC peering to Transit Gateway with minimum downtime.

### Prerequisites:
* Hands on working knowledge with AWS
* Foundational knowledge of IP Networking
* Atleast one AWS account with admin privileges

### Modules:
* Multi VPC and Multi account networking architecture using VPC peering
* Datacenter Connectivity
* AWS Transit Gateway deployment and migration from VPC peering 
* Transit Gateway Network Manager
* Setup Network Monitoring
* Hybrid DNS basic lab1
* Hybrid DNS detailed labs
  
### Core Instructions 
 * Prepare a Multi VPC and Multi Account design that should be someting like below, ideally create on a sharable spreadsheet that all lab participants can refer.

AWS Account Number | Region | Region CIDR | Autonomous Number| Candidate Name
-------------------|--------|-------------|------------------|---------------
<AWS-Account-ID>| us-east-1 |  10.0.0.0/16 | 64512| Spider Man
<AWS-Account-ID| us-east-2 |  10.1.0.0/16 | 64513| Captainm America
<AWS-Account-ID| us-west-1 |  10.2.0.0/16 | 64514| Wonder Women
<AWS-Account-ID| us-west-2 |  10.0.0.0/16 | 64515| Bat Man
 
* Download all the CloudFormation templates from the directory `/CloudFormation` and save on your workstation. 
* In each AWS account create a S3 bucket with a unique name (S3 is a global namespace) like `<AWS-Account-ID>-nw-workshop-templates` and upload all the CloudFormation templates you downloaded in previous step.

Your core steps are now complete, please proceed to the next module.

### Module1 Instructions:  
* On AWS console, nagivate to `CloudFormation` service, ensure you are in the right region as allocated part of `Core Instructions`
* Click on `Create Stack` > `Template is ready` > `Upload a template file` > `Chose file` > locate and upload the file named `nw-workshop-master`
* In `Stack Name` input a meaningful name , under parameters specify the `RegionCIDR` as allocated part of `Core Instructions` and leave the `EnvironemtName` as default.
* Accept defaults in next screen and select `Next`
* Towards the bottom under Capabilities Section accept:
     * `I acknowledge that AWS CloudFormation might create IAM resources with custom names.` 
     * `I acknowledge that AWS CloudFormation might require the following capability: CAPABILITY_AUTO_EXPAND` 
     *  Click `Create Stack`
     
