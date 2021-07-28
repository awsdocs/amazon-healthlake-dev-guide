# Encryption at rest for Amazon HealthLake<a name="encryption-at-rest"></a>

HealthLake provides encryption by default to protect sensitive customer data at rest by using a service owned AWS Key Management Service \(AWS KMS\) key\. Customer\-managed KMS keys are also supported and are required for both importing and exporting files from a Data Store\. To learn more about Customer\-managed KMS Key, see [Amazon Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)\. Customers can choose an AWS owned KMS key or a Customer\-managed KMS key when creating a Data Store\. The encryption configuration cannot be changed after a Data Store has been created\. If a Data Store is using an AWS owned KMS Key, it will be denoted as AWS\_OWNED\_KMS\_KEY and you will not see the specific key used for encryption at rest\.

## AWS owned KMS key<a name="AWS-owned-cmk"></a>

HealthLake uses these keys by default to automatically encrypt potentially sensitive information such as personally identifiable or Private Health Information\(PHI\) data at rest\. AWS owned KMS keys aren't stored in your account\. They're part of a collection of KMS keys that AWS owns and manages for use in multiple AWS accounts\. AWS services can use AWS owned KMS keys to protect your data\. You can't view, manage, use AWS owned KMS keys, or audit their use\. However, you don't need to do any work or change any programs to protect the keys that encrypt your data\.

You're not charged a monthly fee or a usage fee if you use AWS owned KMS keys, and they don't count against AWS KMS quotas for your account\. For more information, see [AWS owned keys](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#aws-owned-cmk)\.

## Customer managed KMS keys<a name="customer-owned-cmk"></a>

HealthLake supports the use of a symmetric customer managed KMS key that you create, own, and manage to add a second layer of encryption over the existing AWS owned encryption\. Because you have full control of this layer of encryption, you can perform such tasks as:
+ Establishing and maintaining key policies, IAM policies, and grants
+ Rotating key cryptographic material
+ Enabling and disabling key policies
+ Adding tags
+ Creating key aliases
+ Scheduling keys for deletion

 You can also use CloudTrail to track the requests that HealthLake sends to AWS KMS on your behalf\. Additional AWS KMS charges apply\.For more information, see [customer owned keys](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#customer-cmk)\.

## Create a customer managed key<a name="creating-co-cmk"></a>

You can create a symmetric customer managed key by using the AWS Management Console, or the AWS KMS APIs\.

Follow the steps for [Creating symmetric customer managed key](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html#create-symmetric-cmk) in the AWS Key Management Service Developer Guide\.

Key policies control access to your customer managed key\. Every customer managed key must have exactly one key policy, which contains statements that determine who can use the key and how they can use it\. When you create your customer managed key, you can specify a key policy\. For more information, see [Managing access to customer managed keys](https://docs.aws.amazon.com/kms/latest/developerguide/control-access-overview.html#managing-access) in the AWS Key Management Service Developer Guide\.

To use your customer managed key with your HealthLake resources, [kms:CreateGrant ](https://docs.aws.amazon.com/kms/latest/APIReference/API_CreateGrant.html) operations must be permitted in the key policy\. This adds a grant to a customer managed key which controls access to a specified KMS key, which gives a user access to the [kms:grant operations](https://docs.aws.amazon.com/kms/latest/developerguide/grants.html#terms-grant-operations ) HealthLake requires\. See [Using grants](https://docs.aws.amazon.com/kms/latest/developerguide/grants.html)for more information\.

To use your customer managed KMS key with your HealthLake resources, the following API operations must be permitted in the key policy:
+ kms:CreateGrant adds grants to a specific customer managed KMS key which allows access to grant operations\.
+ kms:DescribeKey provides the customer managed key details needed to validate the key\. This is required for all operations\.
+ kms:GenerateDataKey provides access to encrypt resources at rest for all write operations\.
+ kms:Decrypt provides access to read or search operations for encrypted resources\.

The following is a policy statement example that allows a user to create and interact with a Data Store in Amazon HealthLake which is encrypted by that key:

```
    
"Statement": [
    {
        "Sid": "Allow access to create data stores and do CRUD/search in Amazon HealthLake",
        "Effect": "Allow",
        "Principal": {
            "AWS": "arn:aws:iam::111122223333:HealthLakeFullAccessRole"
        },
        "Action": [
            "kms:DescribeKey",
            "kms:CreateGrant",
            "kms:GenerateDataKey",
            "kms:Decrypt"
        ],
        "Resource": "*",
        "Condition": {
            "StringEquals": {
                "kms:ViaService": "healthlake.amazonaws.com",
                "kms:CallerAccount": "111122223333"
            }
        }
    }
]
```

## Required IAM permissions for using a customer managed KMS key<a name="required-iam-cmk"></a>

 When creating a Data Store with AWS KMS encryption enabled using a customer managed KMS key, there are required permissions for both the key policy and the IAM policy for the user or role creating the HealthLake Data Store\.

You can use the [kms:ViaService condition key](https://docs.aws.amazon.com/kms/latest/developerguide/policy-conditions.html#conditions-kms-via-service) to limit use of the KMS key to only requests that originate from HealthLake\.

 For more information about key policies, see [Enabling IAM policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html#key-policy-default-allow-root-enable-iam) in the AWS Key Management Service Developer Guide\. 

The IAM user, IAM role, or AWS account creating your repositories must have the kms:CreateGrant,kms:GenerateDataKey, and kms:DescribeKey permissions plus the necessary HealthLake permissions\.

### How HealthLake uses grants in AWS KMS<a name="grants-kms"></a>

HealthLake requires a [grant](https://docs.aws.amazon.com/kms/latest/developerguide/grants.html) to use your customer managed KMS key\. When you create a Data Store encrypted with a customer managed KMS key, HealthLake creates a grant on your behalf by sending a [CreateGrant](https://docs.aws.amazon.com/kms/latest/APIReference/API_CreateGrant.html) request to AWS KMS\. Grants in AWS KMS are used to give HealthLake access to a KMS key in a customer account\.

The grants that HealthLake creates on your behalf should not be revoked or retired\. If you revoke or retire the grant that gives HealthLake permission to use the AWS KMS keys in your account, HealthLake cannot access this data, encrypt new FHIR resources pushed to the Data Store, or decrypt them when they are pulled\. When you revoke or retire a grant for HealthLake, the change occurs immediately\. To revoke access rights, you should delete the Data Store rather than revoking the grant\. When a Data Store is deleted, HealthLake retires the grants on your behalf\.

### Monitoring your encryption keys for HealthLake<a name="monitoring-kms"></a>

You can use CloudTrail to track the requests that HealthLake sends to AWS KMS on your behalf when using a customer managed KMS key\. The log entries in the CloudTrail log show healthlake\.amazonaws\.com in the userAgent field to clearly distinguish requests made by HealthLake\.

The following examples are CloudTrail events for CreateGrant, GenerateDataKey, Decrypt, and DescribeKey to monitor AWS KMS operations called by HealthLake to access data encrypted by your customer managed key\.

The following shows how to use CreateGrant to allow HealthLake to access a customer provided KMS key, enabling HealthLake to use that KMS key to encrypt all customer data at rest\.

Users are not required to create their own grants\. HealthLake creates a grant on your behalf by sending a CreateGrant request to AWS KMS\. Grants in AWS KMS are used to give HealthLake access to a AWS KMS key in a customer account\.

```
             {
    "eventVersion": "1.08",
    "userIdentity": {
        "type": "AssumedRole",
        "principalId": "EXAMPLEROLE:Sampleuser01",
        "arn": "arn:aws:sts::111122223333:assumed-role/Sampleuser01,
        "accountId": "111122223333",
        "accessKeyId": "EXAMPLEKEYID",
        "sessionContext": {
            "sessionIssuer": {
                "type": "Role",
                "principalId": "EXAMPLEROLE",
                "arn": "arn:aws:iam::111122223333:role/Sampleuser01",
                "accountId": "111122223333",
                "userName": "Sampleuser01"
            },
            "webIdFederationData": {},
            "attributes": {
                "creationDate": "2021-06-30T19:33:37Z",
                "mfaAuthenticated": "false"
            }
        },
        "invokedBy": "healthlake.amazonaws.com"
    },
    "eventTime": "2021-06-30T20:31:15Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "CreateGrant",
    "awsRegion": "us-east-1",
    "sourceIPAddress": "healthlake.amazonaws.com",
    "userAgent": "healthlake.amazonaws.com",
    "requestParameters": {
        "operations": [
            "CreateGrant",
            "Decrypt",
            "DescribeKey",
            "Encrypt",
            "GenerateDataKey",
            "GenerateDataKeyWithoutPlaintext",
            "ReEncryptFrom",
            "ReEncryptTo",
            "RetireGrant"
        ],
        "granteePrincipal": "healthlake.us-east-1.amazonaws.com",
        "keyId": "arn:aws:kms:us-east-1:111122223333:key/EXAMPLE_KEY_ARN",
        "retiringPrincipal": "healthlake.us-east-1.amazonaws.com"
    },
    "responseElements": {
        "grantId": "EXAMPLE_ID_01"
    },
    "requestID": "EXAMPLE_ID_02",
    "eventID": "EXAMPLE_ID_03",
    "readOnly": false,
    "resources": [
        {
            "accountId": "111122223333",
            "type": "AWS::KMS::Key",
            "ARN": "arn:aws:kms:us-east-1:111122223333:key/EXAMPLE_KEY_ARN"
        }
    ],
    "eventType": "AwsApiCall",
    "managementEvent": true,
    "recipientAccountId": "111122223333",
    "eventCategory": "Management"
}
```

The following examples shows how to use GenerateDataKey to ensure the user has necessary permissions to encrypt data before storing it\.

```
             {
    "eventVersion": "1.08",
    "userIdentity": {
        "type": "AssumedRole",
        "principalId": "EXAMPLEUSER",
        "arn": "arn:aws:sts::111122223333:assumed-role/Sampleuser01",
        "accountId": "111122223333",
        "accessKeyId": "EXAMPLEKEYID",
        "sessionContext": {
            "sessionIssuer": {
                "type": "Role",
                "principalId": "EXAMPLEROLE",
                "arn": "arn:aws:iam::111122223333:role/Sampleuser01",
                "accountId": "111122223333",
                "userName": "Sampleuser01"
            },
            "webIdFederationData": {},
            "attributes": {
                "creationDate": "2021-06-30T21:17:06Z",
                "mfaAuthenticated": "false"
            }
        },
        "invokedBy": "healthlake.amazonaws.com"
    },
    "eventTime": "2021-06-30T21:17:37Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "GenerateDataKey",
    "awsRegion": "us-east-1",
    "sourceIPAddress": "healthlake.amazonaws.com",
    "userAgent": "healthlake.amazonaws.com",
    "requestParameters": {
        "keySpec": "AES_256",
        "keyId": "arn:aws:kms:us-east-1:111122223333:key/EXAMPLE_KEY_ARN"
    },
    "responseElements": null,
    "requestID": "EXAMPLE_ID_01",
    "eventID": "EXAMPLE_ID_02",
    "readOnly": true,
    "resources": [
        {
            "accountId": "111122223333",
            "type": "AWS::KMS::Key",
            "ARN": "arn:aws:kms:us-east-1:111122223333:key/EXAMPLE_KEY_ARN"
        }
    ],
    "eventType": "AwsApiCall",
    "managementEvent": true,
    "recipientAccountId": "111122223333",
    "eventCategory": "Management"
}
```

The following example shows how HealthLake calls the Decrypt operation to use the stored encrypted data key to access the encrypted data\.

```
             {
    "eventVersion": "1.08",
    "userIdentity": {
        "type": "AssumedRole",
        "principalId": "EXAMPLEUSER",
        "arn": "arn:aws:sts::111122223333:assumed-role/Sampleuser01",
        "accountId": "111122223333",
        "accessKeyId": "EXAMPLEKEYID",
        "sessionContext": {
            "sessionIssuer": {
                "type": "Role",
                "principalId": "EXAMPLEROLE",
                "arn": "arn:aws:iam::111122223333:role/Sampleuser01",
                "accountId": "111122223333",
                "userName": "Sampleuser01"
            },
            "webIdFederationData": {},
            "attributes": {
                "creationDate": "2021-06-30T21:17:06Z",
                "mfaAuthenticated": "false"
            }
        },
        "invokedBy": "healthlake.amazonaws.com"
    },
    "eventTime": "2021-06-30T21:21:59Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "Decrypt",
    "awsRegion": "us-east-1",
    "sourceIPAddress": "healthlake.amazonaws.com",
    "userAgent": "healthlake.amazonaws.com",
    "requestParameters": {
        "encryptionAlgorithm": "SYMMETRIC_DEFAULT",
        "keyId": "arn:aws:kms:us-east-1:111122223333:key/EXAMPLE_KEY_ARN"
    },
    "responseElements": null,
    "requestID": "EXAMPLE_ID_01",
    "eventID": "EXAMPLE_ID_02",
    "readOnly": true,
    "resources": [
        {
            "accountId": "111122223333",
            "type": "AWS::KMS::Key",
            "ARN": "arn:aws:kms:us-east-1:111122223333:key/EXAMPLE_KEY_ARN"
        }
    ],
    "eventType": "AwsApiCall",
    "managementEvent": true,
    "recipientAccountId": "111122223333",
    "eventCategory": "Management"
}
```

The following example shows how HealthLake uses the DescribeKey operation to verify if the AWS KMS customer owned AWS KMS key is in a usable state and to help a user troubleshoot if it is not functional\.

```
             {
    "eventVersion": "1.08",
    "userIdentity": {
        "type": "AssumedRole",
        "principalId": "EXAMPLEUSER",
        "arn": "arn:aws:sts::111122223333:assumed-role/Sampleuser01",
        "accountId": "111122223333",
        "accessKeyId": "EXAMPLEKEYID",
        "sessionContext": {
            "sessionIssuer": {
                "type": "Role",
                "principalId": "EXAMPLEROLE",
                "arn": "arn:aws:iam::111122223333:role/Sampleuser01",
                "accountId": "111122223333",
                "userName": "Sampleuser01"
            },
            "webIdFederationData": {},
            "attributes": {
                "creationDate": "2021-07-01T18:36:14Z",
                "mfaAuthenticated": "false"
            }
        },
        "invokedBy": "healthlake.amazonaws.com"
    },
    "eventTime": "2021-07-01T18:36:36Z",
    "eventSource": "kms.amazonaws.com",
    "eventName": "DescribeKey",
    "awsRegion": "us-east-1",
    "sourceIPAddress": "healthlake.amazonaws.com",
    "userAgent": "healthlake.amazonaws.com",
    "requestParameters": {
        "keyId": "arn:aws:kms:us-east-1:111122223333:key/EXAMPLE_KEY_ARN"
    },
    "responseElements": null,
    "requestID": "EXAMPLE_ID_01",
    "eventID": "EXAMPLE_ID_02",
    "readOnly": true,
    "resources": [
        {
            "accountId": "111122223333",
            "type": "AWS::KMS::Key",
            "ARN": "arn:aws:kms:us-east-1:111122223333:key/EXAMPLE_KEY_ARN"
        }
    ],
    "eventType": "AwsApiCall",
    "managementEvent": true,
    "recipientAccountId": "111122223333",
    "eventCategory": "Management"
}
```

### Learn more<a name="more-info-kms"></a>

The following resources provide more information about data at rest encryption\.

For more information about [AWS Key Management Service basic concepts](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html), see the AWS KMS documentation\.

For more information about [Security best practices](https://docs.aws.amazon.com/kms/latest/developerguide/best-practices.html) in the AWS KMS documentation\.