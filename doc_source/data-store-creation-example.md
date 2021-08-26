# Creating a Data Store example<a name="data-store-creation-example"></a>

The following example demonstrates how to create a Data Store using the AWS Command Line Interface You can also use either the console or the [create\-fhir\-datastore API](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_CreateFHIRDataStore.html) to create a Data Store\. When you create your Data Store, encryption at rest defaults to an AWS\-owned KMS key unless specified otherwise\. 

```
    aws healthlake create-fhir-datastore \
    --datastore-type-version R4 \ 
    --sse-configuration '{"KmsEncryptionConfig": {"CmkType":"CUSTOMER_MANAGED_KMS_KEY","KmsKeyId":"KMS_KEY_ID_OR_ARN_OR_ALIAS"}}'
    --preload-data-config PreloadDataType="SYNTHEA" \ 
    --datastore-name "FhirTestDatastore"
```

The JSON response includes the Data Store ID, Amazon Resource Name \(ARN\), and confirmation that the Data Store is being created\. When the Data Store is ready to ingest data, the status is `"ACTIVE"`\. The following is the example JSON response\.

```
{
    "DatastoreEndpoint": "https://healthlake.us-east-1.amazonaws.com/datastore/(Datastore ID)/r4/", 
    "DatastoreArn": "arn:aws:healthlake:us-east-1:(AWS Account ID):datastore/(Datastore ID)", 
    "DatastoreStatus": "CREATING", 
    "DatastoreId": "(Datastore ID)"
}
```