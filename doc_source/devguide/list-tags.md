# Listing tags for a Data Store<a name="list-tags"></a>

Follow these steps to use the AWS CLI to view a list of the AWS tags for a HealthLake Data Store\. If no tags have been added, the returned list is empty\.

 At the terminal or command line, run the list\-tags\-for\-resource command as shown in the following example\.

```
aws healthlake-test list-tags-for-resource --resource-arn "arn:aws:healthlake:us-east-1:674914422125:datastore/fhir/0725c83f4307f263e16fd56b6d8ebdbe" --region us-east-1 
```

```
{
    "tags": {
        "key": "value",
        "key1": "value1"
    }
}
```