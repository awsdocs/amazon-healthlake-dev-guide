# Creating and monitoring FHIR Data Stores in Amazon HealthLake<a name="working-with-FHIR-healthlake"></a>

## Important notice<a name="important-notice"></a>

Amazon HealthLake protects customer data under the AWS Shared Responsibility Model policies\. Remember that customer\-inputed names should never contain personally identifiable information \(PII\) or protected health information \(PHI\)\. For more information, see the HealthLake Security chapter\.

## Creating and monitoring FHIR resources<a name="data-store-management"></a>

With Amazon HealthLake, you can create and manage Data Stores for storing FHIR resources\. Use the following operations to create and monitor the Data Store:
+ **CreateFHIRDataStore** – Creates a Data Store that can ingest and export FHIR data\.
+ **DescribeFHIRDataStore** – Gets the properties associated with the FHIR datastore, including Data Store ID, Data Store Arn, Data Store name, Data Store status, created at, Data Store type version, and Data Store endpoint\. These items are used in subsequent operations\.
+ **ListFHIRDataStores** – Lists all FHIR Data Stores that are in the user’s account, regardless of Data Store status\. 
+ **DeleteFHIRDataStores** – Deletes a FHIR Data Store and all of the data included within\. 