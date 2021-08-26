# Preloaded datatypes<a name="preloaded-data"></a>

HealthLake supports only SYNTHEA as a preloaded data type\. [Synthea](https://synthetichealth.github.io/synthea/) is a synthetic patient generator that models the medical history of model\-generated patients\. It’s an open\-source Git repository that allows HealthLake to generate FHIR R4\-compliant resource bundles so that users can test models without using actual patient data\. 

The following resource types are available as preloaded Data Stores\.


**Supported Synthea resource types**  

|  |  | 
| --- |--- |
| AllergyIntolerance | Location | 
| CarePlan | MedicationAdministration | 
|  CareTeam  | MedicationRequest | 
|  Claim  |  Observation  | 
|  Condition  | Organization | 
|  Device  | Patient | 
| DiagnosticReport | Practitioner | 
| Encounter | PractitionerRole | 
|  ExplanationofBenefit  | Procedure | 
|  ImagingStudy  |  Provenance  | 
|  Immunization  |   | 