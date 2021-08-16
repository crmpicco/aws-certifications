# Deployment & Provisioning

## EC2 Launch Issues
* `InstanceLimitExceeded` - you have reached the limit on the number of instances you can launch in a region. There is a 20 limit per region default. You can request an increase.
* `InsufficientInstanceCapacity` - AWS does not currently have enough available on-demand capacity to service your request.

## EBS Volumes & IOPS
### EBS SSD IOPS
* gp2 - General Purpose, boot volumes
* io1 - Provisioned IOPS (Input Output Operations/Second), I/O intensive

Problem: I/O requests will start queueing if you are using gp2 and your workload exceeds the IOPS limit of the gp2 volume

Potential solutions:
* For gp2, increase the size of your volume
* Change your storage class to Provisioned IOPS

## Bastion Hosts
Bastion Host is a host located in your public subnet which you connect to over the internet.

Allows you to connect to your EC2 instances using SSH or RDP

Allows you to safely administer your EC2 instances without exposing them to the internet

Ports should be limited to SSH and RDP access

## Elastic Load Balancers (ELB)

### Application Load Balancer (ALB)
* Content/route-based 
* Layer 7
* Application-aware
* You can send specific requests to specific web servers

### Network Load Balancer (NLB)
* Layer 4, transport-layer
* For super-fast, extreme performance
* Most expensive
* Capable of handling millions of requests per second

### Classic Load Balancer (CLB)
* Legacy, not recommended
* You can load balance at layer 4 and 7
* Features are basic, e.g. `X-Forwarded-For` headers and sticky sessions

Pre-warm your load balancers to avoid overloading your ELB. Pre-warming will configure the ELB to the appropriate level of capacity based on the traffic that you expect.