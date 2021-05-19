

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
### Using S3, Glue and Athena to Get Insights about NYC Taxi Data
### Reading: Columnar Data Formats and Amazon Athena Optimizations
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
