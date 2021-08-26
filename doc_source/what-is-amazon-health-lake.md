# What is Amazon HealthLake?<a name="what-is-amazon-health-lake"></a>

Amazon HealthLake is a HIPAA\-eligible service that healthcare providers, health insurance companies, and pharmaceutical companies can use to store, transform, query, and analyze large\-scale health data\. 

Health data is frequently incomplete and inconsistent\. It's also often unstructured, with information contained in clinical notes, lab reports, insurance claims, medical images, recorded conversations, and time\-series data \(for example, heart ECG or brain EEG traces\)\. 

Healthcare providers can use HealthLake to store, transform, query, and analyze data in the AWS Cloud\. Using the HealthLake integrated medical natural language processing \(NLP\) capabilities, you can analyze unstructured clinical text from diverse sources\. HealthLake transforms unstructured data using natural language processing models, and provides powerful query and search capabilities\. You can use HealthLake to organize, index, and structure patient information in a secure, compliant, and auditable manner\. 

## Benefits of Amazon HealthLake<a name="how-benefits-healthlake"></a>

With Amazon HealthLake, you can:
+ **Quickly and easily ingest health data** – You can bulk import on\-premises Fast Healthcare Interoperability Resources \(FHIR \) files, including clinical notes, lab reports, insurance claims, and more, to an Amazon Simple Storage Service \(Amazon S3\) bucket\. You can then use the data in downstream applications or workflows\.
+ **Store your data in the AWS Cloud in a secure, HIPAA\-eligibile manner that can be audited**– You can store data in FHIR format, so it can be easily queried\. HealthLake creates a complete, chronological view of each patient’s medical history, and structures it in the R4 FHIR standard format\. 
+ **Transform unstructured data using specialized ML models** – Integrated medical natural language processing \(NLP\) transforms all of the raw medical text data using specialized ML models that have been trained to understand and extract meaningful information from unstructured healthcare data\. With integrated medical NLP, you can automatically extract entities \(for example, medical procedures and medications\), entity relationships \(for example, a medication and its dosage\), and entity traits \(for example, positive or negative test result or time of procedure\) data from your medical text\. 
+ **Use powerful query and search capabilities ** – HealthLake supports FHIR CRUD \(Create/Read/Update/Delete\) and FHIR Search operations\. 

## Amazon HealthLake use cases<a name="use-cases-healthlake"></a>

You can use Amazon HealthLake for the following healthcare applications:
+ ** Population health management** – HealthLake helps healthcare organizations analyze population health trends, outcomes, and costs\. This helps organization to identify the most appropriate intervention for a patient population, and choose better care management options\.
+ **Improving quality of care** – HealthLake aids hospitals, health insurance companies, and life sciences organizations close gaps in care, improve quality of care, and reduce cost by compiling a complete view of a patient’s medical history\.
+ **Optimize hospital efficiency** – HealthLake offers hospitals key analytics and machine learning tools to improve efficiency and reduce hospital waste\. 

## Accessing Amazon HealthLake<a name="acessing-amazon-healthlake"></a>

You can access Amazon HealthLake through the AWS Management Console, AWS Command Line Interface \(AWS CLI\), or the AWS SDKs\. 

1. AWS Management Console – Provides a web interface that you can use to access HealthLake\.

1. AWS Command Line Interface \(AWS CLI\) – Provides commands for a broad set of AWS services, including HealthLake, and is supported on Windows, macOS, and Linux\. For more information about installing the AWS CLI, see [ AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html) 

1. AWS SDKs – AWS provides SDKs \(software development kits\) that consist of libraries and sample code for various programming languages and platforms \(Java, Python, Ruby, \.NET, iOS, Android, and so on\)\. The SDKs provide a convenient way to create programmatic access to HealthLake and AWS\. For more information, see the [AWS SDK for Python](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/index.html)

## HIPAA eligibility and data security<a name="hipaa"></a>

This is a HIPAA Eligible Service\. For more information about AWS, U\.S\. Health Insurance Portability and Accountability Act of 1996 \(HIPAA\), and using AWS services to process, store, and transmit protected health information \(PHI\), see [HIPAA Overview](https://aws.amazon.com/compliance/hipaa-compliance/)\.

Connections to HealthLake containing PHI or personally identifiable information \(PII\) must be encrypted\. By default, all connections to HealthLake use HTTPS over TLS\. HealthLake stores encrypted customer content and operates by the AWS Shared Responsibility principle\. 

## Pricing<a name="pricing-for-healthlake"></a>

For information about HealthLake pricing, see the [Amazon HealthLake pricing page](http://aws.amazon.com/healthlake/pricing/)\. 