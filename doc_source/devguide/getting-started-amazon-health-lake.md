# Account set up with Amazon HealthLake<a name="getting-started-amazon-health-lake"></a>

## Sign up for AWS<a name="setting-up-signup-healthlake"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all AWS services\. For access to Amazon HealthLake during the public preview, you need to request access through the AWS Management Console first\. 

If you are a new AWS customer, you can get started with Amazon HealthLake for free\. For more information, see [AWS Free Usage Tier](https://aws.amazon.com/free/)\.

If you already have an AWS account, skip to the next section\. 

**To create an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

Record your AWS account ID because you'll need it for the next task\.

## Create an IAM User<a name="setting-up-iam-amazon-healthlake"></a>

Services in AWS, such as Amazon HealthLake, require that you provide credentials to access them\. This allows the service to determine whether you have permissions to access the service's resources\. 

We strongly recommend that you access AWS using AWS Identity and Access Management \(IAM\), not the credentials for your AWS account\. To use IAM to access AWS, create an IAM user, add the user to an IAM group with administrative permissions, and then grant administrative permissions to the IAM user\. You can then access AWS using a special URL and the IAM user's credentials\.

The getting started exercises in this guide assume that you have a user with administrator privileges, `adminuser`\. 

**To create an administrator and sign in to the console**

1. Create a user named `adminuser` in your AWS account\. For instructions, see [Creating Your First IAM User and Administrators Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

1. Sign in to the AWS Management Console using a special URL\. For more information, see [How Users Sign In to Your Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_how-users-sign-in.html) in the *IAM User Guide*\.

1. To ensure that all necessary users and roles have access to HealthLake, attach a permission policy to grant access to the service\. The following is an example granting access to HealthLake\. 

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Action": [
                   "healthlake:*"
               ],
               "Resource": "*",
               "Effect": "Allow"
           }
       ]
   }
   ```

For more information about IAM, see the following:
+ [AWS Identity and Access Management \(IAM\)](https://aws.amazon.com/iam/)
+ [Getting started](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html)
+ [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)

## Next step: Setting up the AWS CLI<a name="setting-up-next-step-2-amazon-health-lake"></a>