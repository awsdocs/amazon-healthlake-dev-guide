# Creating a FHIR Data Store using the AWS Command Line Interface<a name="healthlake-examples-cli"></a>

The following example demonstrates using the `CreateFHIRDatastore` operation with the AWS CLI\. To run the example, you must install the AWS CLI\.

The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

```
​aws healthlake create-fhir-datastore \
    --datastore-type-version R4 \ 
    --preload-data-config PreloadDataType="SYNTHEA" \ 
    --datastore-name "FhirTestDatastore"
```