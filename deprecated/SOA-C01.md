<span style="display:block; text-align:center">![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Amazon_Web_Services_Logo.svg/300px-Amazon_Web_Services_Logo.svg.png "AWS")</span>

_The SOA-C01 exam has been deprecated_

# AWS Certified SysOps Administrator - Associate (SOA-C01)

# Monitoring & Reporting

## CloudWatch
Monitoring service to monitor performance of AWS resources and applications run on AWS

You can retrieve data using `GetMetricStatistics` API

You can store log data in CloudWatch Logs for as long as you want. Stored indefinitely by default.

### Metric Granularity
1 minute for detailed monitoring
5 minutes for standard monitoring

Host Level metrics: CPU, Network, Disk, Status Check

Can be used on premise

Dashboards are multi-region and can display any widget to any region.

Host Level Metrics:
* CPU
* Network
* Disk
* Status Check

### EBS
`VolumeReadOps`/`VolumeWriteOps` = Total number of IO Ops in a specific period of time
`VolumeQueueLength` - The number of read and write operations requests waiting to be completed in a specified period of time

Volume statuses:

* `ok`
* `warning`
* `impaired`
* `insufficient-data`

### ELB

Access logs - capture detailed information about requests sent to your load balancer.
They can store data where the EC2 instance has been deleted.

### Elasticache

#### Memcached
* Multi-threaded
* Can handle loads of up to 90%
* SwapUsage should be around 0 most of the time and should not exceed 50MB.
* Scale up OR out

#### Redis
* Not multi-threaded
* No SwapUsage metric
* Scale out only (by adding read replicas)

Swap File - the amount of disk storage space reserved on disk if your computer runs out of RAM.

Swap Usage - the amount of the Swap file that is used

Eviction - occurs when a new item is added and an old item mist be removed due to a lack of free space in the system

Concurrent connections - set and alarm on this number

## AWS Organizations

### Central Management
Allows you to manage multiple AWS accounts at once. You can create groups of accounts and then apply policies to those groups.

### Control Access
Create Service Control Policies (SCPs) that centrally control AWS service use across multiple AWS accounts. SCP will override IAM.

### Automate AWS Account Creation

### Consolidated Billing
Allows you to set up a single payment method for all the AWS accounts in your organization

## Tagging & Resource Groups

Tags - Key Value Pairs attached to AWS resources. Case sensitive.

Resource Group - a way to group your tags. They make it easy to group your resources using the tags that are assigned to them.
They contain information such as region, name, health checks.

## Cost Explorer & Cost Allocation Tags
### Cost Explorer 
* a tool that enables you to view and analyze your costs and usage
* use tags to tag your resources
* active 'Cost Allocation Tags'
* you can view data for up to the last 13 months

## AWS Config
Fully managed service that provides you with an AWS resource inventory, configuration history and config change notifications
Enables:
* Compliance auditing
* Security analysis
* Resource tracking

Provides:
* Config snapshots and logs config changes
* Automated compliance checking

AWS Config requires an IAM role with read only permissions to the recorded resources

## Health Dashboards
* [Service Health Dashboard](https://status.aws.amazon.com/)
* Personal Health Dashboard
