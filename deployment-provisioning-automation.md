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