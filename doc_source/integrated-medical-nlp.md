# Integrated medical natural language processing \(NLP\)<a name="integrated-medical-nlp"></a>

Amazon HealthLake automatically integrates with natural language processing \(NLP\) for the `DocumentReference` resource type\. The integrated medical NLP output is provided as an extension to the existing `DocumentReference` resource\. The integration involves reading the text data within the resource, and then calling the following integrated medical NLP operations: `DetectEntities-V2`, `InferICD10-CM`, and `InferRxNorm`\. The response of each of the integrated medical NLP APIs is appended to the `DocumentReference` resource as an extension that is searchable\. This enables users to identify patients through elements of their records that were previously buried within unstructured text\. When you create a resource in HealthLake, the resource is updated with the response from the integrated medical NLP operations\. These extensions follow the FHIR format for extensions with an identifying URL, and the respective value for the URL\. 

## Important notice<a name="important-notice"></a>

The Amazon HealthLake data transformations feature \(integrated medical NLP\) is not a substitute for professional medical advice, diagnosis, or treatment\. HealthLake integrated medical NLP provides confidence scores that indicate the level of confidence in the accuracy of the detected entities\. Identify the right confidence threshold for your use case, and use high confidence thresholds in situations that require high accuracy\. In certain use cases, results should be reviewed and verified by appropriately trained human reviewers\.

## Restrictions for integrated medical NLP<a name="restrictions-integrated-med"></a>

 Integration with medical NLP is nearly seamless\. However, there are two constraints:
+ Integrated medical NLP operations have an input quota of 10 K characters\. If the `DocumentReference` object is larger than the quota for the operation, HealthLake does not initiate the operation\.
+ If a Data Store is deleted before the operation is initiated, an update fails\.

## Search parameters<a name="search-parameters-med"></a>

The following table lists the searchable attributes for integrated medical NLP\. 


**Search parameters**  

| Search parameters | Finds matches for | 
| --- | --- | 
| detectEntities\-entity\-category | Entity Category within the DetectEntities subextension within the AWS CM Extension | 
| detectEntities\-entity\-text | Entity Text within the DetectEntities subextension within the AWS CM Extension | 
| detectEntities\-entity\-type | Entity Type within the DetectEntities subextension within the AWS CM Extension | 
| detectEntities\-entity\-score | Entity Score within the DetectEntities subextension within the AWS CM Extension | 
| infer\-icd10cm\-entity\-text | Entity Text within the InferICD10CM subextension within the AWS CM Extension | 
| infer\-icd10cm\-entity\-score | Entity Score within the InferICD10CM subextension within the AWS CM Extension | 
| infer\-icd10cm\-entity\-concept\-code | Entity Concept Code within the InferICD10CM subextension within the AWS CM Extension | 
| infer\-icd10cm\-entity\-concept\-description | Entity Concept Description within the InferICD10CM subextension within the AWS CM Extension | 
| infer\-icd10cm\-entity\-concept\-score | Entity Concept Score within the InferICD10CM subextension within the AWS CM Extension | 
| infer\-rxnorm\-entity\-score | Entity Score within the InferRxNorm subextension within the AWS CM Extension | 
| infer\-rxnorm\-entity\-text | Entity Text within the InferRxNorm subextension within the AWS CM Extension | 
| infer\-rxnorm\-entity\-concept\-code | Entity Concept Code within the InferRxNorm subextension within the AWS CM Extension | 
| infer\-rxnorm\-entity\-concept\-description | Entity Concept Description within the InferRxNorm subextension within the AWS CM Extension | 
| infer\-rxnorm\-entity\-concept\-score |  Entity Concept Score within the InferRxNorm subextension within the AWS CM Extension  | 

To match the criteria where `EntityText` and `EntityCategory` are part of the same entity, HealthLake provides special search\. The following table describes the special search parameters that are supported within HealthLake\.


**Search parameters**  

| Search parameters | Matches returned | 
| --- | --- | 
| detectEntities\-entity\-text\-category | If there is at least one entity in the DetectEntities subextention that matches both the entityText and entityCategory\. | 
| detectEntities\-entity\-type\-score | If there is at least one entity in the DetectEntities subextention that matches both the entityType and entityScore\. | 
| detectEntities\-entity\-text\-score | If there is at least one entity in the DetectEntities subextention that matches both the entityText and entityScore\. | 
| detectEntities\-entity\-text\-type | If there is at least one entity in the DetectEntities subextention that matches both the entityText and entityType\. | 
| detectEntities\-entity\-category\-score | If there is at least one entity that matches both the entityCategory and entityScore\. | 
| infer\-icd10cm\-entity\-text\-concept\-code | If there is at least one entity in the InferICD10CM subextension that matches the entityText and there is at least one conceptCode for that entity that matches the code\. | 
| infer\-icd10cm\-entity\-text\-concept\-score | If there is at least one entity in the InferICD10CM subextension that matches the entityText and there is at least one conceptScore for that entity that matches the score\. | 
| infer\-icd10cm\-entity\-concept\-description\-concept\-score | If there is at least one concept within the entity in the InferICD10CM subextension that matches the concept description and the conceptScore\. | 
| infer\-rxnorm\-entity\-text\-concept\-code | If there is at least one entity in the InferRxNorm subextension that matches the entityText and there is at least one conceptCode for that entity that matches the code\. | 
| infer\-rxnorm\-entity\-text\-concept\-score | If there is at least one entity in the InferRxNorm subextension that matches the entityText and there is at least one conceptScore for that entity that matches the score\. | 
| infer\-rxnorm\-entity\-concept\-description\-concept\-score |  If there is at least one concept within the entity in the InferRxNorm subextension that matches the concept description and the conceptScore\.  | 

## Integrated medical NLP enrichment<a name="med-example"></a>

The following example shows how integrated medical NLP detects entities and adds information to the FHIR resource for enrichment\. The initial record would read as follows\.

```
POST /datastore/(Datastore ID)/r4/DocumentReference/ HTTP/1.1
Host: healthlake.us-east-1.amazonaws.com
Content-Type: application/json
Authorization: AWS4-HMAC-SHA256 Credential=(Redacted)

{
  "resourceType": "DocumentReference",
  "text": {
          "status": "generated",
          "div": "(div xmlns=\"http://www.w3.org/1999/xhtml\">\n\n\t\t\t\t\t\t< href=\"http://localhost:9556/svc/fhir/Binary/1e404af3-077f-4bee-b7a6-a9be97e1ce32\">Document: urn:oid:129.6.58.92.88336</a>undefined, created 24/12/2005\n\t\t\t\t\t</div"
        },
   "status": "current",
   "content": [
    {
      "attachment": {
        "contentType": "text/plain",
        "data": "CjIwMTktMTItMzEKCiMgQ2hpZWYgQ29tcGxhaW50Ck5vIGNvbXBsYWludHMuCgojIEhpc3Rvcnkgb2YgUHJlc2VudCBJbGxuZXNzCkN1cnRpczk0IGlzIGEgMSB5ZWFyLW9sZCBub24taGlzcGFuaWMgd2hpdGUgbWFsZS4gUGF0aWVudCBoYXMgYSBoaXN0b3J5IG9mIHN0cmVwdG9jb2NjYWwgc29yZSB0aHJvYXQgKGRpc29yZGVyKSwgb3RpdGlzIG1lZGlhLgoKIyBTb2NpYWwgSGlzdG9yeQogUGF0aWVudCBoYXMgbmV2ZXIgc21va2VkLgoKUGF0aWVudCBjb21lcyBmcm9tIGEgaGlnaCBzb2Npb2Vjb25vbWljIGJhY2tncm91bmQuIFBhdGllbnQgY3VycmVudGx5IGhhcyBBbnRoZW0uCgojIEFsbGVyZ2llcwpObyBLbm93biBBbGxlcmdpZXMuCgojIE1lZGljYXRpb25zCnBlbmljaWxsaW4gdiBwb3Rhc3NpdW0gMjUwIG1nIG9yYWwgdGFibGV0OyBhbW94aWNpbGxpbiAyNTAgbWcgb3JhbCBjYXBzdWxlOyBhY2V0YW1pbm9waGVuIDE2MCBtZyBjaGV3YWJsZSB0YWJsZXQKCiMgQXNzZXNzbWVudCBhbmQgUGxhbgoKCiMjIFBsYW4KUGF0aWVudCB3YXMgZ2l2ZW4gdGhlIGZvbGxvd2luZyBpbW11bml6YXRpb25zOiBkdGFwLiAKVGhlIGZvbGxvd2luZyBwcm9jZWR1cmVzIHdlcmUgY29uZHVjdGVkOgotIG1lZGljYXRpb24gcmVjb25jaWxpYXRpb24gKHByb2NlZHVyZSkK"
      }
    }
    ],
        "category": [
          {
            "coding": [
              {
                "system": "http://hl7.org/fhir/us/core/CodeSystem/us-core-documentreference-category",
                "code": "clinical-note",
                "display": "Clinical Note"
              }
            ]
          }
        ],
  "subject": {
    "reference": "Patient/2de04858-ba65-44c1-8af1-f2fe69a977d9"
  }
}




{
    "resourceType": "DocumentReference",
    "text": {
        "status": "generated",
        "div": "<div xmlns=\"http://www.w3.org/1999/xhtml\">\n\n\t\t\t\t\t\t<a href=\"http://localhost:9556/svc/fhir/Binary/1e404af3-077f-4bee-b7a6-a9be97e1ce32\">Document: urn:oid:129.6.58.92.88336</a>undefined, created 24/12/2005\n\t\t\t\t\t</div>"
    },
    "status": "current",
    "content": [
        {
            "attachment": {
                "contentType": "text/plain",
                "data": "CjIwMTktMTItMzEKCiMgQ2hpZWYgQ29tcGxhaW50Ck5vIGNvbXBsYWludHMuCgojIEhpc3Rvcnkgb2YgUHJlc2VudCBJbGxuZXNzCkN1cnRpczk0IGlzIGEgMSB5ZWFyLW9sZCBub24taGlzcGFuaWMgd2hpdGUgbWFsZS4gUGF0aWVudCBoYXMgYSBoaXN0b3J5IG9mIHN0cmVwdG9jb2NjYWwgc29yZSB0aHJvYXQgKGRpc29yZGVyKSwgb3RpdGlzIG1lZGlhLgoKIyBTb2NpYWwgSGlzdG9yeQogUGF0aWVudCBoYXMgbmV2ZXIgc21va2VkLgoKUGF0aWVudCBjb21lcyBmcm9tIGEgaGlnaCBzb2Npb2Vjb25vbWljIGJhY2tncm91bmQuIFBhdGllbnQgY3VycmVudGx5IGhhcyBBbnRoZW0uCgojIEFsbGVyZ2llcwpObyBLbm93biBBbGxlcmdpZXMuCgojIE1lZGljYXRpb25zCnBlbmljaWxsaW4gdiBwb3Rhc3NpdW0gMjUwIG1nIG9yYWwgdGFibGV0OyBhbW94aWNpbGxpbiAyNTAgbWcgb3JhbCBjYXBzdWxlOyBhY2V0YW1pbm9waGVuIDE2MCBtZyBjaGV3YWJsZSB0YWJsZXQKCiMgQXNzZXNzbWVudCBhbmQgUGxhbgoKCiMjIFBsYW4KUGF0aWVudCB3YXMgZ2l2ZW4gdGhlIGZvbGxvd2luZyBpbW11bml6YXRpb25zOiBkdGFwLiAKVGhlIGZvbGxvd2luZyBwcm9jZWR1cmVzIHdlcmUgY29uZHVjdGVkOgotIG1lZGljYXRpb24gcmVjb25jaWxpYXRpb24gKHByb2NlZHVyZSkK"
            }
        }
    ],
    "category": [
        {
            "coding": [
                {
                    "system": "http://hl7.org/fhir/us/core/CodeSystem/us-core-documentreference-category",
                    "code": "clinical-note",
                    "display": "Clinical Note"
                }
            ]
        }
    ],
    "subject": {
        "reference": "Patient/2de04858-ba65-44c1-8af1-f2fe69a977d9"
    },
    "meta": {
        "lastUpdated": "2020-11-23T06:56:11.580Z"
    },
    "id": "3a43969a-c690-4480-85e3-7e2c65c8cefb"
}
```

After enrichment, the resource will have the following information when read\. This is a truncated record for clarity\. Included in the response is whether the operation was successful or unsupported\.

```
{
    "resourceType": "DocumentReference",
    "status": "current",
    "content": [
        {
            "attachment": {
                "contentType": "text/plain",
                "data": "CjIwMTktMTItMzEKCiMgQ2hpZWYgQ29tcGxhaW50Ck5vIGNvbXBsYWludHMuCgojIEhpc3Rvcnkgb2YgUHJlc2VudCBJbGxuZXNzCkN1cnRpczk0IGlzIGEgMSB5ZWFyLW9sZCBub24taGlzcGFuaWMgd2hpdGUgbWFsZS4gUGF0aWVudCBoYXMgYSBoaXN0b3J5IG9mIHN0cmVwdG9jb2NjYWwgc29yZSB0aHJvYXQgKGRpc29yZGVyKSwgb3RpdGlzIG1lZGlhLgoKIyBTb2NpYWwgSGlzdG9yeQogUGF0aWVudCBoYXMgbmV2ZXIgc21va2VkLgoKUGF0aWVudCBjb21lcyBmcm9tIGEgaGlnaCBzb2Npb2Vjb25vbWljIGJhY2tncm91bmQuIFBhdGllbnQgY3VycmVudGx5IGhhcyBBbnRoZW0uCgojIEFsbGVyZ2llcwpObyBLbm93biBBbGxlcmdpZXMuCgojIE1lZGljYXRpb25zCnBlbmljaWxsaW4gdiBwb3Rhc3NpdW0gMjUwIG1nIG9yYWwgdGFibGV0OyBhbW94aWNpbGxpbiAyNTAgbWcgb3JhbCBjYXBzdWxlOyBhY2V0YW1pbm9waGVuIDE2MCBtZyBjaGV3YWJsZSB0YWJsZXQKCiMgQXNzZXNzbWVudCBhbmQgUGxhbgoKCiMjIFBsYW4KUGF0aWVudCB3YXMgZ2l2ZW4gdGhlIGZvbGxvd2luZyBpbW11bml6YXRpb25zOiBkdGFwLiAKVGhlIGZvbGxvd2luZyBwcm9jZWR1cmVzIHdlcmUgY29uZHVjdGVkOgotIG1lZGljYXRpb24gcmVjb25jaWxpYXRpb24gKHByb2NlZHVyZSkK"
            }
        }
    ],
    "category": [
        {
            "coding": [
                {
                    "system": "http://hl7.org/fhir/us/core/CodeSystem/us-core-documentreference-category",
                    "code": "clinical-note",
                    "display": "Clinical Note"
                }
            ]
        }
    ],
    "subject": {
        "reference": "Patient/2de04858-ba65-44c1-8af1-f2fe69a977d9"
    },
    "id": "f40365c6-d714-4ce7-b190-43d0d2047a10",
    "meta": {
        "lastUpdated": "2021-05-07T17:47:35.331Z"
    },
    "extension": [
        {
            "extension": [
                {
                    "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/",
                    "extension": [
                        {
                            "url": "http://healthlake.amazonaws.com/aws-cm/infer-icd10/raw-response",
                            "valueString": "{Entities: [{Id: 1,Text: streptococcal sore throat,Category: MEDICAL_CONDITION,Type: DX_NAME,Score: 0.9721338,BeginOffset: 151,EndOffset: 176,Attributes: [],Traits: [],ICD10CMConcepts: [{Description: Streptococcal pharyngitis,Code: J02.0,Score: 0.67831886}, {Description: Streptococcal sepsis, unspecified,Code: A40.9,Score: 0.6346688}, {Description: Acute pharyngitis, unspecified,Code: J02.9,Score: 0.6200017}, {Description: Acute streptococcal tonsillitis, unspecified,Code: J03.00,Score: 0.6014083}, {Description: Acute pharyngitis,Code: J02,Score: 0.55188143}]}, {Id: 3,Text: disorder,Category: MEDICAL_CONDITION,Type: DX_NAME,Score: 0.8767418,BeginOffset: 178,EndOffset: 186,Attributes: [],Traits: [{Name: DIAGNOSIS,Score: 0.9286054}],ICD10CMConcepts: [{Description: Unspecified disorder of ear, unspecified ear,Code: H93.90,Score: 0.7463527}, {Description: Disorder of brain, unspecified,Code: G93.9,Score: 0.72858506}, {Description: Endocrine disorder, unspecified,Code: E34.9,Score: 0.7257518}, {Description: Disorder of thyroid, unspecified,Code: E07.9,Score: 0.72223496}, {Description: Personal history of other diseases of the nervous system and sense organs,Code: Z86.69,Score: 0.68951124}]}, {Id: 4,Text: otitis media,Category: MEDICAL_CONDITION,Type: DX_NAME,Score: 0.9772095,BeginOffset: 189,EndOffset: 201,Attributes: [],Traits: [{Name: DIAGNOSIS,Score: 0.94999653}],ICD10CMConcepts: [{Description: Otitis media, unspecified, unspecified ear,Code: H66.90,Score: 0.7708893}, {Description: Otitis media, unspecified, bilateral,Code: H66.93,Score: 0.7557719}, {Description: Otitis media, unspecified,Code: H66.9,Score: 0.7519664}, {Description: Otitis media, unspecified, left ear,Code: H66.92,Score: 0.73516965}, {Description: Otitis media, unspecified, right ear,Code: H66.91,Score: 0.69751483}]}],ModelVersion: 0.1.0}"
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
                                    "valueInteger": 1
                                },
...
                {
                    "url": "http://healthlake.amazonaws.com/aws-cm/status/",
                    "valueString": "SUCCESS"
                },
                {
                    "url": "http://healthlake.amazonaws.com/aws-cm/message/",
                    "valueString": "The Amazon HealthLake integrated medical NLP operation was successful."
                }
            ],
            "url": "http://healthlake.amazonaws.com/aws-cm/"
        }
    ]
}
```