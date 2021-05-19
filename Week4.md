

## Processing Data in the Data Lake
### Introduction to Week 4
### Data Prep and AWS Glue Jobs
* Leaving data in its raw format is a great idea. Others can prep the data the way that they see fit.
* The data is then moved to chaper s3 storages as the data ages
* Users can use S3 lifecycle policies to move raw data to more cost-effective storage tiers as it becomes more infrequently accessed over time.
* Multiple types of Dataprep that you might create process for. 
 * **Shaping**

![image](https://user-images.githubusercontent.com/4485129/118804680-a0732900-b8c2-11eb-9c6e-5f95b5b630a3.png)

* Lambda is best used for transformation of real-time data since you can trigger Lambdas to run as data comes in.
* Glue Jobs is best used for processing data in batches.

AWS Glue has three main components. 
* Glue data catalog, 
* The crawlers and the classifiers
* Glue Jobs.
  * A job is the business logic that performs the ETL work in AWS Glue.

* Choose a data source for your job
* Choose a data target. This is where the data that gets transformed will be loaded.
* then provide customized configurations for your job,

You could run your job as an Apache ETL script, a Spark streaming script, or a Python shell script.
You can choose to let Glue generate a script for you, or you can provide an S3 location with a script that you have already written for the job to use
* Configure the transformation type 
    * User can change the schema of a source data and create a new target dataset
    * or User can find matching records.

### File Optimizations
* Columnar data is optimum for most big data and data lake related queries as they mainly do aggregate operations 
* Columnar data formats are also optimized for compression.
* If you have a data set with columnar data format, and do a query that scans entire columns. 
Under the hood, Athena will perform S3 partial GET operations, which will get only the specific part of S3 objects that contains the columns you were looking for.

* File Optimization 
    * file formats
    * compression 
    * partitioning
    * optimizations 
    * Dataprep 
Because of cost and performance,

### Using S3, Glue and Athena to Get Insights about NYC Taxi Data
### Reading: Columnar Data Formats and Amazon Athena Optimizations
#### Columnar Data Formats and Amazon Athena Optimizations
##### Columnar Data Format and Athena Partitioning
<details><summary>CLICK ME</summary>
**Apache Parquet** and **ORC** are columnar storage formats that are optimized for fast retrieval of data and used in AWS analytical applications.Columnar storage formats have the following characteristics that make them suitable for using with Athena:

* Compression by column, with compression algorithm selected for the column data type to save storage space in Amazon S3 and reduce disk space and I/O during query processing.
* Predicate pushdown in Parquet and ORC enables Athena queries to fetch only the blocks it needs, improving query performance. When an Athena query obtains specific column values from your data, it uses statistics from data block predicates, such as max/min values, to determine whether to read or skip the block.
* Splitting of data in Parquet and ORC allows Athena to split the reading of data to multiple readers and increase parallelism during its query processing.

Read more here: https://docs.aws.amazon.com/athena/latest/ug/columnar-storage.html

By partitioning your data, you can restrict the amount of data Athena scans by each query, thus improving performance and reducing cost. Athena leverages Hive for partitioning data. You can partition your data by any key. A common practice is to partition the data based on time, often leading to a multi-level partitioning scheme. 

Read more here: https://docs.aws.amazon.com/athena/latest/ug/partitions.html 
#### AWS Glue Jobs   

An AWS Glue job encapsulates a script that connects to your source data, processes it, and then writes it out to your data target. Typically, a job runs extract, transform, and load (ETL) scripts. Jobs can also run general-purpose Python scripts (Python shell jobs.) AWS Glue triggers can start jobs based on a schedule or event, or on demand. You can monitor job runs to understand runtime metrics such as completion status, duration, and start time.   

AWS Glue provides a set of built-in transforms that you can use to process your data. You can call these transforms from your ETL script. Your data passes from transform to transform in a data structure called a DynamicFrame, which is an extension to an Apache Spark SQL DataFrame. The DynamicFrame contains your data, and you reference its schema to process your data.   

Read more about transforms here: https://docs.aws.amazon.com/glue/latest/dg/built-in-transforms.html   

Read about working with Glue Jobs here: https://docs.aws.amazon.com/glue/latest/dg/console-jobs.html    
<details>

### Introduction to Data Lake Security
### Reading: Security and Compliance

## Data Visualization
### The Power of Data Visualization
### Introduction to Amazon QuickSight
### Amazon QuickSight Demo
### Reading: Data visualization, Amazon QuickSight
### Registry of Open Data on AWS
### Reading: Registry of Open Data
### Ungraded External Tool: Ungraded External ToolLab 3
### Discussion Prompt: Lab 3 Discussion
