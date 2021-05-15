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

### AWS Services Used for Data Movement
Kinesis Firehose ingest data from sources in real-time
Data lake on AWS will be formed by data coming from various places and the tools that you use for data ingestion will vary as well. You can use a service from the Kinesis family for real-time data ingestion, Amazon API Gateway for RESTful data ingestion, App flow for data ingestion from SaaS applications, Data Exchange, or the Registry of open data for public datasets that you want to ingest into your data lake.

### Data lake on AWS will be formed by data coming from various places and the tools that you use for data ingestion will vary as well. 
* Kinesis family for real-time data ingestion
* Amazon API Gateway for RESTful data ingestion
* App flow for data ingestion from SaaS applications
* Data Exchange, or the Registry of open data for ingestion of public datasets

### Reading: Data Movement
### AWS Services for Data Processing
### AWS Services for Analytics
### AWS Services for Predictive Analytics and Machine Learning
### Reading: EMR, Glue Jobs, Lambda, Kinesis Analytics, RedShift
### Introduction to AWS Lake Formation
### Reading: AWS Lake Formation
### Ungraded External Tool: Ungraded External ToolLab 1 Prompt: Lab 1 Discussion
