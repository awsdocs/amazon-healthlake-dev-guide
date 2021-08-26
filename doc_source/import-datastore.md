# Importing files to a FHIR Data Store<a name="import-datastore"></a>

After your FHIR Data Store has been created, you can import files from an Amazon Simple Storage Service \(Amazon S3\) bucket\. You can use the console to create and manage import jobs, or use the import APIs\. Amazon HealthLake accepts input files in newline delimited JSON \(\.ndjson\) format, where each line consists of a valid FHIR resource\. The APIs start, describe, and list ongoing import jobs\. A customer\-owned or AWS\-owned KMS key is required for encryption of the Amazon S3 bucket for all import jobs\. To learn more about creating and using a KMS Keys, see [Creating keys](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) in the AWS Key Management Service developer guide\.

 Only one import or export job can run at time for an active Data Store\. However, users can create, read, update, or delete FHIR resources while an import job is in progress\. 

For each import job, output files are generated for successess or failures that can be analyzed via the Manifest\.json file\. Users can programatically navigate to these output files, and they are organized into two folders named SUCCESS and FAILURE\. An output file is generated for each file in the import job\. Because the output files may contain sensitive information, users are required to provide both an output Amazon S3 bucket and a KMS key for encryption\.

The following is an example of the output Manifest\.json file\. It is recommended users look at the file as the first step of troubleshooting a failed import job because it provides details on each file and what caused the import job to fail\.

```
  {
  "inputDataConfig": {
    "s3Uri": "s3://inputS3Bucket/healthlake-input/invalidInput/"
  },
  "outputDataConfig": {
    "s3Uri": "s3://outputS3Bucket/32839038a2f47f17c2fe0f53f0c3a0ba-FHIR_IMPORT-19dd7bb7bcc8ee12a09bf6d322744a3d/",
    "encryptionKeyID": "arn:aws:kms:us-west-2:123456789012:key/fbbbfee3-20b3-42a5-a99d-c48c655ed545"
  },
  "successOutput": {
    "successOutputS3Uri": "s3://outputS3Bucket/32839038a2f47f17c2fe0f53f0c3a0ba-FHIR_IMPORT-19dd7bb7bcc8ee12a09bf6d322744a3d/SUCCESS/"
  },
  "failureOutput": {
    "failureOutputS3Uri": "s3://outputS3Bucket/32839038a2f47f17c2fe0f53f0c3a0ba-FHIR_IMPORT-19dd7bb7bcc8ee12a09bf6d322744a3d/FAILURE/"
  },
  "numberOfScannedFiles": 1,
  "numberOfFilesImported": 1,
  "sizeOfScannedFilesInMB": 0.023627,
  "sizeOfDataImportedSuccessfullyInMB": 0.011232,
  "numberOfResourcesScanned": 9,
  "numberOfResourcesImportedSuccessfully": 4,
  "numberOfResourcesWithCustomerError": 5,
  "numberOfResourcesWithServerError": 0
}
```

## Performing an import<a name="import-healthlake"></a>

You can start an import job using either the Amazon HealthLake console or the Amazon HealthLake import API, [start\-fhir\-import\-job API](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_StartFHIRImportJob.html)\.

## Importing files using the APIs<a name="performing-import-api"></a>

**Prerequisites**

When you use the Amazon HealthLake APIs, you must first create an AWS Identity Access and Management \(IAM\) policy and attach it to an IAM role\. To learn more about IAM roles and trust policies, see [IAM Policies and Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)\. Customers must also use a KMS key for encryption\. To learn more about using KMS Keys, see [Amazon Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)\.

**To import files \(API\)**

1. Upload your data into an Amazon S3 bucket\.

1. To start a new import job, use the `start-FHIR-import-job` operation\. When you start the job, tell HealthLake the name of the Amazon S3 bucket that contains the input files, the KMS key you wish to use for encryption, and the output data configuration\.

1. To learn more about a FHIR import job, use the [describe\-fhir\-import\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DescribeFHIRImportJob.html) operation to get the job's ID, ARN, name, start time, end time, and current status\. Use [list\-fhir\-import\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_ListFHIRImportJob.html) to show all import jobs and their statuses\.

## Importing files using the console<a name="import-api-console"></a>

**To import files \(console\)**

1. Upload your data into an Amazon S3 bucket\.

1. To start a new import job, identify the Amazon S3 bucket and either create or identify the IAM role and the KMS key you want to use\. To learn more about IAM roles and trust policies, see [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)\. To learn more about using KMS Keys, see [Amazon Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)\.

1. Monitor the status of your job\. The console shows the status of all imports that are in progress\.

## IAM policies for import jobs<a name="import-iam"></a>

The IAM role that calls the Amazon HealthLake APIs must have a policy that grants access to the Amazon S3 buckets containing the input files\. It must also be assigned a trust relationship that enables HealthLake to assume the role\. To learn more about IAM roles and trust policies, see [IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)\.

The role must have the following policy:

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
                "arn:aws:s3:::inputS3Bucket",
                "arn:aws:s3:::outputS3Bucket"
            ],
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::inputS3Bucket/*"
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

The role must have the following trust relationship\.

```
{
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