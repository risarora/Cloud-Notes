# AWS Data Lake
![image](https://user-images.githubusercontent.com/4485129/115526354-8f2c0200-a2ad-11eb-836d-9bb8de0c47f1.png)

# Week 2
We'll explore AWS services that can be used in data lake architectures, like Amazon S3, AWS Glue, Amazon Athena, Amazon Elasticsearch Service, LakeFormation, Amazon Rekognition, API Gateway and other services used for data movement, processing and visualization.

1. Storage and cataloguing
2. Data Movement
3.  analytics and processing


### 1. Storage and cataloguing
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

<describe>
 
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

</describe>


### 2. Data Movement
#### AWS API Gateway

![image](https://user-images.githubusercontent.com/4485129/115541722-19c82d80-a2bd-11eb-9a68-eb1f6d60f100.png)

![image](https://user-images.githubusercontent.com/4485129/115542303-c60a1400-a2bd-11eb-81a5-56e1a3ddd910.png)



### 3.  analytics and processing

