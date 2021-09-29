# Deployment, Provisioning & Automation

## Understanding EBS Volumes

Storage volumes that you attach to your EC2 instances

Highly available and scalable

gp2 - General Purpose SSD
* 3 IOPS per GB
* 16,000 IOPS per volume

io1 - Provisioned IOPS SSD
* 50 IOPS per GB
* Up to 64,000 IOPS per volume

io2 - Provisioned IOPS SSD
* Latest generation
* Higher durability and more IOPS
* 500 IOPS per GB
* Up to 64,000 IOPS per volume

st1 - Throughput Optimized HDD
* Low-cost HDD volume
* Baseline throughput of 40 MB/s per TB
* Burstable up to 250 MB/s per TB
* Used for Big Data, ETL and log processing

sc1 - Cold HDD
* Lowest cost option
* Baseline throughput of 12 MB/s per TB
* Burstable up to 80 MB/s per TB
* Used when performance is not a factor
* Cannot be a boot volume

## What is a Bastion Host?

Public-facing instance which enables you to SSH or RDP to your private instances from an untrusted network

Located in a public subnet and is reachable from the internet

Security hardened with unnecessary services removed

AKA a "jumpbox"

## Exploring Elastic Load Balancer

Load balancer - distributes network traffic across a group of servers

ALB - Application Load Balancer. Intelligent load balancing.

ELB - Network Load Balancer. High-performance load balancing for TCP traffic.

CLB - Classic Load Balancer. Legacy option.

Gateway Load Balancer - allows you to load balance workloads for third-party virtual appliances running in AWS

OSI 7 Layer Model

| Layer        | Use           |
| ------------- |:-------------:|
| 7 | Application |
| 6 | Presentation      |
| 5 | Session      |
| 4 | Transport      |
| 3 | Network      |
| 2 | Data Link      |
| 1 | Physical      |

### Understanding ELB Error Messages

5xx Error Codes - Server-side issues

4xx Error Codes - Client-side issues

HTTP 504 - Gateway Timeout. 
The target failed to respond. The ELB could not establish a connection to the target.

HTTP 502 - Bad gateway.
The target host is unreachable. Check whether traffic is allowed from the load balancer subnets to the targets.

HTTP 503 - Service unavailable.
No registered targets.

HTTP 400 - Bad request.
Malformed request.

HTTP 408 - Request timeout.
The client did not send data before the idle timeout period expired.

HTTP 464
The incoming request protocol is incompatible with the target group protocol.

### Understanding ELB Cloudwatch Metrics

Metrics:

* `HealthyHostCount`
* `UnHealthyHostCount`
* `RequestCount`
* `TargetResponseTime`
* HTTP Status Codes

### Elastic Load Balancer Access Logs

Capture information relating to incoming requests to your ELB

They are disabled by default

They are encrypted and stored in a S3 bucket and decrypted when you access them

## EC2 Image Builder

Allows you to create EC2 images

Image Pipeline - defines the configuration and end-to-end process of building images

Image Recipe - Image builder creates a recipe for each image, which can be shared, version-controlled

Build components - the software components to include in the image

Step 1: Base OS - provide a base OS image, e.g. Amazon Linux 2 AMI

Step 2: Software - define the software to install, e.g. Python, Node.js, security updates etc

Step 3: Test - run tests on the new image, e.g. does it boot?

Step 4: Distribute - distribute the image to the region(s) of your choice

## CloudFormation

IaC - Infrastructure as Code

Templates can be YAML or JSON files

### Template

Parameters - Input custom values

Conditions - e.g. provision resources based on environment

Resources - describes the AWS resources that CloudFormation will create (mandatory)

Mapping - allows you to create custom mappings like Region-AMI

Transform - allows you to reference code located in S3, e.g. Lambda code or reusable snippets of CloudFormation code

### Common Errors

Use the console to view the status of your stack and error messages.

IAM - insufficient permissions

Limits - resource limit exceeded, e.g. 20 EC2 instance limit

Failed rollback (`UPDATE_ROLLBACK_FAILED`) - CloudFormation will rollback to the previous state if a CloudFormation operation fails, i.e. if `create-stack` or `update-stack` do not work as planned.

### CloudFormation StackSets

Allow you to create, delete and update your stacks across multiple AWS accounts and regions using a single operation

You will need Cross-Account Roles to do so

Resource Access Manager - will allow you to share resources with other accounts, e.g. EC2 instances, S3 buckets etc

### Best Practices

IAM - control access to CloudFormation using IAM

Service Limits - be aware of them. If you hit a limit, CloudFormation will fail to create your stack

Avoid Manual Updates - manual changes create a mismatch between your stack template and the current state of the stack

CloudTrail - log calls to CloudFormation using CloudTrail

Stack Policy - a JSON document that describes what update actions can be performed on designated resources. Specify a stack policy whenever you create a stack that has critical resources.

### Blue/Green deployments

Use this deployment strategy when you are deploying a new version of your application

It is a low risk deployment strategy

<span style="color:blue">Blue</span> = Current Version

<span style="color:green">Green</span> = New Version

Rollback is fast and easy

### Rolling deployments

A rolling deployment allows you to make changes in batches and to deploy to only a portion of your environment rather than an all-or-nothing approach

Cost-effective - you can set the batch size and the minimum number of servers to keep in service

Complexity - you have a mixed environment where some servers are on the old version, some are on the new version

### Canary Deployments

Deploy the new version of your application to a small number of web servers

Direct only a small proportion (e.g. 10%) of customer traffic to the new version ("Canary Testing")

Provides an early indication that something is wrong in your application

Rolling back is easy - simply direct all customers back to the original version

### Systems Manager (SSM)

Management tool - gives you visibility and control over your AWS infrastructure at scale

You can automate common operational tasks on groups of instances simultaneously without having to log into each one

Run Command - run operational tasks across multiple EC2 instances (e.g. stop, restart, terminate or re-size instances)

Patch Manager - patch multiple EC2 instances simultaneously