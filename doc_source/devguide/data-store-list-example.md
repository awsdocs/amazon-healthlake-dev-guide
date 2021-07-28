# Listing Data Stores example<a name="data-store-list-example"></a>

Use the [list\-fhir\-datastore](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_ListFHIRDataStore.html) API or the console to find the names, properties, and statuses of the Data Stores associated with your account as shown in the following example\. You can also set filters to focus your listings to `'ACTIVE'` Data Stores only, as shown in the example\.

```
aws healthlake list-fhir-datastores 
    --region us-east-1 
    --filter DatastoreStatus=ACTIVE
```

The following is the response in JSON\.

```
 
{            
     "DatastorePropertiesList": [
    {
        "PreloadDataConfig": {
            "PreloadDataType": "SYNTHEA"
        }, 
        "DatastoreName": "FhirTestDatastore", 
        "DatastoreArn": "arn:aws:healthlake:us-east-1:(AWS Account ID):datastore/(Datastore ID)", 
        "DatastoreEndpoint": "https://healthlake.us-east-1.amazonaws.com/datastore/(Datastore ID)/r4/", 
        "DatastoreStatus": "ACTIVE", 
        "DatastoreTypeVersion": "R4", 
        "CreatedAt": 1605574003.209, 
        "DatastoreId": "(Datastore ID)"
    }, 
    {
        "DatastoreName": "Demo", 
        "DatastoreArn": "arn:aws:healthlake:us-east-1:(AWS Account ID):datastore/(Datastore ID)", 
        "DatastoreEndpoint": "https://healthlake.us-east-1.amazonaws.com/datastore/(Datastore ID)/r4/", 
        "DatastoreStatus": "ACTIVE", 
        "DatastoreTypeVersion": "R4", 
        "CreatedAt": 1603761064.881, 
        "DatastoreId": "(Datastore ID)"
    } 
    ]
}
```