Craete the database using AWS RDS:

  * Use the AWS console to create a new database (postgres).
  * Follow instructions, and make sure you allow connections to your database.
  * Check databse using any software availble


----

ElasticBeanstalk Cli: 

  * First you need to install the ElasticBeanstalk using the following [Link](https://github.com/aws/aws-elastic-beanstalk-cli-setup)
  * Start EB Environment & Application using:
          cd ./udagram/udagram-api/
          eb init <APP_NAME> --platform Node.js --region <REGOIN>

  * New folder will appear inside the udagram-api directory called _.elasticbeanstalk_
  * Create Elastic environment using the following command:

           eb create --sample <ENVIRONMENT_NAME>

  * when the creation process is over, you will be able to check the EB using the command `` eb open ``
  * Now add the desired Environments variables to the EB using:
        AWS CONSOLE -> Elastic Beanstalk -> APP_NAME -> Configuration -> Software -> Add Environtment variables


| Environment Variable | Usage |
|:--------------------:| ----- |
| POSTGRES_HOST | The database host used for connection |
| POSTGRES_DB | The Database name |
| POSTGRES_USERNAME | The database username |
| POSTGRES_PASSWORD | The database password |
| DB_PORT | The database port |
| PORT | The server's port |
| JWT_SECRET | The jwt secret password |
| URL | the S3 APP URL |
| AWS_BUCKET | The s3 bucket ARN |
| AWS_REGION | the s3 region |
| AWS_PROFILE | The s3 profile |

  * Build your API using the following command inside the udagram-api directory:
           npm run build
           
  * Deploy API to the EB by using the following commands:
          eb use ENVIRONMENT_NAME
          eb deploy ENVIRONMENT_NAME
          
  * Now you can access AWS S3 and it's Connected to the AWS EB API.

----
*AWS Cli*
  * Setup the AWS CLI to connect to AWS s3 and copy files from [Here](https://awscli.amazonaws.com/AWSCLIV2.msi)
  * start the AWS configuration by running this command:
  
           aws configure
           
    | Requirements | Defination |
    | :----------: | :--------- |
    |**AWS_ACCESS_KEY_ID**| The AWS Access key ID which will is used for AWS services |
    |**AWS_SECRET_ACCESS_KEY** | The AWS Secret key for the used AWS ID |
    |**AWS_DEFAULT_REGION** | The desired region to use AWS services |
    | **Output** | The data output type to use _json_ |
  
  * Create the S3 Bucket:

          aws s3api create-bucket --bucket <YOUR-BUCKET-NAME> --region <CHOOSE-REGION>
          
      > NOTE: Change *YOUR-BUCKET-NAME* with the desired name for your Bucket, and change *CHOOSE-REGION* with the desired AWS region
  
  *  Enable your AWS S3 Bucket *Static Website*:
  
  		  	aws s3 website s3://<BUCKET_NAME>/ --index-document index.html

  * Make sure your AWS website is running using your AWS s3 Link:
 
       **http://`BUCKET_NAME`.s3-website-`REGION`.amazonaws.com**

  * Change the link to the API into ``` udagram/udagram-frontend/src/environments/ ``` in both files to be:
          apiHost: 'Http://<YOUR_EB_DIRECT_LINK>/api/v0'
          
  * Build FrontEnd and Upload files to the *AWS S3 Bucket*:

          cd ./udagram/udagram-frontend/
          npm run build
          aws s3 cp --recursive ./www s3://<BUCKET-NAME> --acl public-read
          

----