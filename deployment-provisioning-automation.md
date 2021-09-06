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
* Burstable up to 250MB/s per TB
* Used for Big Data, ETL and log processing

sc1 - Cold HDD
* Lowest cost option
* Baseline throughput of 12 MB/s per TB
* Burstable up to 80MB/s per TB
* Used when performance is not a factor
* Cannot be a boot volume

## What is a Bastion Host?

Public-facing instance which enables you to SSH or RDP to your private instances from an untrusted network

Located in a public subnet and is reeachable from the internet

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