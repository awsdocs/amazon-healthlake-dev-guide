# Exporting files from a FHIR Data Store<a name="export-datastore"></a>

After your data is imported to a Data Store, you can export files to an Amazon Simple Storage Service \(Amazon S3\) bucket for analysis or downstream applications using other AWS services\. Amazon HealthLake exports files in newline delimited JSON \(\.ndjson\) format, where each line consists of a valid FHIR resource\. A customer\-owned KMS key is required for encryption of the Amazon S3 bucket for all export jobs\. To learn more about creating a KMS key, see [Creating keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) in the AWS Key Management Service developer guide\. 

 Only one import or export job can run at time for an active Data Store\. However, users can create, read, update, or delete FHIR resources while an export job is in progress\.

## Performing an export<a name="export-healthlake"></a>

You can start an export job using either the Amazon HealthLake console or the Amazon HealthLake export API, [start\-fhir\-export\-job API](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_StartFHIRExportJob.html)\.

### Exporting from your Data Store<a name="performing-export-api"></a>

**Prerequisites**

To use Amazon HealthLake APIs, you must create an AWS Identity Access and Management \(IAM\) policy and attach it to an IAM role\. To learn more about IAM roles and trust policies, see [IAM Policies and Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)\. 

**To export files**

1. Create an S3 bucket\. The Amazon S3 bucket must be in the same AWS region as the service, and BlockPublicAccess must be turned on for all options\. To learn more, see [Using Amazon S3 block public access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html)\. An Amazon\-owned or customer\-owned KMS key must also be used for encryption\. To learn more about using KMS keys, see [Amazon Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)\. 

1. Create and add an IAM policy to allow the user to create and attach roles and policies\. The following is an example\. 

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
         {
            "Action": [
               "iam:CreateRole",
               "iam:CreatePolicy",
               "iam:AttachRolePolicy",
               "iam:PassRole",
               "healthlake:*"
            ],
            "Effect": "Allow",
            "Resource": "*"
         }
      ]
   }
   ```

1. Create a data access role\. HealthLake uses this to write the output Amazon S3 bucket\.

1. Add a trust policy to the data access role\. The following is an example trust policy\.

   ```
    
    "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {
           "Service": [
             "healthlake.amazonaws.com"
           ]
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

1. Add a permission policy to the data access role that enables the role to access the S3 bucket\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Action": [
                   "s3:ListBucket",
                   "s3:GetBucketPublicAccessBlock",
                   "s3:GetEncryptionConfiguration"
               ],
               "Resource": [
                   "arn:aws:s3:::outputS3Bucket"
               ],
               "Effect": "Allow"
           },
           {
               "Action": [
                   "s3:PutObject"
               ],
               "Resource": [
                   "arn:aws:s3:::outputS3Bucket/*"
               ],
               "Effect": "Allow"
           },
           {
               "Action": [
                   "kms:DescribeKey",
                   "kms:GenerateDataKey*"
               ],
               "Resource": [
                   "arn:aws:kms:us-east-1:012345678910:key/d330e7fc-b56c-4216-a250-f4c43ef46e83"
               ],
               "Effect": "Allow"
           }
       ]
   }
   ```

1. Use the [start\-fhir\-export\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_StartFHIRexportJob.html) operation to begin a bulk export job\.

1. To get the ID, ARN, name, start time, end time, and current status of a FHIR export job, use [describe\-fhir\-export\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DescribeFHIRexportJob.html)\. Use [list\-fhir\-export\-jobs](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_ListFHIRexportJobs.html) to list all export jobs and their statuses\. 

### Exporting files \(console\)<a name="export-api-console"></a>

**To export files \(console\)**

1. Create an output S3 bucket in the same region as HealthLake\.

1. To start a new export job, identify the output Amazon S3 bucket and either create or identify the IAM role that you want to use\. To learn more about IAM roles and trust policies, see [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)\. An Amazon\-owned or customer\-owned KMS key must also be used for encyrption\. To learn more about using KMS keys, see [Amazon Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)\. 

1. Monitor the status of your job\. The console shows the status of all exports that are in progress\.