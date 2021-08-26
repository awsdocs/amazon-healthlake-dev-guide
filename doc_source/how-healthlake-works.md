# How Amazon HealthLake works<a name="how-healthlake-works"></a>

Amazon HealthLake maintains Data Stores of health records in FHIR\-compliant format\. You can perform the following tasks using the Amazon HealthLake console, AWS Command Line Interface \(AWS CLI\), or APIs: 
+  Create, monitor, and delete a Data Store
+  Import your data from an Amazon Simple Storage Service \(Amazon S3\) bucket into the Data Store
+  Query data using `Create`, `Read`, `Update`, and `Delete` functions
+  Use FHIR search functionality
+  Transform your data using integrated medical natural language processing \(NLP\)

## Creating and monitoring Data Stores<a name="data-store-creation"></a>

 With Amazon HealthLake, you can create and manage Data Stores for storing R4 FHIR Resources\. Use [create\-fhir\-datastore](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_CreateFHIRDatastore.html) to create a new Data Store, [describe\-fhir\-datastore](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DescribeFHIRDatastore.html) to learn more about the properties of a Data Store, and [list\-fhir\-datastore](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_ListFHIRDatastore.html) to see all Data Stores associated with your account and their status\. When a Data Store is no longer needed, you can delete it using [delete\-fhir\-datastore](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DeleteFHIRDatastore.html)\.

## Create, Read, Update, Delete \(CRUD\) operations<a name="crud-api"></a>

Manage and query data using the `CreateResource`, `ReadResource`, `UpdateResource`, and `DeleteResource` operations for 71 different FHIR resource types\. For a list of FHIR resource types supported by , see [Managing FHIR resources](crud-healthlake.md#fhir-rest-api)\. These operations are all handled through an HTTP client\. 

## Integrated medical natural language processing \(NLP\)<a name="integrated-med-api"></a>

HealthLake has integrated medical natural language processing for the `DocumentReference` resource type\. HealthLake automatically runs the integrated medical NLP on all `DocumentReference` resources as they are written to the system in an `Import` operation, during a `Create` operation, or during an `Update` operation\. The original resource stays unchanged, and the extracted medical information is automatically appended as custom fields\. These fields are indexed and queryable after extraction\.

## FHIR search functionality<a name="search-api"></a>

You can search health records that are stored in the Data Store either through a specific resource type with supported search parameters or for resource IDs in the server without specifying the resource type\. When a FHIR record is created, it is first saved into a FHIR Data Store, where it can be read, updated, queried, or deleted\. After the data is ingested, it is indexed using Amazon ES, which makes the data searchable\. HealthLake operates with eventual consistency with the Data Store, meaning that there might be a brief latency before the data is searchable within the Data Store\. 

## Import data<a name="health-lake-import"></a>

Amazon HealthLake enables you to bulk import your files from an Amazon S3 bucket\. Use either the console or [start\-fhir\-import\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_StartFHIRImportJob.html) to begin an import job\. Afterwards, you can use [describe\-fhir\-import\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DescribeFHIRImportJob.html) to monitor the status of the job and discover its properties\. After the import job is complete, the data can then be added to a Data Store, transformed, or analyzed and used in downstream applications\. 

## Export data<a name="health-lake-export"></a>

Amazon HealthLake enables you to bulk export your files to an Amazon S3 bucket\. Use either the console or [start\-fhir\-export\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_StartFHIRExportJob.html) to begin an export job\. Afterwards, you can use [describe\-fhir\-export\-job](https://docs.aws.amazon.com/healthlake/latest/APIReference/API_DescribeFHIRExportJob.html) to monitor the status of the job and discover its properties\. After the export job is complete, the data can then be visualized using AWS Quicksight or accessed by other AWS services\. 