# Quotas for Amazon HealthLake<a name="limits"></a>

## Throttling and quotas for Amazon HealthLake<a name="throtting"></a>

The following table describes throttling limits for resource management within Amazon HealthLake for each customer account\. For information about limits that can be changed, see [AWS Service Limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\. For all operations, users will receive a `ThrottlingException` error message if throttling limits are exceeeded\. 

A maxmimum quota of ten Data Stores are allowed per an account\. For information about requesting a quota increase, see [the console support center](https://console.aws.amazon.com/support/home#/) [to create a case](https://console.aws.amazon.com/support/home?#/case/create)\.


| Description | Limit in Transactions per second\(TPS\) or requests per minute | 
| --- | --- | 
| CreateFHIRDatastore and DeleteFHIRDatastore | 1 request per minute | 
| DescribeFHIRDatastore | 10 TPS | 
| ListFHIRDatastores | 10 TPS | 
| CreateResource, ReadResource, DeleteResource | 20 TPS | 
| UpdateResource | 100 TPS | 
| GetCapabilities | 10 TPS | 
| SearchWithGet and SearchWithPost | 100 TPS | 
| StartFHIRImportJob and StartFHIRExportJob | 1 request per minute, only 1 job permitted at a time | 
| DescribeFHIRImportJob, DescribeFHIRExportJob, ListFHIRImportJob, FistFHIRExportJob | 10 TPS | 
| ListFHIRImportJobs, FistFHIRExportJobs | 10 TPS | 
| TagResource, UntagResource, ListTagsforResource | 10 TPS | 
| Maximum characters for a medical note within the DocumentReference ResourceType \(CreateResource/UpdateResource\) | 40,000 characters | 

## <a name="quotas-for-import-jobs"></a>

The following table lists the quotas for `Import` jobs\. 


| Description | Limit | 
| --- | --- | 
| Maximum import job size  | 50 GB | 
| Maximum import file size | 50 MB | 
| Maximum number of files | 10,000 | 
| Supported file extension | '\.ndjson' | 