# Monitoring *HealthLake* with Amazon CloudWatch<a name="monitoring-cloudwatch"></a>

You can monitor *HealthLake* using CloudWatch, which collects raw data and processes it into readable, near real\-time metrics\. These statistics are kept for 15 months, so you can use that historical information and gain a better perspective on how your web application or service is performing\. You can also set alarms that watch for certain thresholds, and send notifications or take actions when those thresholds are met\. For more information, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\. 

Metrics are reported for all HealthLake APIs, including the following\.
+ Data Store Management APIs —CreateFHIRDatastore, DeleteFHIRDatastore, DescribeFHIRDatastore, ListFHIRDatastores
+ Import and Export APIs —StartFHIRImportJob, ListFHIRImportJobs, DescribeFHIRImportJob, StartFHIRExportJob, ListFHIRExportJobs, DescribeFHIRExportJob
+ HTTP REST Client and resource management APIs — CreateResource, DeleteResource, GetCapabilities, GetFullHistory, GetHistoryByResourceId, GetHistoryByResourceType, ReadResource, SearchAll, SearchWithGet, SearchWithPost, Transaction, UpdateResource, ValidateExistingResource, ValidateResource, VersionReadResource\. 
+ Tagging APIs — ListTagsForResource, TagResource, UntagResource

The following tables list the metrics and dimensions for *HealthLake*\.

The following metrics are reported\. Each is presented as a frequency count for a user specified data range\.


**Metrics**  

|  Metrics  | Description | 
| --- | --- | 
| Call Count | The number of calls to APIs\. This can be reported either for the account or a specified Data Store\. Units: Count Valid Statistics: Sum, Count Dimensions: Operation, Data Store ID, Data Store type  | 
| Successful Requests | The number of successful API requests\. Units: Count  Valid Statistics: Sum, Average Dimensions: Operation, Data Store ID, Data Store type | 
| User Errors | The number of requests that failed due to user error\. Units: Count  Valid Statistics: Sum, Average Dimensions: Operation, Data Store ID, Data Store type | 
| Server Errors | The number of requests that failed due to server error\. Units: Count  Valid Statistics: Sum, Average Dimensions: Operation, Data Store ID, Data Store type | 
| Throttled Requests | The number of requests that have been throttled\. This metric is not included in user or server errors counts\. Units: Count  Valid Statistics: Sum, Average Dimensions: Operation, Data Store ID, Data Store type  | 
| Latency | The time it took in milliseconds to process the user request\. Unit: Milliseconds Valid statistics: Minimum, Maximum, Average Dimensions: Operation, Data Store ID, Data Store type  | 

The following dimensions are reported\. 


**Dimensions**  

|  Dimensions  | Description | 
| --- | --- | 
| Operation | Which API operation was used | 
| DataStoreID | The Data Store included in the API request | 
| DataStoreType | The type of Data Store \(currently only FHIR R4 is supported\) | 

You can get metrics for HealthLake with the AWS Management Console, the AWS CLI, or the CloudWatch API\. You can use the CloudWatch API through one of the Amazon AWS Software Development Kits \(SDKs\) or the CloudWatch API tools\. The HealthLake console displays graphs based on the raw data from the CloudWatch API\.

You must have the appropriate CloudWatch permissions to monitor HealthLake with CloudWatch\. For more information, see [Authentication and Access Control for Amazon CloudWatch ](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/auth-and-access-control-cw.html)in the Amazon CloudWatch User Guide\.

## Viewing *HealthLake* metrics<a name="viewing-cloudwatch"></a>

**To view metrics \(HealthLake console\)**

1. Sign in to the AWS Management Console and open the [HealthLake console](https://console.aws.amazon.com/healthlake/home)\.

1. From the list of Data Stores, choose the one whose metrics you want to see\.

1. Choose **Monitoring**\. Metrics are displayed in graphs\.

**To view metrics \(CloudWatch console\)**

1. Sign in to the AWS Management Console and open the [CloudWatch console](https://console.aws.amazon.com/cloudwatch/home)\.

1. Choose **Metrics**, choose **All Metrics**, and then choose **AWS/HealthLake**\.

1. Choose the dimension, choose a metric name, then choose **Add to graph**\.

1. Choose a value for the date range\. The metric count for the selected date range is displayed in the graph\.

## Creating an alarm using CloudWatch<a name="alarms-cloudwatch"></a>

A CloudWatch alarm watches a single metric over a specified time period, and performs one or more actions: sending a notification to an Amazon Simple Notification Service \(Amazon SNS\) topic or Auto Scaling policy\. The action or actions are based on the value of the metric relative to a given threshold over a number of time periods that you specify\. CloudWatch can also send you an Amazon SNS message when the alarm changes state\.

CloudWatch alarms invoke actions only when the state changes and has persisted for the period you specify\.

**To view metrics \(CloudWatch console\)**

1. Sign in to the AWS Management Console and open the [CloudWatch console](https://console.aws.amazon.com/cloudwatch/home)\.

1. Choose **Alarms**, and then choose **Create Alarm**\.

1. Choose **AWS/HealthLake**, and then choose a metric\.

1. For **Time Range**, choose a time range to monitor, and then choose **Next**\.

1. Enter a **Name** and **Description**\.

1. For Whenever, choose **>=**, and type a maximum value\.

1. If you want CloudWatch to send an email when the alarm state is reached, in the Actions section, for Whenever this alarm, choose State is **ALARM**\. For Send notification to, choose a mailing list or choose **New list** and create a new mailing list\.

1. Preview the alarm in the Alarm Preview section\. If you are satisfied with the alarm, choose **Create Alarm**\.