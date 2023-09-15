## PROJECTS 3

### REQUIREMENTS

*  Create VPC with all required components
*  Create EC2 Instance inside of newly created VPC
*  Create 2 S3 buckets
*  Upload 1 file to one of the buckets
*  Ssh to EC2 Instance and copy a file from one bucket to another using aws cli (You will
  need to work with permissions)

AWS Project Documentation
Project Overview
This project involves setting up a basic infrastructure on AWS, consisting of an EC2 instance running within a custom VPC. This VPC will have its own isolated network with a subnet and a connection to the internet through an Internet Gateway.

#### Create and Verify your VPC
* login to your aws account
* Navigate to VPC service
* Create VPC
* choose VPC only 
* provide VPC name “project3-vpc”
* Provide IPv4 CIDR block “10.0.0.0/16”
* choose Tenancy “default’
* Click “create VPC” button 

##Create Internet Gateway

* Navigate to Internet Gateway 
* Click the "Create internet gateway" button
* Provide a name “my-igw”
* Click the "Create internet gateway" button
* Click the "Actions" button and choose "Attach to VPC".
* Choose “project3-vpc” from Available VPCs 

##  Create subnets
* Navigate to Subnets
* Click the "Create subnet" button
* Select the VPC “project3-vpc’
* Provide subnet name “pubsub1”
* Availability Zone “us-east-2a”
* Provide IPv4 CIDR block “10.0.1.0/24”

* add new subnet
* Provide subnet name “pubsub2”
* Availability Zone “us-east-2b”
* Provide IPv4 CIDR block “10.0.2.0/24”

* add new subnet
* Provide subnet name “privsub1”
* Availability Zone “us-east-2a”
* Provide IPv4 CIDR block “10.0.100.0/24”

* add new subnet
* Provide subnet name “privsub2”
* Availability Zone “us-east-2b”
* Provide IPv4 CIDR block “10.0.101.0/24”
* Click the "Create subnet" button



## Enabling auto-assign public IPv4 address for public subnets
* Navigate to Subnets
* choose “pubsub1”, actions and “edit subnet settings” and check “Enabling auto-assign public IPv4 address” and click save button. 
* choose “pubsub2”, actions and “edit subnet settings” and check “Enabling auto-assign public IPv4 address” and click save button. 

* Navigate to "Route tables"
* select existing route table
*  choose Routes and “edit routes”
* add route and type give destination cidr block “0.0.0.0/0” and for target choose “internet gateway igw” and save changes
* subnet associations, edit subnet associations  choose public subnets pubsu1 and pubsub2 and click save associations button. 


## Creating an EC2 Instance Inside the Newly Created VPC
* Navigate to the Instances 
* Click on Launch Instance
* provide name “projects3-ec2”
* leave default an Amazon Machine Image choose Amazon Linux
* leave default instance type t2.micro 
* key pair, proceed without key pair
* network settings, click on “edit” button choose “projects3-vpc” choose any of the public subnets “pubsub2” 
* firewall(security group) it will create it by default with ssh port open
* click on Launch instance 

## Creating 2 s3 buckets. 
* Navigate to the S3 Dashboard
* Click on "Create Bucket".
*  provide Bucket name “ damira-bucket1” leave everything else as default and click on “Create button”
*  provide Bucket name “ damira-bucket2” leave everything else as default and click on “Create button”
* Navigate to Buckets click on “ damira-bucket1, click Upload , click on Add Files and choose the file that you want to upload click on that file, open and click on upload button.

	4. Granting EC2 Access to S3 Bucket
To allow an Amazon EC2 instance to interact with an S3 bucket, we primarily use IAM roles. This document will guide you on how to create and assign an IAM role to an EC2 instance to grant it the necessary permissions to access S3
Create an IAM Role for EC2
Navigate to the IAM Dashboard.
In the navigation pane, click Roles and then click Create role.
For the trusted entity type, choose AWS service and select EC2. Then click Next: In our case pick AmazonS3FullAccess. Then click Next. 
Provide the meaningful name for role.
Click Create role.
 
5. Attach the IAM Role to the EC2 Instance
Navigate to the EC2 Dashboard and select the Instances link in the left navigation.
Click Action, click Security, choose Modify IAM role on the EC2 instance you want to grant access to S3. 
Pick created IAM role and click Update IAM role.

6. Access S3 from EC2
Now that your EC2 instance has the required permissions, you can access S3 using the AWS CLI. 
SSH into your EC2 instance.
Use the following command to list the contents of your S3 bucket:
aws s3 ls s3://YOUR_BUCKET_NAME/
Download the file from the bucket to EC2
$ aws s3 cp s3://YOUR_BUCKET_NAME / YOUR_FILE_NAME.txt .
Upload this file from EC2 to the another bucket
aws s3 cp YOUR_FILE_NAME.txt s3:// YOUR_BUCKET_NAME





