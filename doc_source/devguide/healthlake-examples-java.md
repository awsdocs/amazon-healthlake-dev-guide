# Creating a FHIR Data Store using the AWS SDK for Java<a name="healthlake-examples-java"></a>

The following example uses the `CreateFHIRDatastore` operation with Java\. To run the example, install the AWS SDK for Java\. For instructions on installing the AWS SDK for Java, see [ Set up the AWS SDK for Java](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-install.html)\. 

```
import com.amazonaws.auth.AWSCredentials;
import com.amazonaws.auth.AWSCredentialsProvider;
import com.amazonaws.auth.DefaultAWSCredentialsProviderChain;
 
import com.amazonaws.services.HealthLake.AWSHealthLake;
import com.amazonaws.services.HealthLake.AWSHealthLakeClient;
import com.amazonaws.services.HealthLake.model.CreateFHIRDatastoreRequest;
import com.amazonaws.services.HealthLake.model.CreateFHIRDatastoreResult;
import com.amazonaws.services.HealthLake.model.DescribeFHIRDatastoreRequest;
import com.amazonaws.services.HealthLake.model.DescribeFHIRDatastoreResult;
import com.amazonaws.services.HealthLake.model.FHIRVersion;
import com.amazonaws.services.HealthLake.model.ListFHIRDatastoresRequest;
import com.amazonaws.services.HealthLake.model.ListFHIRDatastoresResult;
import com.amazonaws.services.HealthLake.model.PreloadDataConfig;
import com.amazonaws.services.HealthLake.model.PreloadDataType;
 
public class App{
 
    public static void main( String[] args ) {
 
        // Create credentials using a provider chain. For more information, see
        // https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html
        AWSCredentialsProvider awsCreds = DefaultAWSCredentialsProviderChain.getInstance();
 
        AWSHealthLake awsHealthLake = AWSHealthLakeClient.builder()
            .withRegion("us-east-1").withCredentials(awsCreds).defaultClient();
 
        CreateFHIRDatastoreRequest createFHIRDatastoreRequest = new CreateFHIRDatastoreRequest()
            .withData StoreName("TestDatastore123")
            .withData StoreTypeVersion(FHIRVersion.R4)
            .withPreloadDataConfig(new PreloadDataConfig()
                .withPreloadDataType(PreloadDataType.SYNTHEA));
 
        

    }
}
```