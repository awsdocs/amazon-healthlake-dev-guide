# Removing tags from a Data Store<a name="remove-tags"></a>

 You can remove one or more tags associated with a Data Store\. Removing a tag does not delete the tag from other AWS resources that are associated with that tag\.

 At the terminal or command line, run the untag\-resource command, specifying the Amazon Resource Name \(ARN\) of the Data Store where you want to remove tags and the tag key of the tag you want to remove\.

```
aws healthlake untag-resource --resource-arn "arn:aws:healthlake:us-east-1:674914422125:datastore/fhir/b91723d65c6fdeb1d26543a49d2ed1fa" --tag-keys '["key1"]' --region us-east-1 
```

If successful, this command does not return a response\. To verify the tags associated with the Data Store, run the list\-tags\-for\-resource command\.