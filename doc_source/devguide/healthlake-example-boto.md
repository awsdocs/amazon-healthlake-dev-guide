# Creating a FHIR Data Store using the SDK for Python<a name="healthlake-example-boto"></a>

The following example demonstrates using the `CreateFHIRDatastore` operation using the AWS SDK for Python\.

```
import boto3
healthlake = boto3.client(service_name='healthlake',
                          region_name='us-east-1',
                          use_ssl=True)
DataStore_type_version = "R4"
DataStore_name = "TestDatastore123"
preload_type = "SYNTHEA"
preload_option = {'PreloadDataType': preload_type}
print('Calling CreateFHIRDatastore\n')
create_response = healthlake.create_fhir_datastore(
    DatastoreTypeVersion=DataStore_type_version,
    DatastoreName=DataStore_name,
    PreloadDataConfig=preload_option)
print("Create FHIR Datastore response: \n", create_response)
print('End of CreateFHIRDatastore\n')
```