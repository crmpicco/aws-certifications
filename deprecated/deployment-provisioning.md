_The SOA-C01 exam has been deprecated_

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

### ELB Error Messages
* 4xx message - something has gone wrong on the client side
* 5xx message - server side errors

400 - Bad/malformed request

401 - Unauthorized, user access denied

403 - Forbidden, request blocked by WAF ACL

460 - Client closed connection before the ELB could respond

463 - ELB received `X-Forwarded-For` header with > 30 IPs

500 - Internal Server Error

502 - Bad Gateway. Application server closed the connection or sent back a malformed response

503 - Service unavailable, no registered targets

504 - Gateway timeout. Application is not responding

561 - Unauthorized, received an error code from the ID provider when attempting to authenticate a user

### ELB CloudWatch Metrics
ELBs publish metrics to CloudWatch by default for the load balancer itself **and** for the back-end instances.

Metrics are gathered at 60 second intervals

`BackendConnectionErrors` - number of unsuccessful connections to backend instances

`HealthyHostCount` - number of healthy instances registered

`UnHealthyHostCount` - number of unhealthy instances

`Latency` - number of seconds taken for registered instance to respond / connect

`RequestCount` - number of requests completed / connections made during the specified interval

`SurgeQueueLength` - number of pending requests (_Classic Load Balancer only_)

`SpilloverCount` - number of requests rejected because the surge queue is full (_Classic Load Balancer only_)

## Systems Manager (SSM)
A management tool which gives you visibility and control over your AWS infrastructure

Integrates with CloudWatch dashboards

Run Command
* allows you to run pre-defined commands on one or more EC2 instances without needing to log in to each one
* attach/detach EBS volumes
* run a shell script
* run an Ansible playbook

## Placement Groups
Allow you to control how your instances are deployed
* Cluster - instances all created in single AZ
* Partition - instances are created in logical segments called partitions
* Spread - each instance is created in a separate rack with independent network and power