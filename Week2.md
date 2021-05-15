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
 
* Reading: Amazon S3 and Glue Data Catalog
<define>
</define>



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
