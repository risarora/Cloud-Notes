## Introduction to Data Lakes
The goal of this course is to equip you with the knowledge needed to understand what exactly a data lake is. And how to use AWS data related services to create and operate a data lake in a secure and scalable way. 

## Introduction to Week 1
## Why Data Lakes
The main reasons to invest in a data lake are: to increase operational efficiency, make data available from departmental silos, lower transactional costs, and offload capacity from databases and data warehouses.     
Datalake have storage and processing mechanisms decoupled.
* Cheaper and more versatile.
Decoupling storage from data processing, user can use different data processing and data visualization components that look at the same data,
Store your data without having to think about its structure

## Characteristics of Data Lakes
* data-agnostic. 
* future proof
There are two kinds of processing involved in a data lakes.    
* First is the process made before or while ingesting data. 
* Second is process made after data has been stored. This process includes, but is not limited to cleansing, aggregating and reaching, merging with other datasets, and much more. 

## Data Lakes Components
Four main components
* Ingest and store
    For low latency at scale and realtime processing we use data streaming technologies Kinesis family or Amazon Managed Streaming for Apache Kafka.
    For normal ingestion we could use ingestion mechanism that consumes data in batches.
* Catalog and search 
    Mature data lakes provide efficient indexing and searching
* Process and serve 
    AWS Glue which execute Hadoop jobs on demand where you only pay when there is a job running.
* Protect and secure 
secure way with configurable permission mechanisms that prevent unauthorized users from accessing the data

## Comparison of a Data Lake to a Data Warehouse
schema-on-write architecture
AWS has a service called Amazon Athena that allow you to match the table schema to your dataset and not the datasets to your table schema

Data Lakes and Data Warehouses
Data Lakes compared to Data Warehouses – Two Different Approaches 
Depending on the requirements, a typical organization will require both a data warehouse and a data lake as they serve different needs, and use cases. 

A data warehouse is a database optimized to analyze relational data coming from transactional systems and line of business applications. The data structure, and schema are defined in advance to optimize for fast SQL queries, where the results are typically used for operational reporting and analysis. Data is cleaned, enriched, and transformed so it can act as the “single source of truth” that users can trust. 

A data lake is different, because it stores relational data from line of business applications, and non-relational data from mobile apps, IoT devices, and social media. The structure of the data or schema is not defined when data is captured. This means you can store all of your data without careful design or the need to know what questions you might need answers for in the future. Different types of analytics on your data like SQL queries, big data analytics, full text search, real-time analytics, and machine learning can be used to uncover insights. 

As organizations with data warehouses see the benefits of data lakes, they are evolving their warehouse to include data lakes, and enable diverse query capabilities, data science use-cases, and advanced capabilities for discovering new information models. Gartner names this evolution the “Data Management Solution for Analytics” or “DMSA.”

### Data warehouse vs. Data lake
![It5HCGkWSfqeRwhpFnn6WQ_b75153889ebf412e91cd07b1bddc9309_image-1-](https://user-images.githubusercontent.com/4485129/117894992-23045300-b2db-11eb-817a-d0c5db505f97.png)


### Data warehouse vs. Database
![gpJapWkaSAmSWqVpGugJDw_a5509ea0cbe74a62b687d04d9fe3ef1e_image-2-](https://user-images.githubusercontent.com/4485129/117895118-58a93c00-b2db-11eb-962c-21db995eee40.png)


![image](https://user-images.githubusercontent.com/4485129/118341454-d8821100-b53c-11eb-8c7b-a632d5a13770.png)
  
