# Week 3

In Week 3, you'll explore specifics of data cataloging and ingestion, and learn about services like AWS Transfer Family, Amazon Kinesis Data Streams, Kinesis Firehose, Kinesis Analytics, AWS Snow Family, AWS Glue Crawlers, and others. You'll also discover when is the right time to process data--before, after, or while data is being ingested. Given scenarios, you'll be able to easily identify when to process data and match the most appropriate AWS services to each scenario.

## Learning Objectives
* Differentiate between structured and unstructured data
* Identify the right time to ingest data
* Differentiate between batch and steaming data ingestion
* Discover the benefits of data cataloging
* Analyze data ingestion in an architectural diagram

### Introduction to Week 3
This week will cover Kineses
* AWS Kinesis Firehose
* AWS Kinesis Datastreams
* AWS Kinesis Lake
* AWS Snow Family
* AWS Transfer Family

### Use the Right Tool for the Job
The tools used for data ingestion totally depend upon the data structure, type and pupose of data ingestion. 
* Auto-generated data, such as data generated from IoT devices or server logs. 
  * Streaming - unstructured
  * Ingest with Amazon Kinesis, store in Amazon S3, catalog with AWS Glue, process with Lambda and query with Amazon Athena. 

* Operational data, such inventory and sales, expense reports, and other inputs. 
  * Batch - Semi Structured 
  * Data is consumed by people who wants to visualize graphs and have access to statistics. 
  * Ingested with API Gateway, stored in S3, catalogs with Glue, transported to Amazon Elasticsearch Service and visualized with Kibana.

* Human-generated data, such as social media feeds, contact forms, call center audio, e-mails, etc. 
  * Batch - Semi Structured
  * For use by Data Analysis Services. 
  * You could ingest that data with S3, SFTP or Upflow, store it in S3, catalog with Glue and use a service like Amazon Comprehend, which is a natural language processing service that uses machine learning to find insights in texts, such as sentimental analysis. 

### Understanding Data Structure and When To Process Data

When we do not want to alter the raw data then classic ELT is performed
Eg. Interplaterary data 

Data lakes prefer **ELT** instead of **ETL**
For Medical records we can remove the **pII (personally Identifiable Information)** from data before storing data in *S3*
After loading in s3 data can be processed.
Why image and data not processed at same time.

1. Different type of services are used.
2. Data needed not available at curent time.

This iscalled **EtLT**

### Data Streaming Ingestion With Kinesis Services
### Reading: Diving Deep on Amazon Kinesis
### Batch Data Ingestion with AWS Transfer Family
### Batch Data Ingestion with AWS Snow Family
### Reading: Batch Data Ingestion with AWS Services
### Data Cataloging
### Using Glue Crawlers
### Reading: The Importance of Data Cataloging
### Reviewing the Ingestion Part in Data Lake Architectures
### External ToolLab 2
