# Supported search parameters and search modifiers in HealthLake<a name="supported-search-healthlake"></a>

Common search parameters are supported for all FHIR resources, regardless of type\. The following tables provide details about supported search parameter types, modifiers, comparators, common search parameters, and search operations\.


**Supported search parameters**  

| Search parameter  |  Description  | 
| --- | --- | 
|  \_id  |  Resource id \(not a full URL\)  | 
| \_lastUpdated | Date last updated\. Server has discretion on the boundary precision\. | 
| \_tag |  Search by a resource tag\.  | 
|  \_profile  |  Search for all resources tagged with a profile\.  | 

Search modifiers allow for different types of matching logic on string\-based fields\. For example, you can specify that a larger string should contain a smaller string, or you can specify that the string should be an exact match of the string that is passed in\.


**Supported search modifiers**  

|  Search modifier  | Type | 
| --- | --- | 
| :missing | All parameters except Composite | 
| :exact | String | 
| :contains | String | 
| :not | Token | 
| :text | Token | 
| :identifier | Reference | 

Search comparators allow you to control the nature of the matching for number, date, and quantity fields\. The following table lists search comparators and their definitions\.


**Supported search comparators**  

|  Search comparator   |  Description  | 
| --- | --- | 
|  eq  | The value for the parameter in the resource is equal to the provided value\. | 
| ne | The value for the parameter in the resource is not equal to the provided value\. | 
| gt | The value for the parameter in the resource is greater than the provided value\. | 
|  lt  | The value for the parameter in the resource is less than the provided value\. | 
| ge | The value for the parameter in the resource is greater or equal to the provided value\. | 
| le | The value for the parameter in the resource is less or equal to the provided value\. | 
| sa | The value for the parameter in the resource starts after the provided value\. | 
| eb | The value for the parameter in the resource ends before the provided value | 