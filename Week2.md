# Week 2
## AWS Data Related Services

* Introduction to Week 2
### AWS Data Lake Related Services

The datalake services can be divided in theree aspects..
* Data storage and cataloging aspect. 
* Data movement aspect. 
* Data analytics and processing aspect

Data Lake has decoupled layers which allows for users to manage and scale and secure each individual building block of it independently

### Amazon S3
* Data Agnostic 
* Data of different types should not be different silios
* 99.999999999.% durability
* S3 offers tier based storage based on frequency of use.
* S3 has intelligent tier identification 
![image](https://user-images.githubusercontent.com/4485129/118358878-778b2500-b59e-11eb-9f60-0b4028cfeca4.png)

### AWS Glue Data Catalog
* AWS Glue is a fully managed
* Serverless data processing and cataloging service.
* A glue crawler is triggered to sort through your data in S3 and calls classifier logic to infer the schema, format, and data type. They will construct a data catalog using existing classifiers for popular asset formats like JSON
 
### Reading: Amazon S3 and Glue Data Catalog

### AWS Services Used for Data Movement
Kinesis Firehose ingest data from sources in real-time
Data lake on AWS will be formed by data coming from various places and the tools that you use for data ingestion will vary as well. You can use a service from the Kinesis family for real-time data ingestion, Amazon API Gateway for RESTful data ingestion, App flow for data ingestion from SaaS applications, Data Exchange, or the Registry of open data for public datasets that you want to ingest into your data lake.

### Data lake on AWS will be formed by data coming from various places and the tools that you use for data ingestion will vary as well. 
* Kinesis family for real-time data ingestion
* Amazon API Gateway for RESTful data ingestion
* App flow for data ingestion from SaaS applications
* Data Exchange, or the Registry of open data for ingestion of public datasets

### Reading: Data Movement

<details><summary>CLICK ME</summary>

#### Data Movement

Data Lakes allow you to import any amount of data that can come in real-time. Data is collected from multiple sources, and moved into the data lake in its original format. This process allows you to scale to data of any size, while saving time of defining data structures, schema, and transformations.   

Read more about data lakes on AWS here: https://aws.amazon.com/big-data/datalakes-and-analytics/https://aws.amazon.com/big-data/datalakes-and-analytics/what-is-a-data-lake/  

##### Amazon Kinesis 
Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information. Amazon Kinesis offers key capabilities to cost-effectively process streaming data at any scale, along with the flexibility to choose the tools that best suit the requirements of your application. With Amazon Kinesis, you can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications. Amazon Kinesis enables you to process and analyze data as it arrives and respond instantly instead of having to wait until all your data is collected before the processing can begin.     

There are multiple services in the Amazon Kinesis family. For data ingestion, there is Amazon Kinesis Data Streams, Amazon Kinesis Video Streams, and Amazon Kinesis Data Firehose.   Read more about Amazon Kinesis here: https://aws.amazon.com/kinesis/    

To better understand each service please review the diagrams below.       

###### Amazon Kinesis Video Streams:    
![image](https://user-images.githubusercontent.com/4485129/118362362-e2dbf380-b5ac-11eb-87f5-0b78ccdf3120.png)


###### Amazon Kinesis Data Streams:     
![image](https://user-images.githubusercontent.com/4485129/118362369-e7081100-b5ac-11eb-92b4-246c1260f954.png)

###### Amazon Kinesis Data Firehose:
![image](https://user-images.githubusercontent.com/4485129/118362377-ec655b80-b5ac-11eb-9261-d4144ccc2aab.png)


#### Amazon API Gateway   
Amazon API Gateway is a fully managed service that makes it easy to create, publish, and maintain secure APIs at scale. APIs are the front door to backend applications and services. API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, CORS support, authorization and access control, throttling, monitoring, and API version management.   

Read more about API Gateway here: https://aws.amazon.com/api-gateway/

</details>

### AWS Services for Data Processing
### AWS Services for Analytics
### AWS Services for Predictive Analytics and Machine Learning
### Reading: EMR, Glue Jobs, Lambda, Kinesis Analytics, RedShift
<details><summary>CLICK ME</summary>

### EMR, Glue Jobs, Lambda, Kinesis Analytics, RedShift
#### Apache Hadoop on AWS   
Apache Hadoop is an open source framework that is used to efficiently store and process large datasets ranging in size from gigabytes to petabytes of data. Instead of using one large computer to store and process the data, Hadoop allows clustering multiple computers to analyze massive datasets in parallel more quickly.   

Read more about Hadoop here: https://aws.amazon.com/emr/details/hadoop/what-is-hadoop/  

#### Amazon EMR    
Amazon EMR is a managed cluster platform that simplifies running big data frameworks, such as Apache Hadoop and Apache Spark, on AWS to process and analyze vast amounts of data. By using these frameworks and related open-source projects, such as Apache Hive and Apache Pig, you can process data for analytics purposes and business intelligence workloads. Additionally, you can use Amazon EMR to transform and move large amounts of data into and out of other AWS data stores and databases, such as Amazon Simple Storage Service (Amazon S3) and Amazon DynamoDB.   

Read more about Amazon EMR here: https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html    

#### AWS Glue Jobs   
A job is the business logic that performs the extract, transform, and load (ETL) work in AWS Glue. When you start a job, AWS Glue runs a script that extracts data from sources, transforms the data, and loads it into targets. You can create jobs in the ETL section of the AWS Glue console.    

![image](https://user-images.githubusercontent.com/4485129/118406737-c61de980-b69a-11eb-9b8d-d92261593771.png)

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

### Introduction to AWS Lake Formation

### Reading: AWS Lake Formation

<details><summary>CLICK ME</summary>
 
#### AWS Lake Formation
AWS Lake Formation makes it easier for you to build, secure, and manage data lakes. Lake Formation helps you do the following, either directly or through other AWS services:  

* Register the Amazon Simple Storage Service (Amazon S3) buckets and paths where your data lake will reside.
* Orchestrate data flows that ingest, cleanse, transform, and organize the raw data.
* Create and manage a Data Catalog containing metadata about data sources and data in the data lake.
* Define granular data access policies to the metadata and data through a grant/revoke permissions model.

The following diagram illustrates how data is loaded and secured in Lake Formation.
![image](https://user-images.githubusercontent.com/4485129/118407099-b7383680-b69c-11eb-8a53-58df7f939f45.png)

As the diagram shows, Lake Formation manages AWS Glue crawlers, AWS Glue ETL jobs, the Data Catalog, security settings, and access control. After the data is securely stored in the data lake, users can access the data through their choice of analytics services, including Amazon Athena, Amazon Redshift, and Amazon EMR.  

Read more about Amazon Lake Formation here: https://docs.aws.amazon.com/lake-formation/latest/dg/what-is-lake-formation.html
</details>

### Ungraded External Tool: Ungraded External ToolLab 1 Prompt: Lab 1 Discussion
