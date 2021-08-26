# Tagging resources in Amazon HealthLake<a name="tagging"></a>

## Important notice<a name="important-notice-tagging"></a>

Amazon HealthLake protects customer data under the AWS Shared Responsibility Model policies\. This means that all customer data is encrypted both in transition and at\-rest\. However, not all customer\-inputed names for Data Stores or job\-based operations are encypted\. They should never contain Personally Identifiable Information or Protected Health Information\. For more information, see the Amazon HealthLake Security chapter\.

## Tagging using HealthLake resources<a name="tagging-using-healthlake"></a>

You can assign metadata to your AWS resources in the form of *tags*\. Each tag is a label consisting of a user\-defined key and value\. Tags can help you manage, identify, organize, search for, and filter resources\. 

This topic describes commonly used tagging categories and strategies to help you implement a consistent and effective tagging strategy\. The following sections assume basic knowledge of AWS resources, tagging, detailed billing, and AWS Identity and Access Management \(IAM\)\.

Each tag has two parts:
+ A *tag key* \(for example, CostCenter, Environment, or Project\)\. Tag keys are case sensitive\.
+ A *tag value* \(for example, 111122223333 or Production\)\. Like tag keys, tag values are case sensitive\.

You can use tags to categorize resources by purpose, owner, environment, or other criteria\. For more information, see [AWS Tagging Strategies](https://d1.awsstatic.com/whitepapers/aws-tagging-best-practices.pdf)\.

 You can add, change, or remove tags one resource at a time from each resource’s service console, service API, or the AWS CLI\.

To enable tagging, make sure TagResources are authorized\. You can authorize TagResources by attaching an IAM policy like the following example\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "healthlake:CreateFHIRDatastore",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "healthlake:TagResource",
            "Resource": "*"
        }
    ]
}
```

## Best practices<a name="best-practices-tagging"></a>

As you create a tagging strategy for AWS resources, follow best practices: 
+ Do not store Personally Identifiable Information \(PII\), Personal Health Information\(PHI\) or other sensitive information in tags\.
+ Use a standardized, case\-sensitive format for tags, and apply it consistently across all resource types\.
+ Consider tag guidelines that support multiple purposes, like managing resource access control, cost tracking, automation, and organization\.
+ Use automated tools to help manage resource tags\. [AWS Resource Groups](https://docs.aws.amazon.com/ARG/latest/userguide/welcome.html) and the [Resource Groups Tagging API](https://docs.aws.amazon.com/resourcegroupstagging/latest/APIReference/overview.html) enable programmatic control of tags, making it possible to automatically manage, search, and filter tags and resources\.
+ Tagging is more effective when you use more tags\.
+ Tags can be edited or modified as user needs change, however to update access control tags, you must also update the policies that reference those tags to control access to your resources\.

## Tagging requirements<a name="tagging-requirements"></a>

Tags have the following requirements:
+ Keys can't be prefixed with aws:\.
+ Keys must be unique per tag set\.
+ A key must be between 1 and 128 allowed characters\.
+ A value must be between 0 and 256 allowed characters\.
+ Values do not need to be unique per tag set\.
+ Allowed characters for keys and values are Unicode letters, digits, white space, and any of the following symbols: \_ \. : / = \+ \- @\.
+ Keys and values are case sensitive\.