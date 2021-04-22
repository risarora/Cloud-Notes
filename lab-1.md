# The Lab Scenario
## Context
Your company is measuring the temperature of water in lakes, ponds, and streams all around your area. They have deployed sensors to each body of water they are monitoring, and the sensors are capable of making HTTPS calls including the sensor id and temperature reading on the payload of the request. The plan is to have the sensors record data every 15 minutes on temperature readings, then upload the data to the AWS data lake via an HTTPS request for each 15 minute interval.

You are tasked with creating a way to ingest data into a data lake being hosted on AWS. The data lake will be using Amazon S3 as the storage layer, and will use Amazon ElasticSearch Service for index and search capabilities. 

You will use Amazon API Gateway to ingest the data being sent from the sensor, which will trigger an AWS Lambda function. This will take the payload of the request and first write a file to an Amazon S3 Bucket where the file name is a combination of the sensorID, the timestamp, and the file contents will be the sensorID, the timestamp, and the temperature reading. The AWS Lambda function will then load the record to Amazon ElasticSearch Service.

This is one way to ingest data that has a relatively small payload for each individual record, but there will be many records, as there will be potentially hundreds of sensors from the area all posting data every 15 minutes.

Once the data is stored in S3, you could then go on to use other tools for analysis for a variety of use cases. For example, maybe you have other weather related data that you are ingesting using another solution, and you could join that data together with the sensor data to provide insights. Another example is maybe there are other people in the organization who want access to the raw data to do their own visualization or analysis using tools they are familiar with.

Data lake architectures often combine many different ingestion methods and analysis methods into one architecture. In this lab, we are focusing on one ingestion solution using API Gateway and Lambda, and using Amazon ElasticSearch as the search and indexing solution. You could use Amazon Kinesis for ingestion and AWS Glue for cataloging the data and we will cover these services in future lessons more in depth. Just remember, that one AWS service is not any better than another AWS service, there are just services that best fit certain use cases- and it's up to you to decide what services you would like to use in your data lake designs.

💁‍♂ Ok, best of luck with this lab. If you get stuck, head over to the forums.

 

## Accessing the AWS Management Console
At the top of these instructions, click Start Lab to launch your lab.

1. A Start Lab panel opens displaying the lab status.
2. Wait until you see the message "Lab status: ready", then click the X to close the Start Lab panel.
3. At the top of these instructions, click AWS
4. This will open the AWS Management Console in a new browser tab. The system will automatically log you in.    

**TIP:** If a new browser tab does not open, there will typically be a banner or icon at the top of your browser indicating that your browser is preventing the site from opening pop-up windows. Click on the banner or icon and choose "Allow pop ups."

Arrange the AWS Management Console tab so that it displays along side these instructions. Ideally, you will be able to see both browser tabs at the same time, to make it easier to follow the lab steps.

Setup
Download the following zip as it will be used in Stage 3 for the Lambda Function:
```
https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-Designing_DataLakes/week2/upload-data.zip
```

## Lab Steps
### Stage 1 - Creating an Amazon Elasticsearch Service Cluster
You will be using Amazon Elasticseach Service for it's cataloging and indexing capabilities. Before you can start ingesting documents to your Amazon ES domain, you must first create it. You could also use AWS Glue for cataloging your data, and you will explore that service in a future lesson.

In this step, you will create an Amazon ES domain.

Choose Services and search for Elasticsearch Service.  Choose Create a new domain.  Choose Development and testing. Leave the Elasticsearch version as the latest. Choose Next.  Paste the following for Elasticsearch domain name:

```
water-temp-domain
```

Leave the remaining settings as is.  Choose Next.  

Choose Public access under Network configuration.  Uncheck the box for Enable fine-grained access control.  

Scroll down to Access policy.  Next to Domain access policy ensure Custom access policy is selected.  

Underneath Domain access policy there is a spot to configure a principal that will be allowed to access the domain. You are going to restrict access to the Amazon ES domain by IPv4 address.  First find your IPv4 address by using an online lookup service such as:https://www.whatismyip.com/.  Take note of your IPv4 address.  

For Select Type choose IPv4 address. Under Enter Principal paste in your IPv4 address. For Select Action choose Allow. Choose Next.  

At the review page notice our Policy is only allowing access to our ES domain to our IPv4 address which is exactly what we want:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": [
        "es:*"
      ],
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": [
            "x.x.x.x"
          ]
        }
      },
      "Resource": "arn:aws:es:us-west-2:000000000000:domain/water-temp-domain/*"
    }
  ]
}
```
Choose Confirm.  This can take up to 15 minutes to complete. 

In this next section you will use a FMI or Fill Me In.  They will be designated by . Make sure to remove the <> when entering them. 

### Stage 2 - Create an Amazon S3 Bucket
Though you are loading your data into Amazon ES, Amazon S3 will be the storage layer for your data lake, and you are just using Amazon ES for one specific use case. You will be loading the data into both Amazon ES and Amazon S3, with the idea that with a data lake you likely will have multiple use cases for the data, and each use case will use it's own set of appropriate services and tooling. By storing the raw data in Amazon S3, it makes it accessible for many use cases and a large variety of services.

In this step, you will create an Amazon S3 bucket.

Choose Services and search for S3.  Choose the orange Create bucket.  

The bucket name must be globally unique and DNS compliant. Name the bucket something like:

datalakes-week2-<FMI> using your initials for the Fill Me In
​
If bucket name is still taken add some numbers to the end of it
Example:

      datalakes-week2-emr
​
datalakes-week2-emr1220
Under Region Ensure the bucket region is the same region your ES cluster is located in. It should be US East (N. Virginia) us-east-1. Choose Create bucket. Take note of the bucket name as it will be needed later.

Take note of the name you gave to your S3 bucket. You will need this in future steps.

Now you have a S3 bucket which will be the storage layer for your data lake. We will come back to this shortly and modify the bucket access policy so that AWS Lambda can write files to the bucket. We will cover what bucket access policies do in future lessons.

In this next section you will create the AWS Lambda function.

### Stage 3 - Create the AWS Lambda Function
AWS Lambda is server-less compute that runs when triggered. The code that is uploaded to a Lambda function does not run continually, instead it runs when triggered by an event.

The AWS Lambda function you will create is already written for you, and all you need to do is create and configure the function.

This Lambda function will capture the data that is on the payload of the incoming request, and upload a JSON document first to S3 then to Amazon ES.

Choose Services and search for Lambda. Choose Create function. 

Leave Author from scratch selected. For Function name paste in the following:

      upload-data
      
For Runtime choose Python 3.8. Under Permissions expand Change default execution role. 

Choose Use an existing role and choose data-lake-week-2. Choose Create function. 

The AWS Lambda function code will need access to permissions to sign API calls that write to S3 and Amazon ES. This role was already created for you containing the correct permissions, choose the existing role.

Scroll down to Function code. Choose Actions and Upload a .zip file. Choose Upload and browse to where the upload-data.zip file was saved. Choose Save. You will need to move the contents of the zip folder to the top level upload-data - / folder.  Make sure it looks like the following:

        image-20201215102828031

This code is prewritten, though feel free to look through it if you're curious.

Choose Deploy and scroll down to Runtime settings.  Choose Edit. 
Under Handler replace the existing text with lambda.handler and choose Save. 
The handler of a lambda function is the entry point for the code. In this step you are telling AWS Lambda at what function to begin running the code.

Under Environment variables choose Edit. Choose Add environment variable. 
Some of the information needed for the code to run is dependent on your personal AWS account, like the Amazon S3 bucket name and the Amazon ES domain that you created in earlier steps.

Under Key put: S3_BUCKET. Under Value paste in your bucket name. Example:

    datalakes-week2-emr
You will add another environment variable for the Amazon ES domain in a future step.

Choose Save. Choose the Permissions tab at the top. Choose the data-lake-week-2 link under Role name. This will open the IAM console. 

Copy the Role ARN at the top which should look similar to:

      arn:aws:iam::000000000000:role/data-lake-week-2
This is needed for Stage 4. 

In the next section you will modify the S3 bucket to allow for lambda access. 

### Stage 4 - Modify S3 Bucket Policy for Lambda Access
The AWS Lambda function will be writing data to the Amazon S3 bucket. You already associated an IAM Role with the AWS Lambda function, but that alone is not enough to allow access. You also must modify the S3 bucket policy, which allows or denies AWS principals access to the bucket.

Choose Services and search for S3. Choose the bucket created in Stage 2. Choose the Permissions tab. Choose Bucket Policy. 

Make sure to replace the first  in the following JSON with the Lambda role ARN:
```
{
    "Version": "2012-10-17",
    "Id": "ExamplePolicy",
    "Statement": [
        {
            "Sid": "ExampleStmt",
            "Effect": "Allow",
            "Principal": {
                "AWS": "<FMI>"
            },
            "Action": "s3:*",
            "Resource": "<FMI>/*"
        }
    ]
} 
Example:

         "Principal": {
             "AWS": "arn:aws:iam::356682777738:role/data-lake-week-2"
         },
Replace the second  with your bucket name:

Example:

         "Action": "s3:*",
         "Resource": "arn:aws:s3:::datalakes-week2-emr/*"
     }
So it should look like the following (with your account number and bucket name):

{
    "Version": "2012-10-17",
    "Id": "ExamplePolicy",
    "Statement": [
        {
            "Sid": "ExampleStmt",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::000000000000:role/data-lake-week-2"
            },
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::datalakes-week2-xxx/*"
        }
    ]
}
```
Paste this into the Bucket policy editor. Choose Save changes. This will allow the Lambda function to upload the temperature files to your bucket.

Choose Services and choose Elasticsearch Service. Choose the water-temp-domain. The Domain status should now say Active. If it's not active yet, please wait a couple more minutes and refresh the page until it is. Also make sure you are in the N. Virginia region.

Make note of the Endpoint which should look something like the following:

https://search-water-temp-domain-xxxxxxxxxxxxxxxxxxxxxxxxx.us-east-1.es.amazonaws.com
Choose Actions and choose Modify access policy. Currently the policy restricts access by IP Address. We also want to allow the Lambda function to have access. The current policy should look similar to the following:

Example:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:us-east-1:000000000000:domain/water-temp-domain/*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "x.x.x.x"
        }
      }
    }
  ]
}
```
We need to add Lambda access to the policy. So it will need to look like this (with your account number and IP address):
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:us-east-1:000000000000:domain/water-temp-domain/*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "x.x.x.x"
        }
      }
    },
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::000000000000:role/data-lake-week-2"
      },
      "Action": "es:*",
      "Resource": "arn:aws:es:us-east-1:000000000000:domain/water-temp-domain/*"
    }
  ]
}
```
Choose Submit. 

In the next step you will modify the AWS lambda function and create an API to publish and test out the solution.

### Stage 5 - Modify AWS Lambda Function & Create Amazon API Gateway
Now that you have an Amazon ES domain and Amazon S3 bucket, you will need to modify one final thing for your AWS Lambda function to work. 

Once the lambda function is configured, you will need a way to run the function. Lambda functions are run based on triggers, and in this case the sensors recording the temperature data are making HTTPS POST requests with the data on the payload. The service Amazon API Gateway will be used to create an API endpoint where the HTTPS POST requests will be received. Once API Gateway receives and validates the request, it will trigger and pass the information to the Lambda function which will then write the data to Amazon S3 and Amazon ES.

Choose Services and search for Lambda. Choose the upload-data function. Scroll down to the Environment variables section. Choose Edit. 

Choose Add environment variable. Under Key put: ES_DOMAIN_URL. For the Value paste in your ES endpoint which you jotted down earlier, which should look similar to the following:

    https://search-water-temp-domain-xxxxxxxxxxxxxxxxxxxxxxxxx.us-east-1.es.amazonaws.com
Choose Save. 

Choose Services and search for API Gateway. Find the REST API. Choose Build. Choose OK.

Choose New API. For API name paste in: sensor-data. Choose Create API. 

Choose Actions and Create Method. Choose the drop down and choose POST. Choose the small checkmark at the right.

Leave Integration type as Lambda Function. Under Lambda Function start typing upload-data and then select it when it comes up.

Choose Save. Choose OK. 

Choose TEST. Scroll down to Request Body and paste the following:
```
{
"sensorID" : "0025",
"temperature" : "67"
}
```
Choose Test. You should see something similar to the following in the Response Body:
```
{
  "Response": "Data Uploaded",
  "sensorID": "0025",
  "temperature": "67"
}
```
This test is simulating the POSTs that would be coming in from the different IoT sensors.

In this next section you will use a FMI or Fill Me In.  They will be designated by . Make sure to remove the <> when entering them.

Your Amazon ES domain will allow you to search your data from the browser by submitting a GET request.  You will need your Amazon ES domain for this next step.  So make sure you have it.  

### Stage 6 - Check Amazon ES for data
Open a text editor of your choice and paste the following text along with your domain URL into the editor.

<FMI>/lambda-s3-index/lambda-type/_search?pretty
Example:

https://search-water-temp-domain-xxxxxxxxxxxxxxxxxxxxxxxxxx.us-east-1.es.amazonaws.com/lambda-s3-index/lambda-type/_search?pretty
Copy the search URL and paste it into a new tab in your browser.

You should be able to see some test index data being returned. Feel free to run a few more tests using different sensorID's and temperatures in the API gateway test.  So for example paste the following into the Request Body:
```
{
"sensorID" : "0026",
"temperature" : "70"
}
```
Choose Text. 

Choose Services and  S3.  Choose the bucket. 

You should see several .json files.  If you download one it should contain the test data that was sent via API Gateway:

      {"sensorID": "0026", "timestamp": "20201019153601", "temperature": "70"}

In the real world your data wouldn't be origination from API Gateway. It would be coming from a fleet of sensors and devices. Using API Gateway tests is an easy way for us to generate a POST request as if it was coming from outside AWS. In reality API Gateway would accepting the requests from an external device and then triggering the backend.

 

Through your creation of the Amazon ES domain, it also gave you access to Kibana. Feel free to explore Kibana to view and analyze the data loaded into the Amazon ES domain.

Ending the lab
At the top of these instructions, click End Lab.
A pop up will ask you to confirm this.  choose Yes.  
