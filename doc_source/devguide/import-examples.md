# Example: Starting and monitoring import jobs using the AWS CLI<a name="import-examples"></a>

 The following example shows how to use the AWS CLI to start and monitor an import job\. You can also use the [start\-fhir\-import\-job API](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_StartFHIRImportJob.html) or the console\. 

```
aws healthlake start-fhir-import-job \
--input-data-config S3Uri=s3://inputS3Bucket/inputFolder/ \
--datastore-id (Datastore ID) \
--data-access-role-arn "arn:aws:iam::012345678910:role/DataAccessRole" \
--job-output-data-config '{"S3Configuration": {"S3Uri":"s3://outputS3Bucket/healthlake-output","KmsKeyId":"arn:aws:kms:us-east-1:012345678910:key/d330e7fc-b56c-4216-a250-f4c43ef46e83"}}' \
--region us-east-1
```

When the import job begins, you'll receive the following confirmation\.

```
{
 "JobId": "8a4077553e9a485ad889c1a89c7541f0",
 "JobStatus": "SUBMITTED",
 "DatastoreId": "32839038a2f47f17c2fe0f53f0c3a0ba"
}
```

To monitor the status of an import job or to learn its configuration properties, use the [describe\-fhir\-import\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DescribeFHIRImportJob.html) API or the AWS CLI command as shown in the following example\.

```
    aws healthlake describe-fhir-import-job \
    --datastore-id (Datastore ID) \
    --job-id c145fbb27b192af392f8ce6e7838e34f \
    --region us-east-1
```

 You receive the following information in response\.

```
{
    "ImportJobProperties": {
    "InputDataConfig": {
    "S3Uri": "s3://(Bucket Name)/(Prefix Name)/"
    }, 
    "DataAccessRoleArn": "arn:aws:iam::(AWS Account ID):role/(Role Name)", 
    "JobStatus": "COMPLETED", 
    "JobId": "c145fbb27b192af392f8ce6e7838e34f", 
    "SubmitTime": 1606272542.161, 
    "EndTime": 1606272609.497, 
    "DatastoreId": "(Datastore ID)"
    }
}
```

To see a list of all import jobs, use the [list\-fhir\-import\-jobs](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_ListFHIRImportJobs.html) API or the AWS CLI command as shown in the following example\. Users can add one or more filters to limit the results as shown\.

```
    aws healthlake list-fhir-import-jobs\ 
    --datastore-id (Datastore ID) \
    --submitted-before (DATE like 2024-10-13T19:00:00Z)\
    --submitted-after (DATE like 2020-10-13T19:00:00Z )\
    --job-name "FHIR-IMPORT" \
    --job-status SUBMITTED  \
    --max-results (Integer between 1 and 500)
```

 You receive the following information in response\.

```
{
    "ImportJobProperties": {
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
    "JobName" "FHIR-IMPORT",
    "SubmitTime": 1606272542.161, 
    "EndTime": 1606272609.497, 
    "DatastoreId": "(Datastore ID)"
    }
} 
"NextToken": String
```