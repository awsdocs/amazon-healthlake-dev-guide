# Example: Updating a resource using PUT<a name="update-example"></a>

The following example shows how to use `PUT` to update a patient FHIR resource to correct inaccurate patient information\.

```
PUT /datastore/(Datastore ID)/r4/Patient/2de04858-ba65-44c1-8af1-f2fe69a977d9 HTTP/1.1
Host: healthlake.us-east-1.amazonaws.com
Content-Type: application/json
Authorization: AWS4-HMAC-SHA256 Credential=(Redacted)

{
  "id": "2de04858-ba65-44c1-8af1-f2fe69a977d9",
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
  "birthDate": "1985-12-31"
}
```

You receive the following JSON in response to confirm the change\.

```
{
    "id": "2de04858-ba65-44c1-8af1-f2fe69a977d9",
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
    "birthDate": "1985-12-31",
    "meta": {
        "lastUpdated": "2020-11-23T06:43:45.133Z"
    }
    "id": "2de04858-ba65-44c1-8af1-f2fe69a977d9"
}
```