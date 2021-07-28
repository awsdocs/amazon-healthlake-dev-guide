# Amazon HealthLake Amazon HealthLake Developer Guide

-----
*****Copyright &copy; Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What is Amazon HealthLake?](what-is-amazon-health-lake.md)
+ [How Amazon HealthLake works](how-healthlake-works.md)
+ [Getting started with Amazon HealthLake](getting-started.md)
   + [Account set up with Amazon HealthLake](getting-started-amazon-health-lake.md)
      + [Set up the AWS Command Line Interface (AWS CLI)](setup-awscli.md)
      + [Creating a FHIR Data Store using the AWS Command Line Interface](healthlake-examples-cli.md)
      + [Creating a FHIR Data Store using the SDK for Python](healthlake-example-boto.md)
      + [Creating a FHIR Data Store using the AWS SDK for Java](healthlake-examples-java.md)
      + [Getting started with an HTTP client](getting-started-with-http.md)
      + [Preloaded datatypes](preloaded-data.md)
+ [Security in Amazon HealthLake](healthlake-security.md)
   + [Data Protection in Amazon HealthLake](data-protection.md)
   + [Encryption at rest for Amazon HealthLake](encryption-at-rest.md)
   + [Encryption in transit for Amazon HealthLake](encryption-in-transit.md)
   + [Identity and Access Management for Amazon HealthLake](security-iam.md)
      + [How Amazon HealthLake works with IAM](security_iam_service-with-iam.md)
      + [Identity-based policy examples for Amazon HealthLake](security_iam_id-based-policy-examples.md)
      + [Troubleshooting Amazon HealthLake identity and access](security_iam_troubleshoot.md)
   + [Logging Amazon HealthLake API Calls with AWS CloudTrail](logging-using-cloudtrail.md)
   + [Compliance Validation for Amazon HealthLake](SERVICENAME-compliance.md)
   + [Resilience in Amazon HealthLake](disaster-recovery-resiliency.md)
   + [Infrastructure Security in Amazon HealthLake](infrastructure-security.md)
   + [Security best practices in Amazon HealthLake](best-practices-security.md)
+ [Amazon HealthLake and interface VPC endpoints (AWS PrivateLink)](vpc-endpoints.md)
+ [Tagging resources in Amazon HealthLake](tagging.md)
   + [Adding a tag to a Data Store](add-a-tag.md)
   + [Listing tags for a Data Store](list-tags.md)
   + [Removing tags from a Data Store](remove-tags.md)
+ [Monitoring HealthLake](monitoring-overview.md)
   + [Monitoring HealthLake with Amazon CloudWatch](monitoring-cloudwatch.md)
+ [Creating and monitoring FHIR Data Stores in Amazon HealthLake](working-with-FHIR-healthlake.md)
   + [Creating a Data Store example](data-store-creation-example.md)
   + [Describing a Data Store example](data-store-describe-example.md)
   + [Listing Data Stores example](data-store-list-example.md)
   + [Deleting a Data Store example](data-store-deleting-example.md)
+ [Managing FHIR resources in Amazon HealthLake](crud-healthlake.md)
   + [Example: Using Create with POST](create-example.md)
   + [Example: Reading a resource with GET](read-example.md)
   + [Example: Updating a resource using PUT](update-example.md)
   + [Example: Deleting a resource](delete-example.md)
+ [Importing files to a FHIR Data Store](import-datastore.md)
   + [Example: Starting and monitoring import jobs using the AWS CLI](import-examples.md)
+ [Exporting files from a FHIR Data Store](export-datastore.md)
   + [Example: Starting export jobs](export-examples.md)
+ [Using FHIR search functionality in Amazon HealthLake](search-healthlake.md)
   + [Using FHIR search in Amazon HealthLake](using-search-healthlake.md)
      + [Supported search parameters and search modifiers in HealthLake](supported-search-healthlake.md)
   + [Search with GET](search-with-get.md)
   + [Search with POST](search-with-post.md)
+ [Integrated medical natural language processing (NLP)](integrated-medical-nlp.md)
+ [Quotas for Amazon HealthLake](limits.md)
+ [Troubleshooting](troubleshooting.md)
   + [Why can't I create a Data Store?](iam-troubleshooting.md)
   + [Exceeded number of Data Stores allowed per account](limits-troubleshooting.md)
   + [How do I create authorization for the FHIR RESTful APIs?](authorization-troubleshooting.md)
   + [My data isn't in FHIR R4 format- can I still use HealthLake?](fhir-troubleshooting.md)
   + [Why did my import fail?](import-troubleshooting.md)
+ [Using Amazon HealthLake for healthcare analytics](healthlake-analytics.md)
+ [Document History for the Amazon HealthLake Developer Guide](doc-history.md)
+ [AWS glossary](glossary.md)