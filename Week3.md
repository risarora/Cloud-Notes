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

* Amazon Kinesis Data Streams
* Kinesis Analytics
* Kinesis Firehose
* Kinesis Video Streams
#### Data Retension 
Kinesis works by pull mechanism. The consumer 
### Reading: Diving Deep on Amazon Kinesis

<details>

#### AWS Kinesis Family 
Amazon Kinesis makes it easy to collect, process, and analyze real-time, streaming data so you can get timely insights and react quickly to new information. Amazon Kinesis offers key capabilities to cost-effectively process streaming data at any scale, along with the flexibility to choose the tools that best suit the requirements of your application. With Amazon Kinesis, you can ingest real-time data such as video, audio, application logs, website clickstreams, and IoT telemetry data for machine learning, analytics, and other applications. Amazon Kinesis enables you to process and analyze data as it arrives and respond instantly instead of having to wait until all your data is collected before the processing can begin.

More info: https://aws.amazon.com/kinesis/

#### Amazon Kinesis Data Streams
Amazon Kinesis Data Streams (KDS) is a massively scalable and durable real-time data streaming service. KDS can continuously capture gigabytes of data per second from hundreds of thousands of sources such as website clickstreams, database event streams, financial transactions, social media feeds, IT logs, and location-tracking events. The data collected is available in milliseconds to enable real-time analytics use cases such as real-time dashboards, real-time anomaly detection, dynamic pricing, and more.

More info: https://aws.amazon.com/kinesis/data-streams/

#### Amazon Kinesis Firehose
Amazon Kinesis Data Firehose is the easiest way to reliably load streaming data into data lakes, data stores, and analytics services. It can capture, transform, and deliver streaming data to Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, generic HTTP endpoints, and service providers like Datadog, New Relic, MongoDB, and Splunk. It is a fully managed service that automatically scales to match the throughput of your data and requires no ongoing administration. It can also batch, compress, transform, and encrypt your data streams before loading, minimizing the amount of storage used and increasing security.

More info: https://aws.amazon.com/kinesis/data-firehose/?kinesis-blogs.sort-by=item.additionalFields.createdDate&kinesis-blogs.sort-order=desc

#### Amazon Kinesis Data Analytics
Amazon Kinesis Data Analytics is the easiest way to transform and analyze streaming data in real time with Apache Flink. Apache Flink is an open source framework and engine for processing data streams. Amazon Kinesis Data Analytics reduces the complexity of building, managing, and integrating Apache Flink applications with other AWS services. Amazon Kinesis Data Analytics takes care of everything required to run streaming applications continuously, and scales automatically to match the volume and throughput of your incoming data. With Amazon Kinesis Data Analytics, there are no servers to manage, no minimum fee or setup cost, and you only pay for the resources your streaming applications consume.

More info: https://aws.amazon.com/kinesis/data-analytics/

#### Amazon Kinesis Analytics In-Application Streams and Pumps
When you configure application input, you map a streaming source to an in-application stream that is created. Data continuously flows from the streaming source into the in-application stream. An in-application stream works like a table that you can query using SQL statements, but it's called a stream because it represents continuous data flow.

More info: https://docs.aws.amazon.com/kinesisanalytics/latest/dev/streams-pumps.html
</details>

### Batch Data Ingestion with AWS Transfer Family
### Batch Data Ingestion with AWS Snow Family
### Reading: Batch Data Ingestion with AWS Services
### Data Cataloging
### Using Glue Crawlers
### Reading: The Importance of Data Cataloging
### Reviewing the Ingestion Part in Data Lake Architectures
### External ToolLab 2
