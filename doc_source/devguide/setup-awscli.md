# Set up the AWS Command Line Interface \(AWS CLI\)<a name="setup-awscli"></a>

You don't need the AWS CLI to perform the steps in all the getting started exercises\. However, some of the other exercises in this guide do require it\. 



**To set up the AWS CLI**

1. Download and configure the AWS CLI\. For instructions, see the following topics in the *AWS Command Line Interface User Guide*: 
   + [Getting Set Up with the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html)
   + [Configuring the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)

1. In the AWS CLI `config` file, add a named profile for the administrator\. 

   ```
   [profile adminuser]
   aws_access_key_id = adminuser access key ID
   aws_secret_access_key = adminuser secret access key
   region = aws-region
   ```

   You use this profile when running the AWS CLI commands\. Under the security principle of least privilege, we recommend that you create a separate IAM role with privileges specific to the tasks being performed\. For more information about named profiles, see [Named Profiles](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-multiple-profiles) in the *AWS Command Line Interface User Guide*\. For a list of AWS Regions, see [Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html) in the *Amazon Web Services General Reference*\.

1. Verify the setup by typing the following help command at the command prompt\. 

   ```
   aws healthlake help
   ```

    If the AWS CLI is configured correctly, you will see a brief description of Amazon HealthLake and a list of available commands\. 

1. Amazon HealthLake is available only in the US East Northern Virginia \(us\-east\-1\) Region\. You don't need to specify the "\-\-endpoint" option when using the AWS CLI, but you can if necessary\. The endpoint is https://aws68918\.us\-east\-1\.amazonaws\.com/\.

    For example, to list all of the HealthLake FHIR Data Stores that you own, you use the following command\.

   ```
   $ aws healthlake list-fhir-datastores \
   ```