![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Amazon_Web_Services_Logo.svg/300px-Amazon_Web_Services_Logo.svg.png "AWS")

# AWS Certified SysOps Administrator - Associate

## CloudWatch
Monitoring service to monitor AWS resources and applications run on AWS

You can retrieve data using `GetMetricStatistics` API

You can store log data in CloudWatch Logs for as long as you want. Stored indefinitely by default.

Custom metrics - minimum granularity is 1 minute

Standard monitoring - 5 minute metric granularity

Host Level metrics: CPU, Network, Disk, Status Check

Can be used on premise

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