# Example: Starting export jobs<a name="export-examples"></a>

 The following example shows how to use the AWS CLI to start and monitor an export job\. You can also use the [start\-fhir\-export\-job API](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_StartFHIRExportJob.html) or the console\. 

```
aws healthlake start-fhir-export-job \
--datastore-id b35525cfbd0672ed444bd191aeaa558e \
--data-access-role-arn "arn:aws:iam::012345678910:role/Dummy" \
--output-data-config '{"S3Configuration": {"S3Uri":"s3://outputS3Bucket/healthlake-output","KmsKeyId":"arn:aws:kms:us-east-1:012345678910:key/d330e7fc-b56c-4216-a250-f4c43ef46e83"}}' \
--region us-east-1
```

You receive the following confirmation that the export job has begun\.

```
{
    "DatastoreId": "(Datastore ID)", 
    "JobStatus": "SUBMITTED", 
    "JobId": "9b9a51943afaedd0a8c0c26c49135a31"
}
```

To monitor the status of an export job or to check its configuration properties, use the [describe\-fhir\-export\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DescribeFHIRExportJob.html) API or the AWS CLI command as shown in the following example\.

```
aws healthlake describe-fhir-export-job \
    --datastore-id (Datastore ID) \
    --job-id 9b9a51943afaedd0a8c0c26c49135a31
```

 You receive the following information in response\.

```
{
    "ExportJobProperties": {
        "DataAccessRoleArn": "arn:aws:iam::(AWS Account ID):role/(Role Name)", 
        "JobStatus": "IN_PROGRESS", 
        "JobId": "9009813e9d69ba7cf79bcb3468780f16", 
        "SubmitTime": 1609175692.715, 
        "OutputDataConfig": {
            "S3Uri": "s3://(Bucket Name)/(Prefix Name)/59593b2d0367ce252b5e66bf5fd6b574-FHIR_EXPORT-9009813e9d69ba7cf79bcb3468780f16/"
        }, 
        "DatastoreId": "(Datastore ID)"
    }
}
```

To see a list of all export jobs, use the [list\-fhir\-export\-jobs](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_ListFHIRExportJobs.html) API or the AWS CLI command as shown in the following example\.

```
    aws healthlake list-fhir-export-jobs\ 
    --datastore-id (Datastore ID) \
    --submitted-before (DATE like 2024-10-13T19:00:00Z)\
    --submitted-after (DATE like 2020-10-13T19:00:00Z )\
    --job-name "FHIR-EXPORT" \
    --job-status SUBMITTED  \
    --max-results (Integer between 1 and 500)
```

 You receive the following information in response\.

```
 
{
    "ExportJobProperties": {
    "OutputDataConfig": {
    "S3Uri": "s3://(Bucket Name)/(Prefix Name)/",
    "S3Configuration": {
     "S3Uri": "s3://(Bucket Name)/(Prefix Name)/",
     "KmsKeyId" : "(KmsKey Id)"
     },
    }, 
    "DataAccessRoleArn": "arn:aws:iam::(AWS Account ID):role/(Role Name)", 
    "JobStatus": "COMPLETED", 
    "JobId": "c145fbb27b192af392f8ce6e7838e34f", 
    "JobName" "FHIR-EXPORT",
    "SubmitTime": 1606272542.161, 
    "EndTime": 1606272609.497, 
    "DatastoreId": "(Datastore ID)"
    }
} 
"NextToken": String
```