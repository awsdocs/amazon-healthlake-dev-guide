# Using FHIR search in Amazon HealthLake<a name="using-search-healthlake"></a>

 You can search for a specific resource type with supported search parameters\. You can also search for resource IDs in the server without specifying the resource type\. For more information about FHIR\-supported searches, see the [FHIR Search Documentation](https://www.hl7.org/fhir/search.html)\. HealthLake supports both Search with POST and Search with GET\. Search with POST with the parameters in the request body is strongly recommended for all queries involving PHI and PII\. 

When results are paginated, all follow\-up page requests will be Search with GET by default when the pagination token is used\. 

The following parameters are supported in HealthLake\. 
+ **Number** – Searches for a numerical value\.
+ **Date/DateTime** – Searches for a date or time reference\. 
+ **String** – Searches for a sequence of characters\. 
+ **Token** – Searches for a close\-to\-exact match against a string of characters, often against a pair of values\. 
+ **Composite** – Searches for multiple parameters for a single resource type, using the `AND` operation\.
+ **Quantity** – Searches for a number, system, and code as values\. A number is required, but system and code are optional\.
+ **Reference** – Searches for references to other FHIR resources\. An example is a search for a reference to a patient within an observation resource\. 
+ **URI** – Searches for a string of characters that unambiguously identifies a particular resource\.
+ **Special** – Searches based on integrated medical NLP extensions\. 

To see which search parameters are supported for each resource type, use `GETCapabilities` in your FHIR HTTP client\.

## Managing invalid search parameters<a name="invalid-parameters"></a>

HealthLake manages invalid search parameters based on FHIR guidance\. To specify how the server should handle unknown or unsupported search parameters, define the handling parameter in the HTTP header as follows\. 
+ **handling = strict** – The server should return an error for unknown or unsupported search parameters\.
+ **handling = lenient** – The server should ignore unknown or unsupported search parameters\.