# Cloudformation Deployed Opsworks CM Puppet master in Private only VPC

This Cloudformation when deployed into an AWS account will demonstrate the sucessful deployment of a Opsworks CM Managed Puppet Master into a private only VPC (No internet gateway or other form of internet access)

This is example code as referenced by the blog post at the [Sourced Group blog](https://www.sourcedgroup.com/blog/)

When deployed provisions the following resources;

* A Single VPC
* 2 Private subnets and associated route tables
* VPC endpoints for the following AWS Services to support the bootstraping of the Puppet instance
    * Cloudformation
    * EC2
    * EC2 Messages
    * Systems manager (SSM)
    * S3
* A security group that controls the access to the VPC endpoints
* The Opsworks EC2 instance's instance profile, Service role and instance IAM policies required for Opsworks CM to function in your account
* The Opsworks CM Puppet instance 
* A security group that controls access to the various Puppet services on the Opsworks instance

# Deployment instructions
1. Create the SSM Paramstore value /Opsworks/R10KKey and paste in your R10K Private key
2. Deploy the cloudformation template into your account and adjust any defined parameters that are set

# Additional notes
* Please be aware that this template provisions a number of resources that incur hourly costs.
* This provisions an Puppet instance in a private VPC only with no internet connectivity at all. If you wish to access the Puppet instance, you can
    * Change the network topology to provide access to the environment via the internet
    * Deploy additional EC2 instances into the VPC and use System Manager Session manager or port forwarding to get access within the VPC
* For production environments you should handle the private keys and passwords using encrypted values from Parameter Store or Secrets Manager


I hope that you find this example code of benefit.