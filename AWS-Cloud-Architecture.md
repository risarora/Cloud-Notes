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

### 2. Data Movement

### 3.  analytics and processing

