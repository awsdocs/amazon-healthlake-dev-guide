# Describing a Data Store example<a name="data-store-describe-example"></a>

To learn the properties of a Data Store, use the[ describe\-fhir\-datastore API](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DescribeFHIRDataStore.html), the console, or the AWS CLI command as shown in the following example\.

```
aws healthlake describe-fhir-datastore \
    --datastore-id "1f2f459836ac6c513ce899f9e4f66a59" \
    --region us-east-1
```

In the JSON response, you can learn the ` DatastoreName `, `DatastoreArn(ARN)`, `DatastoreEndpoint`, `DatastoreStatus`, `DatastoreTypeVersion`, and `DatastoreId`, as shown in the following example\.

```
{
    "DatastoreProperties": {
        "PreloadDataConfig": {
            "PreloadDataType": "SYNTHEA"
        }, 
        "DatastoreName": "FhirTestDatastore", 
        "DatastoreArn": "arn:aws:healthlake:us-east-1:(AWS Account ID):datastore/(Datastore ID)", 
        "DatastoreEndpoint": "https://healthlake.us-east-1.amazonaws.com/datastore/(Datastore ID)/r4/", 
        "DatastoreStatus": "CREATING", 
        "DatastoreTypeVersion": "R4", 
        "DatastoreId": "(Datastore ID)"
    }
}
```