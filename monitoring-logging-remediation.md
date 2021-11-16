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

CloudWatch agent - allows you to define your own operation system-level metrics

All EC2 instance send key performance and health metrics to CloudWatch

By default, EC2 does **not** send OS-level metrics (e.g. memory usage, processes, free disk space, CPU idle time) to CloudWatch

EC2 sends metric data to CloudWatch in 5 min intervals

Log Events - Event message and time stamp

Log Stream - a sequence of Log Events from the same source

Log Group - a group of log streams that share the same retention, monitoring and access control settings

Metric Filter - filter for specific phrases in your logs (e.g. warnings, errors, HTTP status codes)
