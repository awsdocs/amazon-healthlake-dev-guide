# Example: Deleting a resource<a name="delete-example"></a>

The following example shows how to delete a patient FHIR resource\.

```
DELETE /datastore/(Datastore ID)/r4/Patient/2de04858-ba65-44c1-8af1-f2fe69a977d9 HTTP/1.1
Host: healthlake.us-east-1.amazonaws.com
Content-Type: application/json
Authorization: AWS4-HMAC-SHA256 Credential=(Redacted)
```

You receive the following response, confirming that the resource is no longer in the Data Store\.

`204 No Content Response Code`