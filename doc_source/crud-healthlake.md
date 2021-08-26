# Managing FHIR resources in Amazon HealthLake<a name="crud-healthlake"></a>

Amazon HealthLake enables users to manage their FHIR resources in a Data Store through an HTTP client or the console\.

## Managing FHIR resources<a name="fhir-rest-api"></a>

Use the Amazon HealthLake FHIR REST APIs to can create, read, update, and delete resources in an active Data Store\. To see all of the active Data Store’s FHIR\-related capabilities, see the capability statement for the active Data Store through either `GETCapabilities` in an HTTP client or the console\. FHIR resources are validated against the FHIR R4 Structure Definition\. If a resource is invalid, an OperationOutcome message will result with details explaining the exception\. 

The following table lists the actions that are supported by HealthLake\. 


**Supported Operations**  

|  Operation  |  Description  | Instance\-level, Type\-level or Whole\-system interaction | 
| --- | --- | --- | 
|  Read  | Read the current state of the resource | Instance\-level | 
| Update | Update a resource by its ID \(or create it if it's new\) | Instance\-level | 
|  Delete  | Delete a resource | Instance\-level | 
|  Create  |  Create a new resource with a server\-assigned ID  | Type\-level  | 
|  Search   | Search the resource type based on filter criteria | Type\-level | 
|  Capabilities  | Get a capability statement for the system | Whole\-system level | 

 The following table lists the resource types supported by HealthLake\. You can use these resources as search criteria or as part of analysis workflows\. 


**Supported FHIR Resource Types**  

|  |  |  | 
| --- |--- |--- |
|  Account  | DocumentReference | Organization | 
| ActivityDefinition | Encounter | Parameters | 
| AllergyIntolerance | Endpoint | Patient | 
| Appointment | EpisodeofCare | PaymentNotice | 
| AppointmentResponse | ExplanationOfBenefit | PaymentReconciliation | 
| AuditEvent |  FamilyMemberHistory  | Person | 
|  Binary  | Goal | Practitioner | 
| Bundle | GuidanceResponse | PractitionerRole | 
|  CapabilityStatement  | HealthcareService | Procedure | 
| CarePlan | ImagingStudy | Provenance | 
| CareTeam | Immunization | Questionnaire | 
| Claim | Library | QuestionnaireResponse | 
| ClaimResponse |  Location  | RelatedPerson | 
|  CodeSystem  |  Measure  |  RequestGroup  | 
|  Communication  |  MeasureReport  |  Schedule  | 
| CommunicationRequest | Medication |  ServiceRequest  | 
| ConceptMap | MedicationAdministration |  Slot  | 
| Condition |  MedicationDispense  |  Specimen  | 
|  Coverage  |  MedicationRequest  |  StructureDefinition  | 
| CoverageEligibilityRequest |  MedicationStatement  |  StructureMap  | 
| CoverageEligibilityResponse |  MessageHeader  |  Substance  | 
| Device | NutritionOrder | ValueSet | 
|  DiagnosticReport  |  Observation  |  VisionPrescription  | 
| DocumentManifest |  OperationOutcome  |     | 

Note: An AuditEvent resource can be created or read, but can not be updated or deleted\. 