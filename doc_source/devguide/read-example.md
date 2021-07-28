# Example: Reading a resource with GET<a name="read-example"></a>

The following example shows how to read a patient FHIR resource using `GET` and using the logical ID \(`LID`\) to define the resource\.

```
GET /datastore/(Datastore ID)/r4/Patient/2de04858-ba65-44c1-8af1-f2fe69a977d9 HTTP/1.1
Host: healthlake.us-east-1.amazonaws.com
Content-Type: application/json
Authorization: AWS4-HMAC-SHA256 Credential=(Redacted)
```

You receive the following JSON in response\.

```
{
    "resourceType": "Patient",
    "active": true,
    "name": [
        {
            "use": "official",
            "family": "Doe",
            "given": [
                "Jane"
            ]
        },
        {
            "use": "usual",
            "given": [
                "Jane"
            ]
        }
    ],
    "gender": "female",
    "birthDate": "1966-09-01",
    "meta": {
        "lastUpdated": "2020-11-23T06:24:13.202Z"
    },
    "id": "2de04858-ba65-44c1-8af1-f2fe69a977d9"
}
```