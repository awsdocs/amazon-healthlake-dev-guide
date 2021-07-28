# Search with POST<a name="search-with-post"></a>

 You can also use Search with POST to query your Data Store through either parameters in the URI or in a request body\. You can not have parameters in both the URI & and the request body\. To protect PHI or PII, customers are strongly advised to put parameters in a body request, not the URI, for queries\.

## Search with POST example with parameters in URI<a name="uri-example"></a>

The following example demonstrates how to perform the same search using an HTTP client with a POST search with parameters in URI for the following input in HTTP\.

```
POST /datastore/(Datastore ID)/r4/DocumentReference/_search?_lastUpdated=le2021-12-19&infer-icd10cm-entity-text-concept-score;=streptococcal|0.6&infer-rxnorm-entity-text-concept-score=Amoxicillin|0.8 HTTP/1.1
Host: healthlake.us-east-1.amazonaws.com
Content-Type: application/json
Authorization: AWS4-HMAC-SHA256 Credential= (Redacted)
```

## Search with POST example with parameters in body<a name="body-example"></a>

The following example demonstrates how to perform the same search using an HTTP client with a POST search with parameters in body for the following input in HTTP\. To use Search With Post with parameters in the request body, you must use content\-type “application/ x\-www\-form\-urlencoded”\. 

```
POST /datastore/(Datastore ID)/r4/DocumentReference/_search HTTP/1.1
Host: healthlake.us-east-1.amazonaws.com
Content-Type: application/ x-www-form-urlencoded
Authorization: AWS4-HMAC-SHA256 Credential= (Redacted)
lastUpdated=le2021-12-19&infer-icd10cm-entity-text-concept-score;=streptococcal|0.6&infer-rxnorm-entity-text-concept-score=Amoxicillin|0.8
```