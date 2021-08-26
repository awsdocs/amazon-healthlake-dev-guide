# Deleting a Data Store example<a name="data-store-deleting-example"></a>

To delete a data store and all information in it, use the `DeleteFHIRDataStore` command using the AWS CLI as shown in the following example\. You can also delete a data store using the [delete\-fhir\-datastore API](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DeleteFHIRDataStore.html) or the console\. Deleting a Data Store removes all of the FHIR resource versions contained within the Data Store and the underlying infrastructure\. Logs related to a deleted Data Store are retained within the service account in accordance with HIPAA guidelines\.

Deleting a Data Store is an asynchronous operation\. When you start deleting a Data Store, the Data Store status changes to `DELETING`\. It remains in the `DELETING` state until all of the FHIR data from the Data Store is removed along with the underlying infrastructure necessary to support the data\. Once the data and infrastructure are removed, the status of the Data Store changes to `DELETED`\. After deletion, the Data Store appears in the `DescribeFHIRDataStore` and `ListFHIRDataStores` operations for seven days\. After seven days the Data Store will no longer appear in the results\.

```
aws healthlake delete-fhir-datastore 
    --datastore-id (Data Store ID)
```

As shown in the following example JSON response, the status changes to "`DELETING`" to confirm that the Data Store and its contents are in the process of being deleted\.

```
{ 
    "DatastoreEndpoint": "https://healthlake.us-east-1.amazonaws.com/datastore/(Datastore ID)/r4/", 
    "DatastoreArn": "arn:aws:healthlake:us-east-1:(AWS Account ID):datastore/(Datastore ID)", 
    "DatastoreStatus": "DELETING", 
    "DatastoreId": "(Datastore ID)"
}
```