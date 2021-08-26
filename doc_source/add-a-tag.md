# Adding a tag to a Data Store<a name="add-a-tag"></a>

Adding tags to a Data Store can help you identify and organize your AWS resources and manage access to them\. First, you add one or more tags \(key\-value pairs\) to a Data Store\. You can use up to fifty tags per user\. There are also restrictions on the characters you can use in the key and value fields\. 

After you have tags, you can create IAM policies to manage access to the Data Store based on these tags\. You can use the the HealthLake console or the AWS CLI to add tags to a Data Store\. Adding tags to a repository can impact access to that repository\. Before you add a tag to a Data Store, make sure to review any IAM policies that might use tags to control access to resources such as Data Stores\.

Follow these steps to use the AWS CLI to add a tag to a HealthLake Data Store\. To add a tag to a Data Store when you create it, see [Creating and monitoring FHIR resources](working-with-FHIR-healthlake.md#data-store-management)\.

At the terminal or command line, run the tag\-resource command, specifying the Amazon Resource Name \(ARN\) of the Data Store where you want to add tags and the key and value of the tag you want to add\. You can add more than one tag to a Data Store\. There are also restrictions on the characters you can use in the key and value fields, as listed in [Tagging requirements](tagging.md#tagging-requirements)For example, to add tags to a Data Store while it is being created, you would use the following command in the AWS CLI\. The name of the Data Store is Test\_Data\_Store, and the two added tags with keys are key1 and key2 with values as value1 and value2 respectively :

```
aws healthlake create-fhir-datastore --datastore-type-version R4 --preload-data-config PreloadDataType="SYNTHEA" --datastore-name "Test_Data_Store" --tags '[{"Key": "key1", "Value": "value1"}, {"Key": "key2", "Value": "value2"}]' --region us-east-1 
```

To add tags to an existing Data Store, you would run the following example command:

```
aws healthlake tag-resource --resource-arn "arn:aws:healthlake:us-east-1:691207106566:datastore/fhir/0725c83f4307f263e16fd56b6d8ebdbe" --tags '[{"Key": "key1", "Value": "value1"}]' --region us-east-1 
```

If successful, this command returns no response\.