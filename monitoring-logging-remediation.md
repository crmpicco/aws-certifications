# Monitoring, Logging & Remediation

## CloudWatch
Monitoring services to monitor the health and performance of your AWS resources

Monitors:
* Compute
* Database and Analytics
* Storage and Content Delivery
* SNS topics, SQS queues, API gateway etc

Default EC2 host-level metrics:

* CPU
* Network
* Disk
* Status check

CloudWatch agent - allows you to define your own metrics

All EC2 instance send key performance and health metrics to CloudWatch

By default, EC2 does **not** send OS-level metrics (e.g. memory usage, processes, free disk space, CPU idle time) to CloudWatch

EC2 sends metric data to CloudWatch in 5 min intervals
