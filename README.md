## PROJECT-3

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

## Create and Verify your VPC
* Login to your aws account
* Navigate to VPC service
* Create VPC
* Choose VPC only 
* Provide VPC name “project3-vpc”
* Provide IPv4 CIDR block “10.0.0.0/16”
* Choose Tenancy “default’
* Click “create VPC” button 

## Create Internet Gateway

* Navigate to Internet Gateway 
* Click the "Create internet gateway" button
* Provide a name “my-igw”
* Click the "Create internet gateway" button
* Click the "Actions" button and choose "Attach to VPC".
* Choose “*project3-vpc” from Available VPCs 

## Create subnets
* Navigate to Subnets
* Click the "Create subnet" button
* Select the VPC “project3-vpc’
* Provide subnet name “pubsub1”
* Availability Zone “us-east-2a”
* Provide IPv4 CIDR block “10.0.1.0/24”

* Add new subnet
* Provide subnet name “pubsub2”
* Availability Zone “us-east-2b”
* Provide IPv4 CIDR block “10.0.2.0/24”

* Add new subnet
* Provide subnet name “privsub1”
* Availability Zone “us-east-2a”
* Provide IPv4 CIDR block “10.0.100.0/24”

* Add new subnet
* Provide subnet name “privsub2”
* Availability Zone “us-east-2b”
* Provide IPv4 CIDR block “10.0.101.0/24”
* Click the "Create subnet" button



## Enabling auto-assign public IPv4 address for public subnets

* Navigate to Subnets
* Choose “pubsub1”, actions and “edit subnet settings” and check “Enabling auto-assign public IPv4 address” and click save button. 
* Choose “pubsub2”, actions and “edit subnet settings” and check “Enabling auto-assign public IPv4 address” and click save button. 

* Navigate to "Route tables"
* Select existing route table
* Choose Routes and “edit routes”
* Add route and type give destination cidr block “0.0.0.0/0” and for target choose “internet gateway igw” and save changes
* Subnet associations, edit subnet associations  choose public subnets pubsu1 and pubsub2 and click save associations button. 


## Creating an EC2 Instance Inside the Newly Created VPC

* Navigate to EC2
* Click on Instance 
* Click on Launch Instance
* Provide name “projects3-ec2”
* Leave default an Amazon Machine Image choose Amazon Linux
* Leave default instance type t2.micro 
* Key pair, proceed without key pair
* Network settings, click on “edit” button choose “projects3-vpc” choose any of the public subnets “pubsub2” 
* Firewall(security group) it will create it by default with ssh port open
* Click on Launch instance 

## Creating 2 S3 Buckets. 

* Navigate to the S3 Dashboard
* Click on "Create Bucket".
* Provide Bucket name “damira-bucket1” leave everything else as default and click on “Create button”
* Provide Bucket name “damira-bucket2” leave everything else as default and click on “Create button”
* Navigate to Buckets click on “ damira-bucket1, click Upload , click on Add Files and choose the file that you want to upload click on that file, open and click on upload button.

## Grant Access to EC2 for S3 Bucket
* Navigate to the IAM Dashboard
* Click on Roles
* Click on Create role and Trusted entity type leave as default "AWS services"
* Use case choose EC2 and click on next
* Permission policies search for "AmazonS3FullAccess" and click next
* Provide the role name "ec2-s3-full-access" click create role
* Navigate to EC2, click on instance, choose the proper instance "projects3-ec2", click on Actions choose "Security" then click on "Modify IAM role" 
* Choose IAM role "ec2-s3-full-access" then click on Update IAM role


## Copy file "filename" from one bucket to another

* Choose you EC2 instance, click on connect and connect  
* To list the all the buckets in your account use command 
  aws s3 ls
* To list content of the bucket use command below
  aws s3 ls s3://damira-bucket1
* To copy the file from s3 bucket1 to EC2 instance use command below
  aws s3 cp s3://damira-bucket1/eliza.txt . 
* To copy file from EC2 instance to S3 bucket2
  aws s3 cp eliza.txt s3://damira-bucket2
* To confirm file was copied to bucket2, run command below
  aws s3 ls s3://damira-bucket2
* You may also check from the console clicking on bucket2


| Participants | Time Spent hrs |
| ------------ | -------------- |
| Amela        | 10             |
| Eliza        | 10             |
| Damira       | 10             |
| Mukhiddin    | 10             |
| John         | 10             |




