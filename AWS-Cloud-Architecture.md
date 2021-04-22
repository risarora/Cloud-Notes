# AWS Data Lake
![image](https://user-images.githubusercontent.com/4485129/115526354-8f2c0200-a2ad-11eb-836d-9bb8de0c47f1.png)

# Week 2
We'll explore AWS services that can be used in data lake architectures, like Amazon S3, AWS Glue, Amazon Athena, Amazon Elasticsearch Service, LakeFormation, Amazon Rekognition, API Gateway and other services used for data movement, processing and visualization.

1. Storage and cataloguing
2. Data Movement
3. Analytics and processing


### 1. Storage and cataloguing
<details>
The first category is AWS services used for data storage and cataloguing. And data lake has a few key components. It stores and secures data at an unlimited scale. It allows for structured and unstructured data to be stored together. It catalogs and indexes data without data movement, and it connects data with services and tooling for analysis and processing. So, what AWS services can you use to enable these key factors of a data lake? We will cover that with the AWS services used for data storage and cataloguing.
 
![image](https://user-images.githubusercontent.com/4485129/115531164-167b7480-a2b2-11eb-8fb5-b9310aef2a3e.png)

#### Storage - S3 is the most popular choice for storage option for a Lake
* Schema on Read model
* Supports Scaling
* Data Agnostic
* Data is stored in Buckets which are scalable
* S3 and S3 Glacier are preferred
* High Durability - 
  * 99.999999999.% Durability supported by S3
*  Pricing tiers based on frequency of the data access
  
![image](https://user-images.githubusercontent.com/4485129/115532802-c1406280-a2b3-11eb-9299-8163ef433628.png)


#### Catalog - AWS Glue Data Catalog

* AWS Glue is a fully managed, serverless data processing and cataloging service.

AWS Glue Data Catalog consists of tables, which are the metadata definition that represents your data. 
A table consists of a schema, and tables are then organized into logical groups called databases. 
You used what is called a glue crawler to populate the AWS Glue Data Catalog with tables. 

<details>
 
## Amazon S3 and Glue Data Catalog
### Amazon S3 
Amazon Simple Storage Service is storage for the Internet. It is designed to make web-scale computing easier for developers.

Amazon S3 has a simple web services interface that you can use to store and retrieve any amount of data, at any time, from anywhere on the web. It gives any developer access to the same highly scalable, reliable, fast, inexpensive data storage infrastructure that Amazon uses to run its own global network of web sites. The service aims to maximize benefits of scale and to pass those benefits on to developers. 

Amazon S3 is the largest and most performant object storage service for structured and unstructured data and the storage service of choice to build a data lake. With Amazon S3, you can cost-effectively build and scale a data lake of any size in a secure environment where data is protected by 99.999999999% (11 9s) of durability.   

Read more about Amazon S3 and data lakes here: https://aws.amazon.com/products/storage/data-lake-storage/

### Amazon S3 Storage Classes
For performance-sensitive use cases (those that require millisecond access time) and frequently accessed data, Amazon S3 provides the following storage classes: S3 Standard—The default storage class. If you don't specify the storage class when you upload an object, Amazon S3 assigns the S3 Standard storage class. Reduced Redundancy—The Reduced Redundancy Storage (RRS) storage class is designed for noncritical, reproducible data that can be stored with less redundancy than the S3 Standard storage class. 

The S3 Standard-IA and S3 One Zone-IA storage classes are designed for long-lived and infrequently accessed data. (IA stands for infrequent access.) S3 Standard-IA and S3 One Zone-IA objects are available for millisecond access (same as the S3 Standard storage class). Amazon S3 charges a retrieval fee for these objects, so they are most suitable for infrequently accessed data.   

The S3 Glacier and S3 Glacier Deep Archive storage classes are designed for low-cost data archiving. These storage classes offer the same durability and resiliency as the S3 Standard storage class.   

The S3 Intelligent-Tiering storage class is designed to optimize storage costs by automatically moving data to the most cost-effective storage access tier, without performance impact or operational overhead. S3 Intelligent-Tiering delivers automatic cost savings by moving data on a granular object level between two access tiers, a frequent access tier and a lower-cost infrequent access tier, when access patterns change. The Intelligent-Tiering storage class is ideal if you want to optimize storage costs automatically for long-lived data when access patterns are unknown or unpredictable.   

Read more about storage classes here: https://docs.aws.amazon.com/AmazonS3/latest/dev/storage-class-intro.html  

### AWS Glue  
AWS Glue is a fully managed ETL (extract, transform, and load) service that makes it simple and cost-effective to categorize your data, clean it, enrich it, and move it reliably between various data stores and data streams. AWS Glue consists of a central metadata repository known as the AWS Glue Data Catalog, an ETL engine that automatically generates Python or Scala code, and a flexible scheduler that handles dependency resolution, job monitoring, and retries. AWS Glue is serverless, so there’s no infrastructure to set up or manage.   

The AWS Glue Data Catalog is your persistent metadata store. It is a managed service that lets you store, annotate, and share metadata in the AWS Cloud in the same way you would in an Apache Hive metastore.    

AWS Glue also lets you set up crawlers that can scan data in all kinds of repositories, classify it, extract schema information from it, and store the metadata automatically in the AWS Glue Data Catalog. The AWS Glue Data Catalog can then be used to guide ETL operations.   

Crawlers use classifiers, a classifier reads the data in a data store. If it recognizes the format of the data, it generates a schema. The classifier also returns a certainty number to indicate how certain the format recognition was.   

Read more about crawlers and classifiers here: https://docs.aws.amazon.com/glue/latest/dg/add-classifier.html  

</details>
</details>

### 2. Data Movement
<details>

#### AWS API Gateway

![image](https://user-images.githubusercontent.com/4485129/115541722-19c82d80-a2bd-11eb-9a68-eb1f6d60f100.png)

![image](https://user-images.githubusercontent.com/4485129/115542303-c60a1400-a2bd-11eb-81a5-56e1a3ddd910.png)


Data Movement
Data Movement   
Data Lakes allow you to import any amount of data that can come in real-time. Data is collected from multiple sources, and moved into the data lake in its original format. This process allows you to scale to data of any size, while saving time of defining data structures, schema, and transformations.   

Read more about data lakes on AWS here: https://aws.amazon.com/big-data/datalakes-and-analytics/https://aws.amazon.com/big-data/datalakes-and-analytics/what-is-a-data-lake/  

#### Amazon Kinesis 
Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information. Amazon Kinesis offers key capabilities to cost-effectively process streaming data at any scale, along with the flexibility to choose the tools that best suit the requirements of your application. With Amazon Kinesis, you can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications. Amazon Kinesis enables you to process and analyze data as it arrives and respond instantly instead of having to wait until all your data is collected before the processing can begin.     

There are multiple services in the Amazon Kinesis family. For data ingestion, there is Amazon Kinesis Data Streams, Amazon Kinesis Video Streams, and Amazon Kinesis Data Firehose.   Read more about Amazon Kinesis here: https://aws.amazon.com/kinesis/    

To better understand each service please review the diagrams below.       

###### Amazon Kinesis Video Streams:    
![image](https://user-images.githubusercontent.com/4485129/115542764-3c0e7b00-a2be-11eb-85e6-1b8a0f0226aa.png)

##### Amazon Kinesis Data Streams:     
![image](https://user-images.githubusercontent.com/4485129/115542827-4e88b480-a2be-11eb-9ec7-189030d09ad2.png)

##### Amazon Kinesis Data Firehose:
![image](https://user-images.githubusercontent.com/4485129/115542846-55afc280-a2be-11eb-8e5b-0fffd35eb65c.png)


### Amazon API Gateway   
Amazon API Gateway is a fully managed service that makes it easy to create, publish, and maintain secure APIs at scale. APIs are the front door to backend applications and services. API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, CORS support, authorization and access control, throttling, monitoring, and API version management.   

Read more about API Gateway here: https://aws.amazon.com/api-gateway/
</details>

### 3.  analytics and processing
<details>
 
### EMR, Glue Jobs, Lambda, Kinesis Analytics, RedShift

#### Apache Hadoop on AWS   
Apache Hadoop is an open source framework that is used to efficiently store and process large datasets ranging in size from gigabytes to petabytes of data. Instead of using one large computer to store and process the data, Hadoop allows clustering multiple computers to analyze massive datasets in parallel more quickly.   

Read more about Hadoop here: https://aws.amazon.com/emr/details/hadoop/what-is-hadoop/  

#### Amazon EMR    
Amazon EMR is a managed cluster platform that simplifies running big data frameworks, such as Apache Hadoop and Apache Spark, on AWS to process and analyze vast amounts of data. By using these frameworks and related open-source projects, such as Apache Hive and Apache Pig, you can process data for analytics purposes and business intelligence workloads. Additionally, you can use Amazon EMR to transform and move large amounts of data into and out of other AWS data stores and databases, such as Amazon Simple Storage Service (Amazon S3) and Amazon DynamoDB.   

Read more about Amazon EMR here: https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html    

#### AWS Glue Jobs   
A job is the business logic that performs the extract, transform, and load (ETL) work in AWS Glue. When you start a job, AWS Glue runs a script that extracts data from sources, transforms the data, and loads it into targets. You can create jobs in the ETL section of the AWS Glue console.    

![image](https://user-images.githubusercontent.com/4485129/115675081-e690a780-a36b-11eb-9b09-135be87a7d1d.png)

Read more about authoring AWS Glue jobs here: https://docs.aws.amazon.com/glue/latest/dg/author-job.html  

#### AWS Lambda 
AWS Lambda is a compute service that lets you run code without provisioning or managing servers. AWS Lambda runs your code only when needed and scales automatically, from a few requests per day to thousands per second. You pay only for the compute time you consume - there is no charge when your code is not running. With AWS Lambda, you can run code for virtually any type of application or backend service - all with zero administration. AWS Lambda runs your code on a high-availability compute infrastructure and performs all of the administration of the compute resources, including server and operating system maintenance, capacity provisioning and automatic scaling, code monitoring and logging.   

When using AWS Lambda, you are responsible only for your code. AWS Lambda manages the compute fleet that offers a balance of memory, CPU, network, and other resources. This can be helpful when processing incoming data for your data lake being hosted on AWS.   

Read more about AWS Lambda here: https://docs.aws.amazon.com/lambda/latest/dg/welcome.html  

#### Amazon Athena  
Amazon Athena is an interactive query service that makes it easy to analyze data directly in Amazon Simple Storage Service (Amazon S3) using standard SQL. With a few actions in the AWS Management Console, you can point Athena at your data stored in Amazon S3 and begin using standard SQL to run ad-hoc queries and get results in seconds. 

Read more about Athena here: https://docs.aws.amazon.com/athena/latest/ug/what-is.html 

#### Amazon RedShift
Amazon Redshift makes it simple and cost effective to run high performance queries on petabytes of structured data so that you can build powerful reports and dashboards using your existing business intelligence tools.   

Read more about Amazon RedShift here: https://aws.amazon.com/redshift/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc    

#### Amazon Kinesis Data Analytics    
With Amazon Kinesis Data Analytics for SQL Applications, you can process and analyze streaming data using standard SQL. The service enables you to quickly author and run powerful SQL code against streaming sources to perform time series analytics, feed real-time dashboards, and create real-time metrics.   

To get started with Kinesis Data Analytics, you create a Kinesis data analytics application that continuously reads and processes streaming data. The service supports ingesting data from Amazon Kinesis Data Streams and Amazon Kinesis Data Firehose streaming sources. Then, you author your SQL code using the interactive editor and test it with live streaming data. You can also configure destinations where you want Kinesis Data Analytics to send the results.   Kinesis Data Analytics supports Amazon Kinesis Data Firehose (Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk), AWS Lambda, and Amazon Kinesis Data Streams as destinations.   

Read more about Amazon Kinesis Data Analytics here: https://docs.aws.amazon.com/kinesisanalytics/latest/dev/what-is.html  

#### Amazon Elasticsearch Service  
Amazon Elasticsearch Service (Amazon ES) is a managed service that makes it easy to deploy, operate, and scale Elasticsearch clusters in the AWS Cloud. Elasticsearch is a popular open-source search and analytics engine for use cases such as log analytics, real-time application monitoring, and clickstream analysis. With Amazon ES, you get direct access to the Elasticsearch APIs; existing code and applications work seamlessly with the service.   

Read more about Amazon ES here: https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/what-is-amazon-elasticsearch-service.html  


</details>


## AWS Lake Formation

AWS Lake Formation makes it easier for you to build, secure, and manage data lakes. Lake Formation helps you do the following, either directly or through other AWS services:  

Register the Amazon Simple Storage Service (Amazon S3) buckets and paths where your data lake will reside.
Orchestrate data flows that ingest, cleanse, transform, and organize the raw data.
Create and manage a Data Catalog containing metadata about data sources and data in the data lake.
Define granular data access policies to the metadata and data through a grant/revoke permissions model.
The following diagram illustrates how data is loaded and secured in Lake Formation.

![image](https://user-images.githubusercontent.com/4485129/115702890-18633780-a387-11eb-96f5-5c7f1919b056.png)

As the diagram shows, Lake Formation manages AWS Glue crawlers, AWS Glue ETL jobs, the Data Catalog, security settings, and access control. After the data is securely stored in the data lake, users can access the data through their choice of analytics services, including Amazon Athena, Amazon Redshift, and Amazon EMR.  

Read more about Amazon Lake Formation here: https://docs.aws.amazon.com/lake-formation/latest/dg/what-is-lake-formation.html

