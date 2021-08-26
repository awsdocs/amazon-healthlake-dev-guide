# How do I create authorization for the FHIR RESTful APIs?<a name="authorization-troubleshooting"></a>

Users should use a Signature version 4 signing process to add authentication to HealthLake API requests sent through an HTTP client\. To learn more, see [Signature Version 4 signing process](https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html)\.

To create sigv4 authorization using the AWS SDK for Python, create a script similar to the following example\. 

```
import boto3
import requests
import json
from requests_auth_aws_sigv4 import AWSSigV4
 
# Set the input arguments
data_store_endpoint = 'https://healthlake.us-east-1.amazonaws.com/datastore/<datastore id>/r4//'
resource_path = "Patient"
requestBody = {"resourceType": "Patient", "active": True, "name": [{"use": "official","family": "Dow","given": ["Jen"]},{"use": "usual","given": ["Jen"]}],"gender": "female","birthDate": "1966-09-01"}
region = 'us-east-1'
 
#Frame the resource endpoint
resource_endpoint = data_store_endpoint+resource_path
session = boto3.session.Session(region_name=region)
client = session.client("healthlake")
 
# Frame authorization
auth = AWSSigV4("healthlake", session=session)
 
# Calling data store FHIR endpoint using SigV4 auth

r = requests.post(resource_endpoint, json=requestBody, auth=auth, )
print(r.json())
```

Additional information about using sigv4 authorization using AWS SDK for Python can be found in the [Boto3 credentials topic](https://boto3.amazonaws.com/v1/documentation/api/latest/guide/credentials.html)\.