# Search with GET<a name="search-with-get"></a>

HealthLake supports queries using Search with GET, however it is recommened that any queries involving PHI or PII are performed using Search with POST with the query parameters in the request body, not the URI\. Parameters in Search with GET are only accepted with search parameters in the URI\. The following example shows how to search `DocumentReferences` for streptococcal diagnosis and amoxicillin medication using an HTTP client with a `GET` search for the following input in HTTP\.

```
GET /datastore/(Datastore ID)/r4/DocumentReference?_lastUpdated=le2021-12-19&infer-icd10cm-entity-text-concept-score;=streptococcal|0.6&infer-rxnorm-entity-text-concept-score=Amoxicillin|0.8 HTTP/1.1
Host: healthlake.us-east-1.amazonaws.com
Content-Type: application/json
Authorization: AWS4-HMAC-SHA256 Credential= (Redacted)
```

 You will receive the following JSON response\.

```
 
{
    "resourceType": "Bundle",
    "type": "searchset",
    "entry": [
    {
       "resource": {
       "resourceType": "DocumentReference",
       "id": "985c3e94-4219-4c79-97a1-c94694525e24",
       "meta": {
          "lastUpdated": "2020-11-23T06:09:10.719Z"
        },
        "extension": [
          {
            "url": "http://healthlake.amazonaws.com/aws-cm/",
            "extension": [
              {
                "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/",
                "extension": [
                  {
                    "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/raw-response",
                    "valueString": "{Entities: [{Id: 0,Text: otitis media,Category: MEDICAL_CONDITION,Type: DX_NAME,Score: 0.9815994,BeginOffset: 151,EndOffset: 163,Attributes: [],Traits: [{Name: DIAGNOSIS,Score: 0.95042425}],ICD10CMConcepts: [{Description: Otitis media, unspecified, unspecified ear,Code: H66.90,Score: 0.7176407}, {Description: Otitis media, unspecified,Code: H66.9,Score: 0.6930445}, {Description: Otitis media, unspecified, left ear,Code: H66.92,Score: 0.688161}, {Description: Otitis media, unspecified, bilateral,Code: H66.93,Score: 0.6748094}, {Description: Otitis media, unspecified, right ear,Code: H66.91,Score: 0.6645618}]}, {Id: 1,Text: streptococcal sore throat,Category: MEDICAL_CONDITION,Type: DX_NAME,Score: 0.92208487,BeginOffset: 461,EndOffset: 486,Attributes: [],Traits: [],ICD10CMConcepts: [{Description: Streptococcal pharyngitis,Code: J02.0,Score: 0.55638546}, {Description: Acute streptococcal tonsillitis, unspecified,Code: J03.00,Score: 0.53159785}, {Description: Streptococcal sepsis, unspecified,Code: A40.9,Score: 0.51865804}, {Description: Acute pharyngitis, unspecified,Code: J02.9,Score: 0.45085955}, {Description: Streptococcal infection, unspecified site,Code: A49.1,Score: 0.41550553}]}, {Id: 3,Text: disorder,Category: MEDICAL_CONDITION,Type: DX_NAME,Score: 0.9191257,BeginOffset: 488,EndOffset: 496,Attributes: [],Traits: [{Name: DIAGNOSIS,Score: 0.93372077}],ICD10CMConcepts: [{Description: Parkinson's disease,Code: G20,Score: 0.6959145}, {Description: Illness, unspecified,Code: R69,Score: 0.68428487}, {Description: Disorder of bone, unspecified,Code: M89.9,Score: 0.6542605}, {Description: Unspecified mental disorder due to known physiological condition,Code: F09,Score: 0.6240179}, {Description: Mental disorder, not otherwise specified,Code: F99,Score: 0.61046}]}],ModelVersion: 0.1.0}"
                  },
                  {
                    "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/model-version",
                    "valueString": "0.1.0"
                  },
                  {
                    "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity",
                    "extension": [
                      {
                        "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-id",
                        "valueInteger": 0
                      },
                      {
                        "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-text",
                        "valueString": "otitis media"
                      },
                      {
                        "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-begin-offset",
                        "valueInteger": 151
                      },
                      {
                        "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-end-offset",
                        "valueInteger": 163
                      },
                      {
                        "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-score",
                        "valueDecimal": 0.9815994
                      },
                      {
                        "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-ConceptList",
                        "extension": [
                          {
                            "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept",
                            "extension": [
                              {
                                "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept-Code",
                                "valueString": "H66.90"
                              },
                              {
                                "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept-Description",
                                "valueString": "Otitis media, unspecified, unspecified ear"
                              },
                              {
                                "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept-Score",
                                "valueDecimal": 0.7176407
                              }
                            ]
                          },
                          {
                            "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept",
                            "extension": [
                              {
                                "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept-Code",
                                "valueString": "H66.9"
                              },
                              {
                                "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept-Description",
                                "valueString": "Otitis media, unspecified"
                              },
                              {
                                "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept-Score",
                                "valueDecimal": 0.6930445
                              }
                            ]
                          },
                          {
                            "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept",
                            "extension": [
                              {
                                "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/aws-cm-icd10-entity-Concept-Code",
                                "valueString": "H66.92"
                              }
                            ]
                          }
```